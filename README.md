#UI-Policy-and-UI-Policy-Actions

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
