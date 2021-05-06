# Create Actions flows

A case action flows will determine what actions or steps a user can perform related to a case. We will also restrict the availability of case actions based on the current case state. This is not a requirement and purely optional. It allows you to define case actions for every state in the process to allow people to interact with the case when required. In the same way it is possible to restrict case actions to resources with specific privileges. Lets see how this is done. We will create an update case action for the Dispute case type. Then we will select the state for which this action is valid.

1) Find MyDisputeActions project > Rightclick "Processes" > New > Case Action
<img src="/images/actions/1.jpg" alt="create actions" width=700/>

2) In the Dialog > Change the Label to "Advise" >  Select "Update Case Action Process" > Open Case Class > Select  Dispute from the list and hit "OK"

<img src="/images/actions/2.jpg" alt="create actions" width=700/>

3) Also under Properties > General > Select "Specific States" and select "registered"

<img src="/images/actions/3.jpg" alt="create actions" width=700/>

Save the project. This 

4)

<img src="/images/actions/4.jpg" alt="create actions" width=700/>
