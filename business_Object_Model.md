# Business Object Models (_bom)
This section will explain general information about the business object model. When you have an understanding of the basics, we will build our first business object model.

## Global Data
Global data allows the process to interact with data in a central repository/BPM data store instead of saving the data in the process. Global data allows a process to share data across processes instead of having one local copy of the data embedded in a process. It is recommended that the system of record should be the main repository for case data. Case data table should only store the meta-data allowing the process to find the relevant data in the system of record.

## Case States/Case Lifecycle
Case States allows the BPM engine to define and manage the life cycle of every case in the system. A good example is a mortgage application case with all the milestones that a mortgage goes through in its life cycle, e.g. Application, Review, Approved, etc.

## Lookup Tables
The case data repository has multiple uses. 
Storing BPM process-related data is just one capability. 
Lookup Tables are case data tables that stores process execution business rules.  In the Tibco Case Management methodology, case data tables store the links to processes associated with case status. 
## Find Cases/Case Reference
The engine provides multiple ways to find case data.
Find by case identifier: Auto-generated Case Id 
Find all: cases of a specific type
Find by Specific criteria: Search on specific DQL Query
Find by Simple Search: Search on case data searchable fields to find 

## Linking Case Objects
Based on the case data model, you may want to associate case objects. Association allows users to navigate related data objects (customer to product etc.). The BPMN palette activity, "Add Links to Other Case Objects", is used to associate case object to each other.

## Parameters/Data Fields 
Parameters and data fields are similar to parameters and local variables in most programming languages. Parameters can be passed in and out of a process where data fields are local to data fields. Parameters can be simple types like text, number, etc. but also reference a bom object like a customer, service, etc.

## Data Best Practices
Pass case id to sub-processes instead of case objects. Case date can change between the time a sub-process is triggered to when a user views the data. Using a case id ensures users see real-time data. A pageflow responsible for presenting the data to the user is responsible for fetching the latest version of the data.
It also means that when working with data, you need to fetch the data using the case search functionality. For this reason, it is also a good idea to create reusable service processes to do searching as it will speed up development time. We will be implementing this best practice in this workshop.

OK, so let's start building our first business object model.
## Next Step: [Building your first business object model (_bom)](create_Data_Project.md)


<!--
Let's start building the forms
## Next Step: [Building the project forms (_forms)](forms_project.md)
```
```
Let's start building the organizational model
## Next Step: [Building the organizational model](org_Model.md)
```-->