# Business Services (_businessServices)

Business Services are used to initiate new long running processes, start cases and also to do basic CRUD operations, whether on BPM case data or other system of record.
In this lab we will create a Business Service in a separate project to capture a new dispute.

Select File->New->BPM process Project like you did when we created the Forms Project. Enter the name of the project and note the Id that is automatically generated. You will see the defualt name start with com.example. This can be changed in the Studio Preferences if you want. It would make sense to be something like com.<customer name>.<solution name>_businesservices. This is completely optional, but it will be very handy as this is what you will see when the project is deployed to the BPM server.

![forms_project](images/bServices/1.png)

Your project structure now looks like this.

![forms_project](images/bServices/2.png)

