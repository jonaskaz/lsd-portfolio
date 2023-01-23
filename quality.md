# Re-Designing and Building Olin Hydroponics Club's Automation System

## Introduction

This semester I re-designed Olin Hydroponics Club's automation system. Olin Hydroponics (Hydro) is a subteam of a club at Olin called Public Interest Technology (PiNT). Hydro is focused on exploring the intersection of agriculture, technology, food, and people as well as building an automated hydroponics garden on campus.

Hydroponics is a type of horticulture where plants are grown out of soil, either in an inert medium or directly in water. Typically in a hydroponics system water is pumped to plants from a large reservoir of water. This reservoir of water is measured using sensors and solutions are added to it so that it is hospitable and nutritious to the plants.

In previous years Hydro built an automation system that performed the following:

- Measure and adjust the ph of the water reservoir using a pump
- Measure the electrical conductivity of the water and dispense nutrients using a pump as needed
- Turn on a water pump and lights periodically
- Measure the temperature of the water

This semester we continued with this work by taking what we learned in the previous iteration and designing a new system.

## Design Decisions

A description of the previous automation architecture can be found [here](https://docs.google.com/document/d/1Pc2PLaOh7dCDCJWnpELBCgfNip4MotUVfBgKtQ5LqRU/edit?usp=sharing).

### Maintainability

In our first design of this automation system we did not define standard interfaces between our components. This made each service tightly coupled to each other, often requiring changes across the entire stack when making updates.

To address this, we defined message types that will be sent and received within our system. These message types offer structure to design around and flexibility to withstand future changes. The message types are commands and schedules.

**Command**  
A command is a way to tell the gardener to act on a sensor or a switch in JSON format.

Sensor commands tell the gardener to collect sensor data for a specific sensor referenced by its id. Example sensor command:

```
{
    "type": "sensor",
    "id": 1
}
```

Actuator commands tell the gardener to turn a switch on (1) or off (0). The actuator is referenced by its id. Example actuator command:

```
{
    "type": "actuator",
    "id": 1,
    "cmd": 0
}
```

Commands can be sent to the gardener to act immediately, or they can also be sent as a part of a schedule.

### Scale

Our previous design was only set up to be able to manage a few gardens. We designed our new system to be able to scale up to 1000 gardens if needed. To do this, we moved much of our computation into the cloud which allows us to scale without needing as much hardware. We also designed mother nature to be able to control multiple Gardeners/gardens at once, reducing the need to deploy additional services as we scale.

### Transparency

Our system is designed to make it as clear as possible what the system has done, is doing, and will do in the future. To do this, we moved scheduling to the cloud allowing us to easily log schedules and know when actions will be taking place. Further, when the Gardener performs an action it sends a request to the Data API logging that action. This can help us understand what actions have been performed and when the Gardener is not acting as instructed.

### Robustness

When computation is moved to the cloud the system becomes more dependent on internet connection. We created a 24 hour schedule that is sent to the Gardener to reduce this connection dependency. If the Gardener loses internet access it can continue to execute its 24 hour plan until connection is restored.

## New Architecture Diagram

![Version 2 Architecture](/images/HydroV2Architecture.jpg)

### Mother Nature

[Github Repository](https://github.com/Olin-Hydro/mother-nature)  
Mother Nature is our high level controller where all decisions are made. Mother nature generates 24 hour schedules of when operations in the garden should occur, and sends them to the Gardener to execute. Mother nature also checks the latest sensor data and will send immediate commands to the Gardener to adjust conditions as needed.

### Gardener

[Github Repository](https://github.com/Olin-Hydro/gardener)  
The Gardener is a microcontroller that lives on the physical hydroponics garden and is wired to sensors and pumps. The Gardener is responsible for interfacing with pumps and sensors to collect data, turn on actuators (pumps and lights), and send information to our Data API.

### Data API (Hydrangea)

[Github Repository](https://github.com/Olin-Hydro/hydrangea)  
The Data API is a simple REST wrapper around a mongo database. This API will be responsible for receiving data from the Gardener and Web-UI, and making it easily accessible.

### Web-UI (Saffron)

[Github Repository](https://github.com/Olin-Hydro/saffron)  
The Web-UI is a dashboard for viewing sensor data and adjusting system parameters. This website will begin as an internal tool but we eventually want to open up a portion of it for engagement with the Olin Community.

## Testing

### Mother Nature

Mother nature is written using interfaces which allows for robust unit testing. The mockgen library is used which creates mock interfaces where the behavior can be defined within a test. This allows interdependent components to be tested individually by mocking dependencies ([example](https://github.com/Olin-Hydro/mother-nature/blob/main/tests/main_test.go)). This is especially useful in the http package which allows us to mock any http request in a test ([link](https://github.com/Olin-Hydro/mother-nature/blob/main/mocks/http.go)). By setting up these testing systems we have caught numerous bugs that would have gone unnoticed. For example, by adding unit tests that checked the creation of our requests we found that our urls were not getting encoded properly and were able to fix the bug: [test link](https://github.com/Olin-Hydro/mother-nature/blob/4a11f91bef0c1a770ec03617d5d4e35ebaecd188/tests/storage_test.go#L38)

### Data API

FastAPI comes with a built in test client which we used for testing the Data API. For testing each route a test database is used, and the collections created in the tests are removed at the end of the testing. [Testing Example](https://github.com/Olin-Hydro/hydrangea/blob/main/App/server/tests/test_gardens.py). This testing gave us more confidence in the functionality of our API and made it more clear to future developers how the API can be used.

The other services in our architecture are still in early development and testing procedures are being developed.

## Conclusion

The above automation architecture for Hydroponics demonstrates my ability to plan software architecture and create unit tests. Looking back I am glad we spent a long time designing the new system before building it. Having built the system once gave us insight into how it can be improved. In the future I want to place more emphasis on testing earlier on. Testing was often added towards the end of our development cycle and it caused us to get stuck on many bugs.
