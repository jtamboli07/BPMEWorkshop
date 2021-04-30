# Understanding Case Management Framework Implementation
Case Management bring a lot of functionality to a BPM solution implementation. All the implementation capabilities are not that obvious. We created this lab to illustrate this implementation methodology. 

This slide below is a good illustration of such an implementation. 

![build_project](images/buildproject/8.png)

In this implementation we created is a solution that makes use of both long running as well as short lived processes. We have some customer solutions that use only short lived processes (Case Actions and/or Business Services) for their entire banking fraud management back office solution. One thing that short lived processes does not do is managing SLA's/timer events, this type of functionality ensures work gets done in a predefined time. 

Case Management provides a lot of flexibility on top the normal BPM solution. Using case management, the long running process steps are replaced with states/milestones that makes up an end to end process. These states/milestones are not statically linked. A long running process are modelled to execute steps of a process in sequence or in parallel, the state model allows you to process multiple state processes in any order based on the business rules for the process execution. The ability to create CRUD processes that are stateless (case actions or business services) allows user to update case state without the need to process a work item associated with a process step. 

Take this process below. In this process every step needs to be executed in the order that it is modeled. If the order of the steps needs to be changed, the process definition needs to change and the process needs to be re-deployed. Re-deploying a long running process requires migration of existing process instances that takes effort and careful consideration. 

![build_project](images/buildproject/9.png)

In the process below we defined the major states/milestones for a support process for fault resolution. As you can see, every state is defined as a stateless process. Because the state processes are stateless, it brings flexibility in that the user can update the state through a stateless process and based on the business rules, the process will be processed to the next appropriate state. Another benefit is that a stateless process is much easier to upgrade in place as there is no need to migrate data that may be associated with a long running process. Stateless processes fetch data in the central repository at the current state to present to the user. Case actions are also called CRUD processes as they allow the user to modify data associated with a case. 

Stateless processes isn't always the appropriate way to progress a process from state to state. Some times, long running processes is required to keep track of SLA. Using the Case Management Framework (CMF) we created a methodology to dynamically manage stateful processes associated with specific states. This methodology is dynamic and allows solutions to be extremely agile. 

![build_project](images/buildproject/10.png)

At the center of this implementation methodology lies the case data repository. This repository we also have the ability to store document. The BPME engine as a built in lightweight document store that allow the system to upload and store documents of many types, like pdf's, word, excel etc.



![build_project](images/buildproject/31.png)

Processes as well as case actions can interact with others systems of record by implementing BW/CE as part of the processes.

![build_project](images/buildproject/30.png)

