# Business Services (_businessServices)

Business Services fulfills multiple purposes.
trigger new long-running processes, 
create cases, 
do basic CRUD operations on BPM case data or other systems of record data.
In this lab, we will create a Business Service in a separate project to capture a new dispute.

Select File->New->BPM process Project like you did when we created the Forms Project. Enter the name of the project and note the "Id" is auto-generated. You will see the default project id start with "com.example". It is possible to modify the default project id in the Studio Preferences. It would make sense to be something like com.<customer name>.<solution name>_businesservices. Changing the project id is optional but a best practice. The id identifies the project when deployed to the BPM server.

![forms_project](images/bServices/1.png)

Your project structure now looks like this.

![forms_project](images/bServices/2.png)

You will see that a process MyDisputeBusiunessServices is automatically created. We could change the name to CaptureDispute.
We can go ahead and delete this process for now, but just in case you want to re-use this process to build a business service from scratch, follow the following steps.

![forms_project](images/bServices/3.png)

A Business Service is a particular type of pageflow. To change the process (the yellow process) to a business service, we need to change the type to "pageflow process" then indicate the pageflow to expose as a business service. Right-click the process and select Convert to Pageflow Process.

![forms_project](images/bServices/4.png)

Now, select the properties of the process, then select "Publish as a Business Service" checkbox. Also, change the Business Category to MyDispute.

![forms_project](images/bServices/5.png)

Let us create a Business Service from a template. Business Studio provides templates to make the building of processes much easier and quicker. Right-click on Processes and select Business Services.

![forms_project](images/bServices/6.png)

Now complete the New Process Wizard to look like this. Add a label and select "Create Case Data Business Service Process." We will configure the Business Service to have a form to handle the data capture, a service task to create the case, and also handle any errors that may occur.
Remember to change the Business service label and rename the Business Category to MyDispute.

![forms_project](images/bServices/7.png)

You will notice the created process has some errors. We need to fix that to make sure the process will run. The errors are because the data fields are not defined correctly. We need to select the BOM types for the case data field and reference fields.  

![forms_project](images/bServices/8.png)

I prefer to have my case data fields be more descriptive. Let's change the name and select the bom case class for the caseBomType Field. Call the field Dispute and select the correct case type.

![forms_project](images/bServices/9.png)

Rename the caseRefType data field and call it Dispute Ref. The errors on the 2 data fields should disappear after you save your project. There is still an error on the Create Case Data Service Task. 

![forms_project](images/bServices/10.png)

The reason is that the service task also needs to be configured to update the correct BOM case. Click on the "..." ellipses and select the Dispute class. After this, your error should not disappear and, the process should function correctly.

![forms_project](images/bServices/11.png)

Select the Enter Data To Create Case user form in the process. You will see the "Use Default Form" radio button is selected. Change it to "Form..". You may see a message pop-up, click on OK to proceed and, create a new form that will override the default form. 

![forms_project](images/bServices/12.png)

We want to customize the default form. Now click on "Open" to display the form. You should see a form looking like this.

![forms_project](images/bServices/13.png)

We want to use the embedded form we created earlier. Delete the current form and replace it with the embedded form. 

![forms_project](images/bServices/14.png)
![forms_project](images/bServices/15.png)

In the forms control palette, select the embedded form control and drop the selected control on the empty frame. Select the Dispute form in the Select form to embed dialog.

![forms_project](images/bServices/16.png)

Click Yes on the pop-up dialog. 

![forms_project](images/bServices/17.png)

Next, we need to create a parameter mapping to send the parameter data from the form to the embedded form. Make sure to map the value of the parameter.

![forms_project](images/bServices/18.png)

If you preview your form, it should now look like this. We will make some other minor changes a little later. This process should not be ready to deploy.

## Next Step: Deploy and test the BOM, Business Services, and Forms projects.
## [First Deployment](first_Deployment.md)