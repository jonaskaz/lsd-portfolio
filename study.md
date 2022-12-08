# Understanding Software Outsourcing
## Introduction

Outsourcing has become ubiquitous in software development teams for its potential strategic, economic, political and technological benefits[1]. According to the National Outsourcing Association[2] 70% of buyers plan to increase their use of outsourcing, with 35% planning to significantly. Despite this growing interest, a review of global outsourcing[3] found that 20 to 25% of all outsourcing relationships fail within two years, and 50% fail within five. It is becoming increasingly important for organizations to think critically about their use of outsourcing in software development.


This study will compare projects developed externally to internally developed projects. This research study design outlines one metric to investigate that can help inform organizations on the past success of their outsourcing projects. This information is valuable in deciding how future projects should be developed. This study sets out to answer the question: do projects that are outsourced to external development teams experience more bugs than internally developed projects? 

## Study Design

This study is designed to explore the past behavior of projects, therefore no behavior changes or set up is required in the organization being studied. In order to perform the study, a few definitions of the metrics being used should be outlined:

### Bug
A bug is an unintended behavior of the software that requires an update to the code

We must consider that each organization may have different definitions for what constitutes a bug. This metric will need to be approximated to the closest possible match given the above definition. In organizations that use github and github issues to track bugs, paying close attention to the tags used is important. If a new feature also includes a bug fix, it should be considered a bug. If an unexpected behavior is identified in the software but is not fixable by updating the code, for the purposes of this study it should not be considered a bug. We are focused on bugs that relate specifically to the code written that can give us a signal of the quality of the code.

### Number of bugs
The number of bugs identified in each internal/external project

The number of bugs will not always be available to count at every organization. This study is only feasible where bugs identified in the software are tracked and logged. It is not uncommon for one bug to relate to other bugs, making it difficult to determine what constitutes a single bug. For the purpose of this study, consistency in how bugs are counted is more important than correctness. For example take the case that an organization lists a bug multiple times despite it being related to a single code change that is required. In this case we recommend counting this as multiple bugs in order to capture the impact of the bug. However, this bug could also be counted as a single bug so long as future bugs are also counted in this way.

### Project Development lifetime
The length of time each internal/external project has existed: time since first contribution in code to the last contribution in days

The start date of a project should be clear if the project has a version history. In the case that a project was created, but development did not start actively until later, the first contribution that marks the beginning of active development should be used. The version history should also be used to find the last contribution time. 

### Code quality
The number of bugs / project lifetime

This metric is a combination of the above metrics and will be used to compare internal and external projects. This metric represents roughly the number of bugs found per day during the lifetime of a project.

## Data Collection

In order to collect the data to perform this study, it is important to understand the tools used at the given organization. As an example, consider the case that an organization uses github to store project repositories and github issues to track bugs. 

To collect data, go to each repository and count the total number of issues raised that are tagged with the term most closely matching the definition for “bug”. This data should be stored so that the number of bugs for each repository is tracked.

Next, go to each repository and find the time of the first commit. This is the starting time. Find the time that the last commit was added to the project. This is the ending time. The difference between these times in days is the project lifetime. 

For each repository, divide the number of bugs by the project lifetime. This value can be considered the code quality. The mean code quality across all projects internally can be compared to the code quality across external projects. This can give you a signal to understand the possible differences in quality between internal and external projects.

## Validity

The data collection techniques are relatively rudimentary, and do not capture all the possible edge cases. For example, the severity of a bug is not captured in this analysis. For example, a bug that takes weeks to find and solve is weighted the same as a bug that requires a single line change. This could be improved by taking into acount the number of lines required to solve the bug. Additionally, the projects can be decomissioned due to poor quality or inability to maintain them. This will be accounted for in this study. This study could be improved by explanding the metrics used in it. For example, it could also measure the number of engineering hours needed in each project.

## Conclusion

Understanding the code quality between internal and external projects can help organizations understand the benefits and drawbacks of outsourcing. The metric outlined in this study only captures a sliver of the whole picture of what constitues quality code. However, we do know bugs are costly and are an important indicator of the quality of code [4]. We hope that this study will help organizations make more informed decisions on development outsourcing.


## Sources

[1] Abbas, Rasha & Dart, Philip & O'Brien, Fergus & Kazmierczak, Edmund. (1998). Outsourcing for software applications development: issues, implications and impact.. 628-642. https://www.researchgate.net/publication/221408519_Outsourcing_for_software_applications_development_issues_implications_and_impact

[2] Coward, Jeremy. “Outsourcing in 2020.” National Outsourcing Association, 2016, https://www.gsa-uk.com/resources/Documents/outsourcing%20in%202020.pdf

[3] Andriole, Steve. “Vanguard and Infosys Are Now Billion Dollar Outsourcing Partners. Good, Bad and Always Risky.” Forbes, Forbes Magazine, 3 Aug. 2020, https://www.forbes.com/sites/steveandriole/2020/08/02/vanguard--infosys-are-now-billion-dollar-outsourcing-partners-good-bad--risky/?sh=69027f702672. 

[4] Jones, Capers, et al. The Economics of Software Quality. Addison-Wesley, 2012, https://books.google.com/books?hl=en&lr=&id=oEPjYVfUR1wC&oi=fnd&pg=PR9&dq=cost+economic+of+a+software+bug+in+code&ots=bbz6RriUDD&sig=vXaiqD8-He4O2vlofAo5g5wAvKY#v=onepage&q=cost%20economic%20of%20a%20software%20bug%20in%20code&f=false

