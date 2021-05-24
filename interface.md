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

You should see a screen like this.n We will be adding a new parameter for Dispute Id. You could add many more fields, but what we will do is to pass the Id for the case from where we can find all the other data we may want to use. That way the interface template is nice and clean and it will be easier to change what every sub process needs as the real data is in the case. 

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

## 3. Calling process to have a RunTime Id field: 
The name/location where the sub-process can be found. e.g. /MyDispute_BusinessService/Process Packages/MyDisputeBusinessServices.xpdl

