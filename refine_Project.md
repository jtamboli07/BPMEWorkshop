## Refining the project
Let's refine our project a little and explore some UI capabilities.

We made the following changes.
1. In the form below, we changed the visibility of the Dispute Id field to false, which means it will not be visible on the form.
2. We made the "Case State" field a text box, we made the text box Read-Only and 
3. We renames the caseState1 field for Case State, which makes it more user-friendly.
4. We changed the visibility of the Resolution field to false, as the user that captures the dispute does not need to see this field.

![refine_project](images/Refine/1.png)

Let's also make a process field change. For this, we will preset the Case State field to Registered to indicate that the case was created and is a registered case in the system.

TIBCO BPM Enterprise only uses JavaScript for all scripting. There are three places to create scripts in BPM Enterprise. 
1. Script tasks: used for initializing data or do some data manipulation for subsequent activities in the process. 
2. Process-level: It is possible to create process-level scripts for events on activities. 
Initial, 
Complete, 
Timeout,
Canceling . 
These scripts provide the ability to evaluate data, set data, and even more complex activities.
3. Work Manager Level Scripts: On "User Tasks," it is possible to create Work Manager Level Scripts. Task scripts get evaluated when users open the task from the inbox.  The following event scripts are available. 
Schedule, 
Reschedule, 
Open, 
Close, and
Submit. 

In the tutorial process, we want to set the case state before the first task. If you're going to set the value of a case data field before it is displayed, you will need to initialize the data field. If you want to set a case data field after processing a user task, you don't need to do that as the user form does the initialization for you. 

We will do this on the Process Manager Initiate Script to illustrate creating an object.

Select the Enter Data to Create Case user task. Make sure the "Process Manager" script is displayed. Click the Initiate Script Tab and change the Script Defined as: to JavaScript. Enter the following two lines

TIBCO BusinessStudio provides code auto-complete. You may be familiar with this if you are used to the Eclipse framework. By clicking "ctrl-space," you should see the autocomplete section open up. In this case, you can see the following predefined variables. 

Data: this is for accessing and data that you as the developer created. 
Factory: this is for accessing the creators/initializers of the data that you created. 
Pkg: this is for accessing the enumeration values for setting enum field values. 

```
//Create the object
data.Dispute = factory.com_example_mydisputecase.createDispute();

//Set the value of the state attribute in the Dispute ojject.
data.Dispute.caseState1 = pkg.com_example_mydisputecase.states.REGISTERED;
```

You have to use the package variable to set an enumeration. You cannot use plain text.

![refine_project](images/Refine/2.png)

Re-deploy and test your application. Your capture form should now look like this. You will see that 
Dispute Id Field is gone, 
the "Case State" is renamed, 
Case State has been re-defined as a read-only text field  
finally, the Resolution field is hidden.

![refine_project](images/Refine/3.png)

Next Step: We will define "Users" in the Organizational Model to allow work to be "Offered" to the Dispute Advisor Position for completion.

## Next Step: [Create Org Model](create_Organisation_Project.md)