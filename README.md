# UI-Policy-and-UI-Policy-Actions

Task: <br>
Employees return all types of assets (monitors, ID cards, laptops, etc.), but only laptops require a unique serial number that must be verified for security and warranty purposes. We need to add a new field specifically for laptops, and to ensure it only appears and becomes required when Asset Type = Laptop. <br>
- Step 1: Add a New Field to the Table via Form Builder
- Step 2: Create a UI Policy to match the requirement
- Step 3: Add a UI Policy Action
- Step 4: Test Your Work
------------------------------------------------------------------------------------------------------------
1.Add a Custom Field to the Form<br>
Navigation: <br>
All > DXC Technologies > Device Inventory <br>
The Laptop Asset Type requires specific **fields**. To add a custom field to the form: <br>
- Click on one of the records to see the **Form Builder** option.  <br>
- Right click on the header, then choose **Configure > Form Builder** <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Click%20on%20one%20of%20the%20records%20to%20show%20Form%20Builder%20option.png?raw=true)
- To create a new field, click **'+ Add a field in the table'**.
- Set the **Column label*** (a name for the field). The **Column name*** will automatically populate. Leave the **Type*** as a "String". <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Name%20the%20field%20we%20have%20created.png?raw=true)
- The newly created field will appear on the left. Drag it onto the form layout to officially add it, and **Save**. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/New%20field%20added.png?raw=true) <br>
2.Create a UI Policy <br>
 Navigation: <br>
All > System Definition > UI Policies <br>
**OR** go to the **Asset Recovery** table, right-click on a column, and select **UI Policies**.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policies.png?raw=true)
 - Click **New** to create a new UI Policy <br>
 - Associate the UI Policy with the Asset Recovery table <br>
 - There is no name but Short description is required <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Short%20Description%20for%20UI%20Policy.png?raw=true)
3. Define the UI Policy Condition
- Create a condition so that the UI only appears and becomes required when the **Asset Type** is **Laptop**. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20appears%20when%20Asset%20Type%20is%20laptop.png?raw=true)
- After saving, **UI Policy Actions** tab appears.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policy%20Actions%20tab.png?raw=true)
- Click **New** to define the action should occur when the condition is met. <br>
- When the **Asset Type** is **Laptop**, we want to interact with the previously created field: **Laptop Serial Number** <br>
  - Set **Laptop Serial Number** to be **Mandatory** and **Visible**
    ![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/New%20Record%20of%20New%20UI%20Policy%20Action.png?raw=true)
4. Test the UI Policy <br>
- Go to **Asset Recovery Request** table and create a New record
- When we select **Laptop** as the Asset Type, the **Laptop Serial Number** field becomes **Visible** and **Mandatory**.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Create%20New%20record%20to%20Test%20the%20Asset%20Type.png?raw=true)
- If you change the**Asset Type**  to something that doesn't match the condition (e.g., **Monitor**), the **Laptop Serial Number** field disappears.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/When%20Condition%20is%20Not%20Met.png?raw=true)

Bonus, Replace the Asset tag with **Laptop Serial Number** when Laptop is selected
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
