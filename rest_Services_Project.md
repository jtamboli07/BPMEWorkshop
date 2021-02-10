# Rest Services Project (_rest)

In order to execute a rest service from a process task, a REST service project needs to be created. This project defines the interface for the rest service including the rest URL, the request and response formats. Configuring a process rest activity it is required to select the operation defined in the rest project.

This screenshot below shows a configuration of a rest project.

 ![build_project](images/buildproject/11.png)

A rest service operation required request as well as response data. Below is an example of a request payload configuration.

 ![build_project](images/buildproject/13.png)

 See below the configuration of the activity that will trigger the rest project configured above. Whats left to do is to complete the mapping ot the data fields in the Input to service and Output from service tabs.

  ![build_project](images/buildproject/12.png)


## Trigger Process As a Rest Services
This is a critical part of any BPM solution. This is not done through the rest service project.  API Explorer explains the API but not the data payload. We created some sample documentation and BWCE project ware that will be supplied on request to explain the implementation of calling a process as a rest service.

## Rest from User forms
There is often a requirement to call a Rest service directly from a form, rather than a service task in a pageflow. One example is to populate an option list in a form as the user types data into a control. This is also not done through the rest service project. The same documentation mentioned above explains and illustrates this implementation.
