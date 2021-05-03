# Understanding Case Management Framework Implementation
Case Management brings a lot of functionality to a BPM solution implementation. All the implementation capabilities are not that obvious. We created this lab to illustrate this implementation methodology. 

The slide below is a good illustration of such an implementation. 

![build_project](images/buildproject/8.png)

In this implementation we created is a solution that makes use of both long-running as well as short-lived processes. We have some custom solutions that use only short-lived processes (Case Actions and/or Business Services) for their entire banking fraud management back-office solution. One thing that short-lived processes do not do is managing SLA's/timer events, this type of functionality ensures work gets done in a predefined time. 

Case Management provides a lot of flexibility on top of the normal BPM solution. Using case management, the long-running process steps are replaced with states/milestones that make up an end-to-end process. These states/milestones are not statically linked. A long-running process is modeled to execute steps of a process in sequence or parallel, the state model allows you to process multiple state processes in any order based on the business rules for the process execution. The ability to create stateless CRUD processes (case actions or business services) allows users to update case states without the need to process a work item associated with a process step. 

## Long-Running Processes
Take this process below. In this process, every step needs to be executed in the order that it is modeled. If the order of the steps needs to be changed, the process definition needs to change and the process needs to be re-deployed. Re-deploying a long-running process requires the migration of existing process instances that takes effort and careful consideration. 

![build_project](images/buildproject/9.png)

## Stateless processes
In the process below we defined the major states/milestones for a support process for fault resolution. As you can see, every state is defined as a stateless process. Because the state processes are stateless, it brings flexibility in that the user can update the state through a stateless process, and based on the business rules, the process will be processed to the next appropriate state. Another benefit is that a stateless process is much easier to upgrade in place as there is no need to migrate data that may be associated with a long-running process. Stateless processes fetch data in the central repository at the current state to present to the user. Case actions are also called CRUD processes as they allow the user to modify data associated with a case. 

Stateless processes aren't always the appropriate way to progress a process from state to state. Sometimes, long-running processes are required to keep track of SLA. Using the Case Management Framework (CMF) we created a methodology to dynamically manage stateful processes associated with specific states. This methodology is dynamic and allows solutions to be extremely agile. 

![build_project](images/buildproject/10.png)

## Central Case Date
At the center of this implementation methodology lies the case data repository. A part of this repository also contains the ability to store and upload documents. The BPME engine is a built-in lightweight document store that allows the system to upload and store documents of many types, like PDFs, word, excel, etc. This repository should not be used for large amounts of documents. Organizations that have this requirement often already have large ECM solutions that could be integrated into the CMF.

Collaboration is a big part of servicing customers in BPM/Case Management solutions. Collaboration can be done by creating a special case type that records all comments, questions, and other collaboration around Case Management Solutions. In AMX BPM 4.3, this functionality was built in, but in BPME 5.0 this functionality needs to be custom build for the time being. 

Email is just another way of collaborating, but mostly used for resources like customers that does not have access to the system. BPME 5.0 can send email through a service task in the process, but cannot receive email messages. Responses to email message can be done in different ways. BW can be used to scan a central mailbox and link incoming messages to process instances responsible for sending out mail messages. Signal functionality is used to accomplish this. 

Custom help functionality can ge provided by employing TIBCO Nimbus. Process documentation can be the trigger for business process implementations. Once these processes are mapped, they could be the ideal business view of process implementations and used for process execution help with minimal changes.


![build_project](images/buildproject/31.png)

## Integration Layer
BPM Solutions should not replace current systems of record. Data should always stay in a central location and BPM should only use the data to present to users where required. If changes are made, they should be done directly from the business process at the time of the change. BPM should always only store reference data to allow for finding the data required to complete activities. Business works are the ideal product to accomplish this. As part of the CMF methodology, this capability will be explained.

![build_project](images/buildproject/30.png)

## Events 
In the case management framework, Events are used to trigger the correct dynamic sub-processes based on the current state of the case. A case data signal event is used to listen to any data changes in a specific case. When the process detects changes, the solution implements a mechanism to find the current state, then search for a new state based on an action that triggered the change. This implementation consists of 2 case data tables. the first is the location of processes that are associated with specific states and the second is the order of state execution. We will discuss this in more detail later.  


![build_project](images/buildproject/34.png)

Event triggers can be initiated by Case Actions, Business Services, or long-running processes. The process snippet below shows the section of the process that is responsible for the change of a state and triggering the new case state process.

![build_project](images/buildproject/36.png)

Events can also come from external triggers like BusinessWorks. A good example could be a customer canceling a request for service through an email message. BW can read the email, and correlate the message with an existing case that intern could cause the event to cancel the process/customer request. 

## Analytics
![build_project](images/buildproject/37.png)

Analytics is a really important piece of the Case management Framework. To better manage user performance Process KPI's you need to visualize the work in the system. We use TIBCO Spotfire to visualize all aspects of the solution. Spotfire is good at visualizing data from not only the BPM system but data from the entire organization that forms part of any BPM solution including all systems of record. The Spotfire dashboard is exposed inside the CMF UI so that users don't have to load a separate application to see what's going on. TIBCO BPM provides dashboards for users at different levels, like Management, Supervisor, and end-users. 
