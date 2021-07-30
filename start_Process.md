# Starting a process after Case creation. 
A long-running process provides the ability to manage user activities and ensure work is done timely by the predefined user/offer set. Long-running processes are persisted in the BPM engine database to keep track of progress as the work gets completed. In triggering a long-running process, you create a process instance that will run until the completion of the activities that make up the process.  As a best practice, long-running rather be smaller processes. Each process should be responsible for managing one phase in the life of the end-to-end process.  When it comes to Case Management, define multiple milestones that complete specific activities to solve a problem. We then string these activities together to complete the life of the Case. A milestone represents a Case states that we defined in the business object model. In our scenario, we have Registered, Advice, Investigate, and Resolved as the Case states. Each of these states may or may not have multiple activities to complete for the process or move the case state from one to the next. We will create a process for each of these states. 

We will create a process responsible for processing the "Registered" state of the process. The Case represents the meta-data of the Case, for example, the customer or Dispute. The organization's system of record should be the primary location for case data. The BPM process should collect the data required to perform to work as the user needs the data. In our case, we assume the BPM case is the actual data. When we created the business service, we initiated the Case but did not trigger a long-running process to handle the genuine Dispute. 

Another best practice is not to pass big chunks of data from one process or activity to the next. We know the data is in the database, and we know the unique ID of that Case. We can easily find the case data if we have the id number. When a global Case data object "create case" is triggered, the response of the activity is a case reference. When using the OOTB IDs,  the ID of the Case is only assigned when the Case gets created. So the data that we pass in does not have the ID.  To get the ID, we need to use the reference number to get a new copy of the data and then read the ID number of the Case. We would have used the case reference, but we did not, as the reference field contains a version number built-in. Every time a case changes, the version number of the reference field gets updated.  The Best to access a Case reference is by searching the Case by Id.

<img src="/images/process/1.png" alt="get case id" width=700/>

In the screenshot above, you will see the script that we execute when the create case service task completes. The first line is responsible for reading the case data from the reference field. When populating data in the Dispute data field, you can extract the newly created ID that we are doing in the second line. We will use this field to pass into the new long-running business process we will make next.

Click menu File-> New -> BPM Process Project. 

<img src="/images/process/2.png" alt="get case id" width=700/>

Enter the name, review the id and click finish to create the project in BPM business studio. 

<img src="/images/process/3.png" alt="get case id" width=700/>

Your project should look like this.

<img src="/images/process/4.png" alt="get case id" width=700/>

Next, you can rename the MyDispute_Process-Process to "Registered."

<img src="/images/process/5.png" alt="get case id" width=700/>

You should have a process that looks like this.

<img src="/images/process/6.png" alt="get case id" width=700/>

First, let's create the input parameter that will receive the case ID we are passing in from the business service. We will make this ID parameter input only and required. 

<img src="/images/process/7.png" alt="get case id" width=700/>
<img src="/images/process/8.png" alt="get case id" width=700/>

The parameter type should be the same as the case id in the BOM.

Also, let's create 2 data fields. FYI, not parameters, as these fields will only be local to this process. One for the Dispute case data field and one for the Dispute case data reference.  

<img src="/images/process/12.png" alt="get case id" width=700/>
<img src="/images/process/13.png" alt="get case id" width=700/>


Next, in the process, click on the triangle in the top right of the process editor. You will see the BPMN palette pop open. Click on the tasks and select the script task icon. Drag it to the process on top of the line. You will see that if you position the mouse cursor on top of the line, the script task should be linked into the line automatically. If not, click on the line and drag the black square on the arrow side to the left of the newly created script task. Drawing lines takes a little practice at first.

<img src="/images/process/9.png" alt="get case id" width=700/>

<img src="/images/process/10.png" alt="get case id" width=700/>

Rename the script task to Init Data. Change the "Script Defined as" to JavaScript.

<img src="/images/process/11.png" alt="get case id" width=700/>

We will now populate the Dispute Reference field and the Dispute case data field. We will use the reference field to link the Case to the user task we will be creating next. 


Add the following lines to your "Init Data - JavaScript." 

```
//Find Dispute Reference for provided Dispute Id
data.DisputeRef = bpm.caseData.findByCaseIdentifier(data.DisputeID,'com.example.mydisputecase.Dispute');

//Read the data from the case reference
data.Dispute = bpm.caseData.read(data.DisputeRef);
```

<img src="/images/process/14.png" alt="get case id" width=700/>

Let's examine this script. 
1. "data.disputeID" is the parameter passed down to the process instance from the business service.
2. "com.example.mydisputecase.Dispute" is the case class. The case class is constructed from the BOM class name and the Dispute case name
- in line one, we use a Case object bpm.caseData to find the case reference (pointer to the data) for the case id.
3. when we have the case reference, in 3, we read the data from the database with the bpm command bpm.caseData.read.

