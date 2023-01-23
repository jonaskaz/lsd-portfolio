# Hydro Automation Collaboration

This semester I worked on the second revision of Hydro's Automation Architecture. I worked mainly with 1 peer collaborator and a group of ~5 first years/sophomores on this development. Working in a group of this size required deliberate processes to encourage productive collaboration; below are the processes and resources created to facilitate this.

## Team Values

We created a document that contained the values we hope to embody in the team. The values and their description can be found [here](https://docs.google.com/document/d/1-OJNvd0kenk9DHmTYejzCaRjYyAjlhd418WMiSivKus/edit). We presented these values to the team and accepted any feedback or changes that members wanted to add. We found that this enabled some members to operate with more autonomy on the project. I worked with a student who was designing a custom PCB and he was able to complete the design without my direct support by the end of the semester. In the past completing independent projects like this would typically involve more guidance and therefore span beyond a semester.

I also gave a presentation to the entire PiNT organization to explain how Hydro thinks about their impact as an organization. This was intended to help give each team member agency and motivation to explore their interests freely. This presentation can be found [here](https://docs.google.com/presentation/d/1-0RsYcsTI9V0iFOwBBgDNXiJhX1RRLCftFCTicgvpvw/edit?usp=sharing).

## Facilitating Knowledge Transfer

As there were many members of the automation team that did not have experience writing software, I took time to explain many of the concepts and tools that we are using. I gave tutorials/demos on how to use github, how to set up Platformio, and how to interact with our graphql API. For some of these tutorials and demos I created references to go along with them [link](https://drive.google.com/drive/folders/1pWJFK-0sHZhJPD8K4xb3IIYOxR7ymnW-). Hydro also has an onboarding document that was created in the past that I updated with more up to date and relevant information [link](https://drive.google.com/drive/folders/1pWJFK-0sHZhJPD8K4xb3IIYOxR7ymnW-). All of these resources were used and created to help new and current members get up to speed with our new architecture and design. There were members that did not know Python or github before the project, and by the end of the semester they were able to contribute meaningfully with pull requests: [link](https://github.com/Olin-Hydro/hydrangea/pull/19).

## Code Review

We set up our Data API and Mother Nature repositories to require reviews before merging into main. By reviewing code, we caught a number of unclear items in our design specification. For example, in [this pull request](https://github.com/Olin-Hydro/hydrangea/pull/19) there was ambiguity in how we were storing dates and times for scheduling actuators. By reviewing code we caught this and decided on a standard of only looking at times instead of datetimes. Reviewing also helped us keep our documentation up to date because the reviewer could catch steps that were not added to the README: [link](https://github.com/Olin-Hydro/hydrangea/pull/14)

My code reviewed:

- https://github.com/Olin-Hydro/mother-nature/pulls?q=is%3Apr+is%3Aclosed

Reviewing others code:

- https://github.com/Olin-Hydro/hydrangea/pull/14
- https://github.com/Olin-Hydro/hydrangea/pull/7
- https://github.com/Olin-Hydro/hydrangea/pull/10
- https://github.com/Olin-Hydro/hydrangea/pull/16

Code review allowed our team to stay up to date on the progress in each project as well as get valuable feedback.

## Conclusion

The above work demonstrates my ability to document team values, facilitate knowledge transfer and review code. I found it extremely useful to write down our team values, however in the future I want to work on intentionally demonstrating these values and acknowledging when others on the team embody them. Code reviews were also a great change of pace and way to catch bugs early. I want to continue this practice going forward.
