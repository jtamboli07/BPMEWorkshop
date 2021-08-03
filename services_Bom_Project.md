# Services Business Object Model (_servicesBom)

The purpose of the services bom project is to create the lookup tables that determine the process execution of the main process lifecycle/state processes.

![build_project](images/buildproject/6.png)

The services bom project contains two case tables. State Locations determine the location of the dynamic sub-process that is responsible for processing a state. Interfaces expose the processes. In the case management framework, we use one parameter to trigger state processes. The parameter points to the id of the main case. 

![build_project](images/buildproject/7.png)

Let's start building the services process project (_servicesProcess)
## Next Step: [Building the services process project](services_Process_Project.md)