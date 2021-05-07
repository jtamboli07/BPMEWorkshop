# Business Services (_businessServices)

Business Services are used to initiate new long running processes, start cases and also to do basic CRUD operations, whether on BPM case data or other system of record.
In this lab we will create a Business Service in a separate project to capture a new dispute.

Select File->New->BPM process Project like you did when we created the Forms Project. Enter the name of the project and note the Id that is automatically generated. You will see the defualt name start with com.example. This can be changed in the Studio Preferences if you want. It would make sense to be something like com.<customer name>.<solution name>_businesservices. This is completely optional, but it will be very handy as this is what you will see when the project is deployed to the BPM server.

![forms_project](images/bServices/1.png)

Your project structure now looks like this.

![forms_project](images/bServices/2.png)

You will see that a process MyDisputeBusiunessServices is automatically created. We can go ahead and change the name to CaptureDispute.

![forms_project](images/bServices/3.png)

A Business Service is a special type of pageflow. In order to change the process (the yellow process) to a business service, we need to change the type to pageflow process and then mark the pageflow to be exposed as a business service. Right-click the process and select Convert to Pageflow Process.

![forms_project](images/bServices/4.png)

Now, select the properties of the process send select Publish as a Business Service checkbox. Also change the Business Category to MyDispute.

![forms_project](images/bServices/5.png)
