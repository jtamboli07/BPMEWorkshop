# Process Interfaces

Dynamic Sub-processes require process interfaces based on some process data instead of hard coding the sub-process into a sub-process activity. Interfaces allow us to cater for rules like triggering a sub-process based on priority, location, credit score, and many more.  To call a process via a process interface, you require a couple of things.

## 1. A process interface definition 
Process interface definitions are a template that tells the calling process to pass in specific data to the sub-process, like the Id of the Dispute in our case. You can do this in the process project, but it is best practice to do this in a separate project to keep it in a central location easy to find.

To do this, you create a regular BPM Process Project and simply deleting the process added by default. See the steps below.

<img src="/images/Interface/1.png" alt="get case id" width=700/>
<img src="/images/Interface/2.png" alt="get case id" width=700/>
<img src="/images/Interface/3.png" alt="get case id" width=700/>

Now add a new process interface.

<img src="/images/Interface/4.png" alt="get case id" width=700/>
<img src="/images/Interface/5.png" alt="get case id" width=700/>

You should see a screen like this. We will be adding a new parameter for Dispute Id. You could add more fields, but we will pass the Id for the case from where we can find all the other data we may want to use. That way, the interface template is nice and clean, and it will be easier to change what every sub-process needs as the actual data is in the case. 

<img src="/images/Interface/6.png" alt="get case id" width=700/>

Add a parameter and call it Dispute Id.

<img src="/images/Interface/7.png" alt="get case id" width=700/>
<img src="/images/Interface/8.png" alt="get case id" width=700/>

Your project should now look like this. That's all you need to do to create an interface project.

<img src="/images/Interface/9.png" alt="get case id" width=700/>


## 2. A process exposed via a process interface: 
A process requires configuration to allow dynamic execution. The general tab of process properties provides this configuration.

In your Registered project, click the three ellipses to select the interface we just created.

<img src="/images/Interface/10.png" alt="get case id" width=700/>
<img src="/images/Interface/11.png" alt="get case id" width=700/>

Your process will now look like this. 

<img src="/images/Interface/12.png" alt="get case id" width=700/>

You will now delete the yellow starter and join the grey starter with the Init data script task. 

<img src="/images/Interface/13.png" alt="get case id" width=700/>

Your process is ready to be called.

## 3. Calling process to have a RunTime Id field: 

Calling a process with an interface requires the name/location.  An example of the location of a process is this /MyDispute_BusinessService/Process Packages/MyDisputeBusinessServices.xpdl. A Runtime Identifier data field stores the location. The runtime identifier data field will tell the engine where the sub-process is. 

You will now see your Business Service has an error marker on the sub-process for starting the process. 
The error marker indicates the sub-process has changed, and the standard parameter is not available anymore. You will have to re-select the sub-process interface instead of the actual process.

<img src="/images/Interface/17.png" alt="get case id" width=700/>

Now create a new Text field called Runtime Id.

<img src="/images/Interface/15.png" alt="get case id" width=700/>

Make sure the field is 150 characters long. Process locations is a long path to the actual process location like "/MyDispute_BusinessService/Process Packages/MyDisputeBusinessServices.xpdl"

Now select the newly created Runtime Id in the sub-process properties page.


<img src="/images/Interface/19.png" alt="get case id" width=700/>
<img src="/images/Interface/20.png" alt="get case id" width=700/>

Your Properties page should look like this.

<img src="/images/Interface/21.png" alt="get case id" width=700/>

You will also have to map the Dispute Id in the Map To Sub-Process Tab.

<img src="/images/Interface/22.png" alt="get case id" width=700/>

The last item we need to do is to specify the location of the sub-process. 
Select the MyDispute_process.xpdl file and see the resource properties below. The path is the value that you will need. Tiy can right-click and copy the line in the studio properties section. 

<img src="/images/Interface/23.png" alt="get case id" width=700/>

Next, we need to create an Init Script for the Sub-process to set the runtime id. See below

```
data.RuntimeId = "/MyDispute_Process/Process Packages/MyDispute_Process.xpdl";
```

<img src="/images/Interface/24.png" alt="get case id" width=700/>


Your process should be ready to be deployed and tested. Take a stab at it and make sure it works as it is supposed to.
You have to deploy the BusinessService, Interface, and Process projects. And remember to deploy the interface first. The other two projects have the interface project as a dependency.

It should do what it did before and deliver a work item to the Review Dispute task to the Dispute Advisor.

The benefit of this is 
1. The called process is not hardcoded into the calling process sub-process step. 
2. The sub-process can be determined at runtime, which gives you, the developer, a lot of flexibility. The entire Case Management Process implementation depends on this dynamic nature of the process execution.

