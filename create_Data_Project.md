# Build a data Project

For the Dispute BPM Project, We will start by creating a Business data project. Business Data projects are used to store business data models that will be referenced by process projects further in the workshop.

Open the Business Studio and select a workspace then

1) Select New > Business Data Project

<img src="/images/businessData/1.jpg" alt="Create Business Data Project" width=700/>

2) Name the Project "MyDisputeCase" and Click "Finish"

<img src="/images/businessData/2.jpg" alt="Create Business Data Project" width=400/>

3) From right pane Palette > Under Case Data > Case > Click & drag Case Data object

<img src="/images/businessData/3.jpg" alt="Create Business Data Project" width=850/>

and Click and rename the Case1 as Dispute.

4) click on Dispute and select "Add Case Identifier"

<img src="/images/businessData/4.jpg" alt="Create Business Data Project" width=400/>

5) Rename the added case Identifier to "disputeref"

<img src="/images/businessData/5.jpg" alt="Create Business Data Project" width=700/>

6) Click the "Dispute" Case Data and select "Add Attribute" option and name it as "customer name"
<img src="/images/businessData/6.jpg" alt="Create Business Data Project" width=400/>

7) Similarily add 3 more attributes of name and type
   ***dob (Date), disputetype(text), cardtype(text)***

  <img src="/images/businessData/7.jpg" alt="Create Business Data Project" width=400/>

8) From the palette > Under elements > select and drag Enumeration to canvas in the middle > rename it to disputetype

<img src="/images/businessData/8.jpg" alt="Create Business Data Project" width=400/>

9) Add below enumeration values :  ***overcharge, wronglycharged***. Click on disputetype and change Type by selecting newly created enumeration group as shown below :

<img src="/images/businessData/9.jpg" alt="Create Business Data Project" width=700/>

10) Click on dispute and select "Add Identifier"

<img src="/images/businessData/10.jpg" alt="Create Business Data Project" width=400/>

11) From Palette > Create Enumerations "states" and put 4 values
a)***registered*** b)***advise*** c)***investigate*** d)***resolved***
<img src="/images/businessData/11.jpg" alt="Create Business Data Project" width=700/>

12) link the enumeration object to the earlier created Identifier "states" :
<img src="/images/businessData/12.jpg" alt="Create Business Data Project" width=700/>

13) Also mark the attribute "resolved" under Terminal States.
<img src="/images/businessData/13.jpg" alt="Create Business Data Project" width=700/>

14) Here is the final project view:  
<img src="/images/businessData/14.jpg" alt="Create Business Data Project" width=700/>

###Congratulations you have successfully created a Business Data Project 

In the next section, we will create an Organisation project to be
Next step: [Creating an Organisation Project ](2.apiimplementation.md)
