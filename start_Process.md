# Starting a process when the case is created. 
A long-running process provides the ability to manage user activities and making sure work is done in a timely fashion by the predefined user/offer set. Long-running processes are persisted in the BPM engine database to keep track of progress as the work gets completed. In triggering a long-running process, you create a process instance that will run until the completion of the activities that make up the process.  As a best practice, long-running processes should be broken up into multiple smaller sub-processes that are responsible for a specific part of the process. When it comes to case management we break the life of the case up into multiple milestones that complete specific activities to solve a problem. We then string these activities together to complete the life of the case end-to-end. Every one of these milestones is represented by a case states that we defined in the business object model. In our scenario, we have Registered, Advise, Investigate, and Resolved as the case states. Each of these states may or may not have multiple activities to be performed to complete the process or move the case state from one to the next. We will create a process for each of these states. 

For the first process, we will create a process that will be responsible for processing the "Registered" state of the process. The case represents the meta-data of the case for example the customer or dispute. The actual data should be located in the organization's systems of record and the BPM process should collect the data that is required to perform to work as the user needs the data. In our case, we assume the BPM case is the real data. When we created the business service we created the case but did not trigger a long-running process to handle the actual dispute. 

Another best practice is not to pass huge chunks of data from one process or activity to the next. We know the data is in the database and we know what the unique ID of that case is. We can easily find the data if we just have the id number. When a global case data object "create case" is triggered, the response of the activity is a case reference. When using the OOTB IDs,  the ID of the case is only assigned when the case gets created. So the data that we pass in does not have the ID.  To get the ID, we need to use the reference number to get a new copy of the data and then read the ID number of the case. We would have used the case reference, but we did not as the reference field contains a version number built-in. Every time a case changes, the version number of the reference field gets updated.  So, the best way of keeping a reference to the case is by the ID number that does not change.

<img src="/images/process/1.png" alt="get case id" width=700/>

In this screenshot you will see the script that we execute when the create case service task is completed. The first line is responsible for reading the case data from the reference field. When the data is populated in the Dispute data field, you can extract the newly created ID that we are doing in the second line. We will use this field to pass into the new long running business process we will create next.

Click menu File-> New -> BPM Process Project. 

<img src="/images/process/2.png" alt="get case id" width=700/>

Enter the name, review the id and click finish to create the project in studio. 

<img src="/images/process/3.png" alt="get case id" width=700/>

Your project should look like this.

<img src="/images/process/4.png" alt="get case id" width=700/>

Next you can rename the MyDispute_Process-Process to Registered

<img src="/images/process/5.png" alt="get case id" width=700/>

You should have a process that looks like this.

<img src="/images/process/6.png" alt="get case id" width=700/>

First lets create the input parameter that will receive the case ID we are passing in from the business service. We will make this ID parameter input only and required. 

<img src="/images/process/7.png" alt="get case id" width=700/>
<img src="/images/process/8.png" alt="get case id" width=700/>

The parameter type should be the same as the case id in the BOM.

Also lets create 2 data fields. FYI, not parameters as these field will only be local to this process. One for the Dispute case data field and one for the Dispute case data reference.  

<img src="/images/process/12.png" alt="get case id" width=700/>
<img src="/images/process/13.png" alt="get case id" width=700/>


Next, in the process, click on the triangle in the top right of the process editor. You will see the BPMN palette pop open. Click on the tasks and select the script task icon and drag it to the process on top of the line. You will see that if you position the mouse cursor on top of the line, the script task should be linked into the line automatically. If not, simply click on the line and drag the black square on the arrow side to the left of the newly created script task. This sometimes takes practice.

<img src="/images/process/9.png" alt="get case id" width=700/>

<img src="/images/process/10.png" alt="get case id" width=700/>

Rename the script task to Init Data. Change the Script Defined as  to JavaScript.

<img src="/images/process/11.png" alt="get case id" width=700/>

We will now populate the Dispute Reference field and the Dispute case data field. We will ise the reference field to link the case to the user task we will be creating next. 


Add the following lines to your "Init Data - JavaScript" 

```
//Find Dispute Reference for provided Dispute Id
data.DisputeRef = bpm.caseData.findByCaseIdentifier(data.DisputeID,'com.example.mydisputecase.Dispute');

//Read the data from the case reference
data.Dispute = bpm.caseData.read(data.DisputeRef);
```