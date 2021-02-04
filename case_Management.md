# Understanding Case Management Framework Implementation
Case Management bring a lot of functionality to BPM but all the implementation capabilities are not that obvious. We created this lab to illustrate this implementation methodology. 

This slide below is a good illustration of such an implementation. 

![build_project](images/buildproject/8.png)

In this implementation we created is a solution that makes use of both long running processes as well as short lived processes. We have some customers that used base short lived processes (Case Actions and/or Business Services) for their entire banking fraud management back office solution. One thing that short lived processes does not do is managing SLA's/Timer Events that ensures work gets done in a predefined time. 

Case Management provides a lot of flexibility on top the normal BPM solution. Using case management, the long running process steps are replaced with states/milestones that makes up an end to end process. These states/milestones are not statically linked. Where a long running process were modelled to execute steps of a process in sequence or in parallel, the state model allows you to process multiple states in any order based on the business rules for the process execution. The ability to create CRUD processes that are stateless allows user to update case state without the need to process a work item associated with a process step. 

Take this process below. In this process every step needs to be executed in the order that it is modeled. If the order of the steps needs to be changed, the process definition needs to change and the process re-deployed. 

![build_project](images/buildproject/9.png)

In the process below we defined the major states/milestones for a support process for fault resolution. As you can see, every state is defined as a stateless process. Because the state processes are stateless, the flexibility that it brings is that the user can update the state through a user interface and based on the business rules, the process will be processed to the next appropriate state. 

![build_project](images/buildproject/10.png)