# 3 Sections of the main process
## Main Process Flow
 The main process flow is responsible for keeping the lifecycle process for the case alive. The start event complete script is responsible for initializing process data. The case data field is one of these data elements initialized. Through this data field, all changes in the state are monitored, and the relevant sub-process triggered.
 
The case data is retrieved from the bpm engine through a find case script function. The case state is passed into the find state location sub-process as a parameter. This sub-process is a process in the service process explained a little later on this page.  The Find State Location subprocess sets a runtime_id field that is used by the ad-hoc sub-process. This location tells the main process, which sub-process to use for the initial state sub-process. 

 Once the initial state is determined, the Init Data script task sets the data and tells the ad-hoc sub-process that it needs to trigger the first sub-process. Some debugging in this init data script is very useful to ensure everything is going according to plan.


 The section that initializes data in this script looks like this.

    data.cCaseId = data.serviceId;
    data.ServiceRef = bpm.caseData.findByCaseIdentifier(data.serviceId,'com.xxx_bom.Service');
    data.Service = bpm.caseData.read(data.ServiceRef);
    data.StateChanged = true;

Logging data looks like this.

    Log.write("********** Debug initial data **********");
    Log.write("Runtime Id   : " + data.runtimeId);
    Log.write("Order State  : " + data.Service.state);
    Log.write("Order Id     : " + data.serviceId);
    Log.write("cOrder Id    : " + data.cCaseId);
    Log.write("StateChanged : " + data.StateChanged);

Container logs contain the process log data. It is possible to use docker logs to view the logs. The logs are in the container  "tibco/bpm/runtime:5.0.0".

After data initialization, the main process flow is processed to a catch event that waits for the process to be canceled. 

## Catch Cancel Event
 The catch cancel event waits for an event to be triggered. The trigger can come from a process or an API. An excellent example of this is if a support ticket process is in progress and the customer figured out what the problem is, he wants to cancel the support ticket. This event will terminate the main process flow and end the lifecycle of the process. In your implementation, you can leave the data in the case tables or archive it. This is beyond the scope of this workshop.

## Case Data Change Event
This section is what drives the changes of the process states/lifecycle events/processes. The catch case data change event listens to all updates to the case data reference field in the process. A case reference has a version associated with it. Once the version changes, the catch case data change is fired. 

The first script task in this section reads the data from the new case reference field. This will then indicate if the case state has changed. 

    data.Service = bpm.caseData.read(data.ServiceRef);

If the new data state is different from the existing state, it means the state has changed. The arrow in the image below shows a conditional line evaluating the state change data field. 
    
    data.Service.state != data.CurrentState;

![build_project](images/buildproject/4.png)

Only if the state has changed will the "Find State Location" task be executed. The "Find State Location" task takes the state name as input and returns the location of the new state sub-process in the runtime id field.  

The state Change Script sets the data field "stateChanged" to true, ensuring the new state sub-process is triggered. This is configured in the ad-hoc sub-process configuration tab in the Describe Execution Trigger Script field. See below.

![build_project](images/buildproject/5.png)