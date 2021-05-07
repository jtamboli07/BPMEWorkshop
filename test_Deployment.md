## Testing your solution
Open the BPM Work Manager - http://localhost/apps/work-manager/#/overview, and navigate to the Business Services Section.
Expand the My Dispute Category and select start Capture Dispute.

![forms_project](images/Testing/1.png)

You will notice a couple of things on this form. 
1. The Dispute Id is blank.
- The reason for this is that the case id is only created when the case is created. This field could really be hidden at the time of capture. 
2. The Case State label is in a non business user friendly format and this field should in any case be auto completed and read only. 
3. The Resolution is displayed on this form and they should not be shown to the customer at the time of capturing the dispute. This field should also be hidden on the form.

We will fix these issues a little later. 

![forms_project](images/Testing/2.png)