# Forms Project (_forms)
## Embed-able forms
Forms project allows you to create one central place for embed-able forms (reusable forms). It makes it very easy to create user interfaces that are consistent throughout your project. It is a recommended best practice to create an embed-able form for every case or global class in your project and reuse it where needed. This way, you can format a task form once and then reuse it. Formatting forms takes time and, having to repeat them can lead to longer than expected implementation times.

## Pageflows
Pageflows can be reused just like embed-able forms. Again this speeds up development. Putting page flows into the forms project keeps all your UI-related processes and artifacts in a single project and, it allows for speeding up development. Pageflows are short-lived processes that can implement CRUD operations. Pageflows that can be linked to process tasks, business services, or case actions. 

## Building our first form
Please create a new BPM Process Project and call it "MyDispute_Forms." Doing this makes a new BPM process project that we will be using for forms and page flows. See below.

![forms_project](images/forms/.5.png)

Expand the project and add a dispute folder under forms, it should look like this below.

![forms_project](images/forms/1.png)

Right-click the Dispute folder and select New->Form.

![forms_project](images/forms/2.png)

Enter the name "Dispute" and select Embeddable under form type. Click Finish.

![forms_project](images/forms/3.png)

Your form should now look like this.

![forms_project](images/forms/4.png)

Expand your business object model and drag the Dispute Case class onto the form. 

![forms_project](images/forms/5.png)

You will see you now have the outer frames called dispute. The one is not necessary for what we need to do. Drag the inner Dispute frame to the white space above the outer Dispute frame. Your form should now look like this below.

![forms_project](images/forms/6.png)

Right-Click on the empty dispute frame and delete it. You can now preview the form to see what it will look like when deployed.

![forms_project](images/forms/8.png)

The form in the preview should look like this.

![forms_project](images/forms/7.png)

We will use this embed-able form in the subsequent user tasks. Embed-able forms ensure a more consistent solution with less effort to maintain.

## Next Steps: Let's create a process to capture the dispute. We will be using the bom as well as the form we just created in this process.
## [Building the business services project](business_Services_Project.md)


<!--//Lets start building the services business object model (_bom)
//## Next Step: [Building the services business object model project](services_Bom_Project.md)-->