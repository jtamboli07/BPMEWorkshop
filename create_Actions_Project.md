# Create Actions flows

A case actions are stateless processes a user can perform on a case data object. You can specify case action availability based on the state and privilege of the user trying to access the case action. We will create a case action and restrict the availability of case actions based on the current case state. This is an optional capability as case actions will be available to all case states if no specific configuration is made. It allows you to define case actions for every state in the process to allow people to interact with the case when required. In the same way, it is possible to restrict case actions to resources with specific privileges. Let's see how this is done. We will create an updated case action for the Dispute case type. Then we will select the state for which this action is valid.

1) In the MyDispute_Actions project -> Rightclick "Processes" -> New -> Case Action
<img src="/images/actions/1.jpg" alt="create actions" width=700/>

2) In the Dialog -> Change the Label to "Advise" ->  Select "Update Case Action Process" -> Open Case Class -> Select  Dispute from the list and hit "OK"

<img src="/images/actions/2.jpg" alt="create actions" width=700/>

3) Also under Properties -> General > Select "Specific States" and select "registered". This will limit the availability of the case action to the Registered case state.

<img src="/images/actions/3.jpg" alt="create actions" width=700/>

Save the project. You can review and examine the activities that were created for you, but there is no need to change anything in this process as it will run with no changes required. What you could do if you want is to change the form to an embedded form and create a separate embedded form as we did for the capture of the case in the MyDispute_BusinessServices. I'll leave it up to you to explore.

4) Let's deploy the process like we did before and test to see how it works. After you deployed the case action, open the case manager (http://localhost/apps/case-manager/#/cases) and click on the Dispute case.  

<img src="/images/actions/4.png" alt="create actions" width=700/>

You should see all the cases you created when you first tested the Business Service. You will notice one thing. On the right-hand side, you only see Dispute Id and caseState1. If you were an Advisor, this would be very difficult to identify a specific case when a customer calls in. We can change this by adding Summary fields to this view. 

<img src="/images/actions/5.png" alt="create actions" width=700/>

Open your case data model and click on the Dispute Case. You can add fields (one by one) to this list and redeploy the data model. NOTE: This change is seen as a non-breaking change. The documentation has a section that explains breaking/distractive changes. if you make a change like changing a name or deleting an attribute the model will not deploy or it will break your data model. You can comfortably add enumerations, attributes, or summary fields without any adverse errors. 

Go ahead and redeploy your bom project and test the case manager again. You should see a screen that looks like this.

<img src="/images/actions/6.png" alt="create actions" width=700/>

Click on the case and review the case details screen. 
1. At the top of the screen you will see the timeline of the selected case. The current state is marked by a checkmark. This is where you will see the progress of the case as it moves through the milestones/states of the case. These are the enumerations you defined in the data model.
2. Below the lifecycle you will see a read-only view of the case details. This is the data you captured during the case started. Data can be changed only through case actions. Those are the Advise and Investigate buttons on my screenshot below. You should have just one at the moment.
3. The case actions allow the user to interact with the data. The user can modify data by selecting a case action button. The edit screen can be created to allow the user to change data and also case state. If the user changes the current state the milestone at the top will change after the case action is completed.


