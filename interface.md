# Process Interfaces

Process Interfaces are used to execute a sub-process dynamically based on some process data instead of hard coding the sub-process into a sub-process activity. This allows us to cater for rules like triggering a sub-process based on priority, location, credit score and many more.  In order to call a process via a process interface you require a couple of things.

## 1. A process interface definition 
This is a template that tells the calling process to pass in certain data to the sub-process, like the Id of the Dispute in our case. You can do this in the process project, but it is best practice to do this in a separate project to keep it in a central location easy to find.

To do this you create a normal BPM Process Project and simply deleting the process that is normally added by default. See steps below.

<img src="/images/Interface/1.png" alt="get case id" width=700/>
<img src="/images/Interface/2.png" alt="get case id" width=700/>
<img src="/images/Interface/3.png" alt="get case id" width=700/>

Now add a new process interface

<img src="/images/Interface/4.png" alt="get case id" width=700/>
<img src="/images/Interface/5.png" alt="get case id" width=700/>

You should see a screen like this. We will be adding a new parameter for Dispute Id. You could add many more fields, but what we will do is to pass the Id for the case from where we can find all the other data we may want to use. That way the interface template is nice and clean and it will be easier to change what every sub process needs as the real data is in the case. 

<img src="/images/Interface/6.png" alt="get case id" width=700/>

Add a parameter and call it Dispute Id.

<img src="/images/Interface/7.png" alt="get case id" width=700/>
<img src="/images/Interface/8.png" alt="get case id" width=700/>

Your project should now look like this. That's really all you need to do to create an interface project.

<img src="/images/Interface/9.png" alt="get case id" width=700/>


## 2. A process configured to be called via a process interface: 
A process needs to be configured to be called dynamically. This is done in the general tab of a process properties

In your Registered project, click the 3 ellipses to select the interface we just created.

<img src="/images/Interface/10.png" alt="get case id" width=700/>
<img src="/images/Interface/11.png" alt="get case id" width=700/>

Your process will now look like this. 

<img src="/images/Interface/12.png" alt="get case id" width=700/>

You will now delete the yellow starter and join the grey starter with the Init data script task. 

<img src="/images/Interface/13.png" alt="get case id" width=700/>

Your process is ready to be called.

## 3. Calling process to have a RunTime Id field: 

Calling a process with an interface requires the name/location where the sub-process can be found. e.g. /MyDispute_BusinessService/Process Packages/MyDisputeBusinessServices.xpdl. This is done in a Runtime Identifier data field. This data field will tell the engine where the sub-process is that needs to be started. This could be any number of sub-processes as long as they are associated with the same interface template that we just created. 

You will now see your Business Service has an error marker on the sub process for starting the process. 
This is because the sub-process is been changed and the normal parameter is not available any more. You will have to re-select the sub-process interface instead of the actual process.

<img src="/images/Interface/17.png" alt="get case id" width=700/>

Now create a new Text field called Runtime Id

<img src="/images/Interface/15.png" alt="get case id" width=700/>

Make sure the field is 150 characters long. Process locations is a long path to the actual process location like "/MyDispute_BusinessService/Process Packages/MyDisputeBusinessServices.xpdl"

Now select the newly created Runtime Id in the sub-process properties page.


<img src="/images/Interface/19.png" alt="get case id" width=700/>
<img src="/images/Interface/20.png" alt="get case id" width=700/>

Your Properties page should look like this.

<img src="/images/Interface/21.png" alt="get case id" width=700/>

You will also have to map the Dispute Id in the Map To Sub-Process Tab.

<img src="/images/Interface/22.png" alt="get case id" width=700/>

Your process should be ready to be deployed and tested. Take a stab at it and make sure it works as it is supposed to.

It should do exactly what it did before and deliver a work item to the Review Dispute task to the Dispute Advisor.
 