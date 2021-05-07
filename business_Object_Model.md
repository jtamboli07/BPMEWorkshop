# Business Object Models (_bom)
This section will explain general information about the business object model. When you have an understanding of the basics, we will build our first business object model.

## Global Data
Global data allows the process to interact with data in a central repository/BPM data store instead of saving the data in the process. This will allow users to share data across processes instead of having one local copy of the data locked into a process while executing a process. While the BPM Engine is able to store data in a case in the BPM repository, it is recommended that the system of record should be the main repository for a case data, and the case data table only store the index values that will allow the process to find the data in the systems of record.

## Case States/Case Lifecycle
Case States allows the BPM engine to define and manage a life cycle of every case in the system. A good example is a mortgage application case with all the milestones that a mortgage goes through in its life cycle, e.g. Application, Review, Approved, etc...

## Lookup Tables
Data Data can be used for more than just storing BPM process related data. Lookup Tables are Case Data tables that are used to store process execution business rules. E.g. in the Case Management methodology, we use case data tables to store the locations of the relevant case state processes so that we can dynamically execute the process when a specific state is reached and also the order in which processes states should be executed.

## Find Cases/Case Reference
In order to find a case in the BPM Case management systems, it is required to do a search for a specific case. This can be done in different ways.
Find by case identifier : Unique Case Id created when the case was created
Find all : cases of a certain type
Find by a Specific criteria : Search on specific DQL Query
Find by Simple Search : Search on case data searchable fields to find 

## Linking Case Objects
Creating a case data model, you often need to link case classes to define a relationship. This can be done by defining an association in the data model. E.g. a customer needs to be linked to a product or a service. This can be done using a Case Data Operation Activity in the BPMN palette, selecting Add Links to Other Case Objects.

## Parameters/Data Fields 
Parameters and data fields are similar to parameters and local variables in most programming languages. A parameter can be passed into a process where data fields are local to data fields. Parameters can be simple types like text, number etc, but also reference a bob object like a customer, service etc.

## Data Best Practices
Using case data as the single source of truth for data, it makes sense to only pass unique case identifiers between processes instead of passing entire case objects between processes. This ensures that data is always in synch when working with data. It also means that when working with data, you need to fetch the data using case search functionality. For this reason it is also a good idea to create reusable service processes to do searching as it will speed up development time. We will be implementing this best practice in this workshop.

OK, so lets start building our first business object model.
## Next Step: [Building your first business object model (_bom)](create_Data_Project.md)


```
Lets tart building the forms
## Next Step: [Building the project forms (_forms)](forms_project.md)
```
```
Lets start building the organizational model
## Next Step: [Building the organizational model](org_Model.md)
```