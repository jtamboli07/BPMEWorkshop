# Build a Project

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

### Organizational Models (_org)
### Interface Project (_interface)
### Forms Project (_forms)
### Main Process (_process)
### Signal Project (_signal)
### Case Actions (_actions)
### Business Services (_businessServices)
### Services Projects (_services)
### Services Business Object Model (_servicesBom)
### Rest Services Project (_rest)
### Process State Projects (_"stateName")



