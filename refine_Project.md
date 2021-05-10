## Refining the project
Lets refine our project a little and explore some UI capabilities.

We made the following changes.
1. In this screen we changed the visibility of the Id field to false, which means it will not be visible when the form is displayed to the user.
2. We made the Case State field a text box, we made the text box Read-Only and 
3. We renames the caseState1 field for Case State, which makes it more user friendly.

![forms_project](images/Refine/1.png)

Lets also make a process field change. For this we will preset the Case State field to Registered to indicate that the case was created and it is a registered case in the system.

TIBCO BPM Enterprise only use JavaScript for all scripting. There are 3 places to create scripts in BPM Enterprise. 
1. Script task in the process: this is used if you want to initialize data or do some data manipulation for subsequent tasks in the process. 
2. On every task in a process you can create Process level scripts for events like initial, Complete, Timeout and cancel script. These are evaluated when the process executes. 
3. On user tasks you can also create Work Manager Level Scripts. There are evaluated when a user task executes. Scripts for the following events are available. Schedule, Reschedule, Open, Close and Submit. 

In order to set the Case State to we can it anywhere but in our case we want to set it before the user task is displayed to the user. If you want to set the value of a case data field before it was displayed to a user, you will need to initialize the data field. If you want to set a case data field after its been processed through a user task, you don't need to do that as the user form does the initialization for you. 

We will do this on the Process Manager Initiate Script to illustrate creating an object.

Select the Enter Data to Create Case user task. Make sure the Process Manager Script is expanded. Click the Initiate Script Tab and change the Script Defined as: to JavaScript. Enter the following 2 lines

```
//Create the object
data.Dispute = factory.com_example_mydisputecase.createDispute();

//Set the value of the state attribute in the Dispute ojject.
data.Dispute.caseState1 = pkg.com_example_mydisputecase.states.REGISTERED;
```




![forms_project](images/Refine/2.png)