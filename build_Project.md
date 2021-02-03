# Build a Project Components Explained

Instructions to build a project through Business Studio. Test Change

# Build Components step by step
Open TIBCO Business Studio and select a new empty folder for your project. This is an example of a workspace location, C:\demo\Healthcare\BST01. 

![build_project](images/buildproject/1.png)

Always create a new workspace for a new project. Artifacts can be shared but it is still recommended to import an artifacts into the new project if you want to reuse it. If you are planning to change anything in the shared artifact, you will need to change the name of the artifact or it will clash with an existing deployed project. 

## Project Artifact Types
These are the project artifacts we will be using to build the solution in this workshop. The section in the brackets are the naming convention that is used to make the project recognizable. e.g. dispute_bom. You will notice that we always use camel casing for variable as well as project artifact names. 

In this section we will highlight some terminology that you may already know but it is important in this workshop.


### Business Object Models (_bom)
#### Global Data
Global data allows the process to interact with data in a central repository/BPM data store instead of saving the data in the process. This will allow users to share data across processes instead of having one local copy of the data locked into a process while executing a process. While the BPM Engine is able to store data in a case in the BPM repository, it is recommended that the system of record should be the main repository for a case data, and the case data table only store the index values that will allow the process to find the data in the systems of record.

#### Case States/Case Lifecycle
Case States allows the BPM engine to define and manage a life cycle of every case in the system. A good example is a mortgage application case with all the milestones that a mortgage goes through in its life cycle, e.g. Application, Review, Approved, etc...

#### Lookup Tables
Data Data can be used for more than just storing BPM process related data. Lookup Tables are Case Data tables that are used to store process execution business rules. E.g. in the Case Management methodology, we use case data tables to store the locations of the relevant case state processes so that we can dynamically execute the process when a specific state is reached and also the order in which processes states should be executed.

#### Find Cases/Case Reference
In order to find a case in the BPM Case management systems, it is required to do a search for a specific case. This can be done in different ways.
Find by case identifier : Unique Case Id created when the case was created
Find all : cases of a certain type
Find by a Specific criteria : Search on specific DQL Query
Find by Simple Search : Search on case data searchable fields to find 

#### Linking Case Objects
Creating a case data model, you often need to link case classes to define a relationship. This can be done by defining an association in the data model. E.g. a customer needs to be linked to a product or a service. This can be done using a Case Data Operation Activity in the BPMN palette, selecting Add Links to Other Case Objects.

#### Parameters/Data Fields 
Parameters and data fields are similar to parameters and local variables in most programming languages. A parameter can be passed into a process where data fields are local to data fields. Parameters can be simple types like text, number etc, but also reference a bob object like a customer, service etc.

#### Data Best Practices
Using case data as the single source of truth for data, it makes sense to only pass unique case identifiers between processes instead of passing entire case objects between processes. This ensures that data is always in synch when working with data. It also means that when working with data, you need to fetch the data using case search functionality. For this reason it is also a good idea to create reusable service processes to do searching as it will speed up development time. We will be implementing this best practice in this workshop.


### Organizational Models (_org)
When creating a BPM project you will require a organizational model for offering and allocating tasks to people in the organization. It is recommended that a new organizational model is used for every project you implement. The reason for this is that it makes it easier to life cycle the artifact with the project it was intended for. This makes trouble shooting easier when problems are occur.

### Interface Project (_interface)
Process Interfaces allows for late binding of sub-processes and therefore the sub-processes are not statically linked into the main process at design time. 
The interface provides a template for the sub-process input and output parameters. It is a best practice to create a separate project for interface files. There is no special project for interfaces so a BPM Process project is used for this purpose. 

 ![build_project](images/buildproject/2.png)

### Forms Project (_forms)
Forms project allow you to create one central place for embed-able forms (forms that are reusable). It makes it very easy to create user interfaces that are consistent throughout your project if you create embed-able forms that is reused in your project. It is a good idea to create a embed-ab;le form for every case or global class in your project and reuse it where needed. This way you can format the form the way you need and then just reuse. Formatting forms some times takes time and having to do this over and over can lead to longer than expected implementation times.

#### Pageflows
Pageflows can re reused just like embed-able forms. Again this speeds up development. Putting pageflows into the forms project keeps all your UI related processes and artifacts in a single project and it allows for speeding up development. Pageflows are often used for CRUD functionality that can be called from process tasks, business services as well as case actions. 

### Main Process (_process)
The main process will be responsible for orchestrating all the lifecycle processes. Below is a good example of this process. It probably looks very complicated as you cannot really follow a process but its is really simple and we will review and use it in this workshop.

 ![build_project](images/buildproject/3.png)

 #### 3 Sections of thew main process
 ##### Main Process Flow
 The main process flow is responsible to keep the lifecycle process for the case alive. The start event complete script is responsible for initializing process data. The case data field is one of these data elements initialized. Through this data field, all changes in state is monitored and the relevant sub-process triggered.
 
 The case data is retrieved from the bpm engine  through a find case script function. The case state is passed to the find state location sub-process. This sub-process is a process in the service process explained little later in this page.  The Find State Location sub process sets a runtime_id field that is used by the ad-hoc sub process. This location tells the main process, which sub-process to use for the initial state sub-process. 

 Once the initial state is determined, the Init Data script task sets the data and tells the ad-hoc sub-process that it needs to trigger the first sub-process. Some debugging in this init data script is very useful to make sure everything is going according to plan.


 The section that initializes data in this script looks like this.

    data.cCaseId = data.serviceId;
    data.ServiceRef = bpm.caseData.findByCaseIdentifier(data.serviceId,'com.xxx_bom.Service');
    data.Service = bpm.caseData.read(data.ServiceRef);
    data.StateChanged = true;

Logging data looks like this.

    Log.write("********** Debug initial data **********");
    Log.write("Runtime Id 	: " + data.runtimeId);
    Log.write("Order State 	: " + data.Service.state);
    Log.write("Order Id 	: " + data.serviceId);
    Log.write("cOrder Id 	: " + data.cCaseId);
    Log.write("StateChanged : " + data.StateChanged);

In order to see the logged data, you need to look at the tibco/bpm/runtime:5.0.0 container logs.

When the data is initialized, the main process flow is processed to a catch event that simply waits for the process to be cancelled. 

 ##### Catch Cancel Event
 The catch cancel event simply waits for an event to be triggered from somewhere in bpm or from a BW/REST service task. A good example for this is if a support ticker process is in progress and the customer figured out what the problem is and he wants to cancel the support ticket. This event will terminate the main process flow and end the lifecycle of the process. In your implementation you can decide to leave the data in the case tables or to archive it. This is beyond the scope of this workshop.

 ##### Case Data Change Event
This section is what drives the changes of the process states/lifecycle events. The catch case data change event listens to all updates to the case data reference field in the process. A case reference has a version associated with it. Once the version changes, the catch case data change is fired. 




### Signal Project (_signal)
### Case Actions (_actions)
### Business Services (_businessServices)
### Services Projects (_services)
### Services Business Object Model (_servicesBom)
### Rest Services Project (_rest)
### Process State Projects (_"stateName")
### State Lookup components
#### State case data bom
#### State service processes



