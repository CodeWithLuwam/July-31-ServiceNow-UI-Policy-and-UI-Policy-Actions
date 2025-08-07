# UI-Policy-and-UI-Policy-Actions

Task: <br>
Employees return all types of assets (monitors, ID cards, laptops, etc.), but only laptops require a unique serial number that must be verified for security and warranty purposes. We need to add a new field specifically for laptops, and to ensure it only appears and becomes required when Asset Type = Laptop. <br>
- Step 1: Add a New Field to the Table via Form Builder
- Step 2: Create a UI Policy to match the requirement
- Step 3: Add a UI Policy Action
- Step 4: Test Your Work
------------------------------------------------------------------------------------------------------------
All > DXC Technologies > Device Inventory <br>
The Laptops need specific **fields** so to add a field to the form: <br>
- Click on one of the records to see the Form Builder option.  <br>
- Right click on the header. Configure > Form Builder <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Click%20on%20one%20of%20the%20records%20to%20show%20Form%20Builder%20option.png?raw=true)
- To create a new field, we will press the '+ Add a field in the table' option
- We will give the Column label * a name and Column name * will automatically populate and we will leave the data Type * as a string <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Name%20the%20field%20we%20have%20created.png?raw=true)
- Our newly created field will be on the left and we will have to drag it to the form to officially add it and save. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/New%20field%20added.png?raw=true) <br>
 - Now we can start creating our UI Policy!
 - All > System Definition > UI Policies **OR** go to the Asset Recovery table, right click on the columns and see UI Policies.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policies.png?raw=true)
 - We will select New <br>
 - We are associating the UI Policy with the Asset Recovery table <br>
 - There is no name but Short description is required <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Short%20Description%20for%20UI%20Policy.png?raw=true)
- We create a condition that the UI should only appears and become required when Asset Type is laptop. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20appears%20when%20Asset%20Type%20is%20laptop.png?raw=true)
- When we save our changes after the previous step, 'UI Policy Actions' tab shows up.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policy%20Actions%20tab.png?raw=true)


------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------
Task: <br>
Employees sometimes confuse model number with serial number, but the model number has letters, and the serial number should only be digits. To reduce errors, write a short script that checks the Laptop Serial Number field and warns the user if they enter letters.

- Use a UI Policy Script to validate Laptop Serial Number contains only digits
- Table: Asset Recovery Request
- UI Policy Conditon: Asset Type is Laptop
- Run scripts: Checked
- Run scripts in UI type: Desktop
- Script location: Script tab of your UI Policy
- Use the "Execute if true" tab to enter script <br>
<br>
