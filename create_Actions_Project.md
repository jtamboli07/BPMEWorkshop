# Create Actions flows

Case actions are stateless processes that implement actions a user can perform on a case data object. You can specify case action availability based on the state and privilege of the user trying to access the case action. We will create a case action and restrict the availability of case actions based on the current case state. Restricting access is an optional capability as case actions will be available to all case states by default. It allows you to define case actions for every Case state to enable users to interact with the Case when required.
In the same way, it is possible to restrict case actions to resources with specific privileges. Let's look at how to do this. We will create an updated case action for the Dispute case type. Then we will select the state for which this action is valid.

1) In the MyDispute_Actions project -> Right-click "Processes" -> New -> Case Action
<img src="/images/actions/1.jpg" alt="create actions" width=700/>

2) In the Dialog -> Change the Label to "Advise" ->  Select "Update Case Action Process" -> Open Case Class -> Select  Dispute from the list and hit "OK"

<img src="/images/actions/2.jpg" alt="create actions" width=700/>

3) Also under Properties -> General > Select "Specific States" and select "registered". Selecting "REGISTERED," limits the availability of the case action to the Registered case state.

<img src="/images/actions/3.jpg" alt="create actions" width=700/>

Save the project. You can review and examine the activities we created for you, but there is no need to change anything in this process as it will run with no changes required. What you could do if you want is to change the form to an embedded form and create a separate embedded form as we did to capture the Case in the MyDispute_BusinessServices. I'll leave it up to you to explore.

4) Let's deploy the process like we did before and test to see how it works. After you deployed the case action, open the case manager (http://localhost/apps/case-manager/#/cases) and click on the Dispute case.  

<img src="/images/actions/4.png" alt="create actions" width=700/>

You should see all the cases you created when you first tested the Business Service. You will notice one thing. On the right-hand side, you only see Dispute Id and caseState1. If you were an Advisor, this would be very difficult to identify a specific case when a customer calls in. We can change this by adding Summary fields to this view. 

<img src="/images/actions/5.png" alt="create actions" width=700/>

Open your case data model and click on the Dispute Case. You can add fields (one by one) to this list and redeploy the data model. NOTE: This change is a non-breaking change. The documentation has a section that explains breaking/distractive changes. If you change a name or delete an attribute, the model will not deploy, or it will break your data model. You can comfortably add enumerations, attributes, or summary fields without any adverse errors. 

Go ahead and redeploy your bom project and test the case manager again. You should see a screen that looks like this.

<img src="/images/actions/6.png" alt="create actions" width=700/>

Click on the Case and review the case details screen. 
1. At the top of the screen, you will see the timeline of the selected Case. The checkmark indicates the current state of the Case. The lifecycle at the top of the screen is where you will see the progress of the Case. These are the enumerations you defined in the data model.
2. Below the lifecycle, you will see a read-only view of the case details captured at the initiation. Case Actions provides the ability to change data. The Advise and Investigate buttons are examples of doing it. You should have just one at the moment.
3. The Case Actions allow the user to interact with the data. The user can modify data by selecting a case action button. If the user changes the current state, the milestone at the top will change after the completion of the case action.
4. On the right-hand side of the screen, you have four sections.
Work Items: User activities associated with a case. You need to have the case reference field on the work item interface to link the work item to the Case. More about this later. 
Linked Cases: If your data model consists of case objects with associations, you will be able to see all related case objects in this section. You need to trigger a Global Case Link service task to accomplish this.
Documents: TIBCO BPM can attach documents to the Case. This section lists the attached documents. You will have to trigger a Link Document service task to create a linked document.
Audit: Every action taken on a case data element gets audited. The Audit Trail is where you will see updates on the Case, including the date, time, user, and action the user took.

<img src="/images/actions/7.png" alt="create actions" width=700/>

We will go through these in more detail as the workshop progresses.

Next Step: Creating a long running process.
## Next Step: [Start Process](start_Process.md)