As soon as the data is extracted and stored in a local case data field, the data becomes stale. The reason data gets stale is because the data can be changed by any process in the system, like user request or update, external event, service task, etc. The best practice, to only load and use the data when required, for instance, when a user opens a form. We can call the same script in a pageflow to execute when a user opens a work item from a worklist. The user will then see new data. When the user is complete, we can update the Case after the pageflow. We will talk about this more later.

Next, let's add a user task to the process. Drag the user task from the BPMN palette and drop it on the line as we did with the script task.

<img src="/images/process/15.png" alt="get case id" width=700/>

Call the user task "Review Dispute." You will notice that there is a red x on the top right of the user task. The red x indicates an incomplete activity. It probably means a participant is required. 

<img src="/images/process/16.png" alt="get case id" width=700/>

You will also notice that the default form is selected. Default forms display all the data exposed to the user task to present to the user. We will change this. Let's get the error on the user task fixed. To fix the error, we need to assign a participant to the user task. Open your Org Project and expose the Dispute Team under MyDisputeOrg. Drag the Dispute Advisor and drop it on top of the Review Dispute User Task. 

<img src="/images/process/18.png" alt="get case id" width=700/>

This action will create a participant in the Process project with the same name as the position in the Org model. 

<img src="/images/process/19.png" alt="get case id" width=700/>

You will notice that the red x error marker on the user task disappears. When you deploy this process and the Org Model project as we did before to the engine. Remember to deploy the org model project first, as the process project has the org model as a dependant project.  

<img src="/images/process/20.png" alt="get case id" width=700/>

Before we can test, we need to make sure the Business Service triggers the process. Open the business service and drag and drop the sub-process task from the BPMN palette and drop it on the line in the process after creating the case data.

<img src="/images/process/24.png" alt="get case id" width=700/>

Click the plus on the task and select the "Registered" process as the target sub-process to start.

<img src="/images/process/25.png" alt="get case id" width=700/>

Now click the Map To Sub-Process and map the Dispute Is from the local data to the Dispute ID in the sub-process.

<img src="/images/process/26.png" alt="get case id" width=700/>

You will see an error on the sub-process with a message. Click the Configure task for the "..." link. and the error should go away. 

<img src="/images/process/27.png" alt="get case id" width=700/>


Re-deploy the Business Service. 


When starting a case, the system creates a work item for the Dispute Adviser group. Before you can test, you will also need to add a user to the position. If you have not done so, you will have to create an LDAP container. The documentation will help you do that. Open the Organization Browser and select Manage LDAP Container.

<img src="/images/process/21.png" alt="get case id" width=700/>

We will use the System Administrator for this exercise. At the top right of the screen, select Browse Organization. Now expand the Organizations till you see the three positions you created in your Org Model project. Select the Dispute Advisor Position and select the checkbox next to the "tibco-admin" user.

<img src="/images/process/22.png" alt="get case id" width=700/>

Click Map selected resource. 

<img src="/images/process/23.png" alt="get case id" width=700/>

Back in the Work Manager, Capture a new Dispute business service. 

<img src="/images/process/28.png" alt="get case id" width=700/>

Complete the form and click submit to create the Case and start a process instance.
Click the Work View button at the top of the screen to display the list of work items created. You can click the item on the list to preview the work item or click the open button to open and process the work item.

<img src="/images/process/30.png" alt="get case id" width=700/>
<img src="/images/process/29.png" alt="get case id" width=700/>

Open the work item to reveal the default form created by the system. You should see a screen like this below.

<img src="/images/process/31.png" alt="get case id" width=700/>

Two copies of the same data are displayed. You may wonder why that is. Let's look at the work item we created in BusinessStudio.

<img src="/images/process/32.png" alt="get case id" width=700/>

By default, the engine adds all the process data to a  new user task created in a process. The data in this Case exposed is a Dispute Id, Dispute Data Field, and a Dispute Reference field. A form interprets a reference field as a data field just like a regular case data field, and that is why the two sets of the same data are displayed.

So far, we have 
1. Create a data model to save our case data. 
2. We created a business service to capture the data.
3. Created a case Action to modify the data.
4. Created an Organizational model to allow users to perform work in the system.
5. Created a long-running business process to do work based on a specific profile. 
6. We called the long-running business process a sub-process step in the business service.

These are all fundamental components of any business process. The following action will call the same sub-process, not directly, but via a process interface.  Dynamic processes are an essential capability when it comes to dynamic process execution. 

## Next Steps: [Creating a process interface](interface.md)
