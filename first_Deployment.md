Let's start creating the deployment artifacts. Select the three projects we have built so far.
Right-click and select Deployment->"Generate Test Artifacts"

![forms_project](images/Deployment/1.png)

Confirm the correct projects are selected and click Generate to create the project Artifacts.

![forms_project](images/Deployment/2.png)

A confirmation dialog will show the completion of the artifacts.

![forms_project](images/Deployment/3.png)

Click close and open the Bom project file structure to expose the Newly generated artifacts.

![forms_project](images/Deployment/4.png)

RASC file is the file that we will deploy to the BPM server. You can drag and drop this file on the new deployment screen or select it from the New Deployment Screen.
The order in which we deploy the artifacts is important. Review the dependencies before deployment to make sure the order you need to follow. Make sure you deploy your project from the bottom up.

![forms_project](images/Deployment/6.png)
![forms_project](images/Deployment/7.png)


Log into the TIBCO BPM Administrator and navigate to the Deployment Manager->New Deployment screen.
Make sure to start with the BOM project Artifact. Select Deploy to the ploy the BOM to the BPM Server. You should get a green box notifying you of successful deployment.

![forms_project](images/Deployment/5.png)

Do the same with the Forms and Business Services Artifacts and then confirm completion of deployment.

![forms_project](images/Deployment/8.png)

OK, we have created processes, data, forms and deployed them, let's test the process.
## Next Step: [Test Deployment](test_Deployment.md)