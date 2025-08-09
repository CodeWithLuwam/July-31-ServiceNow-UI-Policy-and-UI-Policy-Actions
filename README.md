# ServiceNow-Dynamic-Form-Behavior-with-UI-Policies

Task: <br>
Employees return all types of assets (monitors, ID cards, laptops, etc.), but only laptops require a unique serial number that must be verified for security and warranty purposes. We need to add a new field specifically for laptops, and to ensure it only appears and becomes required when Asset Type = Laptop. <br>
- Step 1: Add a New Field to the Table via Form Builder
- Step 2: Create a UI Policy to match the requirement
- Step 3: Add a UI Policy Action
- Step 4: Test Your Work
------------------------------------------------------------------------------------------------------------
**Step 1. Add a Custom Field to the Form**<br>
- Navigation: <br>
  All > DXC Technologies > Device Inventory <br>
- The Laptop Asset Type requires specific **fields**. To add a custom field to the form: <br>
 1. Click on one of the records to see the **Form Builder** option.  <br>
 2. Right click on the header, then choose: **Configure > Form Builder** <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Click%20on%20one%20of%20the%20records%20to%20show%20Form%20Builder%20option.png?raw=true)
 3. To create a new field, click **'+ Add a field in the table'**.
 4. Set the **Column label*** (field name). The **Column name*** will automatically populate. 
 5. Leave the **Type*** as a "String". <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Name%20the%20field%20we%20have%20created.png?raw=true)
 6. The new field will appear on the left. Drag it into the form layout to officially add it.
 7. Click **Save**. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/New%20field%20added.png?raw=true)<br>

    ---
**Step 2. Create a UI Policy** <br>
- **Navigation:** <br>
  All > System Definition > UI Policies <br>
  **OR** 
  Right-click on any column in the **Asset Recovery** table and select **UI Policies**.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policies.png?raw=true) <br>
- Click **New** to create a new UI Policy
- Associate the UI Policy with the **Asset Recovery** table
- There is no name field, but **Short Description** is required
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Short%20Description%20for%20UI%20Policy.png?raw=true)
- Define a UI Policy Condition to control when the UI field appears: *"When Asset Type is Laptop"* <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20appears%20when%20Asset%20Type%20is%20laptop.png?raw=true) <br>

    ---
**Step 3: Add a UI Policy Action**
- After saving the UI Policy, a **UI Policy Actions** tab will appear. <br>
- Click **New** to define the action should occur when the condition is met. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policy%20Actions%20tab.png?raw=true)
- When the **Asset Type** is **Laptop**, we want to interact with the previously created field: **Laptop Serial Number** <br>
  - Set **Laptop Serial Number** to be:<br>
    - **Mandatory**: True <br>
    - **Visible**: True <br>
    ![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/New%20Record%20of%20New%20UI%20Policy%20Action.png?raw=true) <br>
    ---
**Step 4: Test Your Work - Ensure Fields Respond to Asset Type Selection** <br>
- Go to the **Asset Recovery Request** table.
- Create a New Record. <br>
- When Asset Type = **Laptop**:
  - **Laptop Serial Number** becomes **Visible** and **Mandatory**.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Create%20New%20record%20to%20Test%20the%20Asset%20Type.png?raw=true)
- When **Asset Type** ≠ **Laptop** (e.g., **Monitor**): <br>
  - **Laptop Serial Number** field disappears.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/When%20Condition%20is%20Not%20Met.png?raw=true)

## Bonus: Replace Asset Tag with **Laptop Serial Number** when Laptop is selected <br>
- To create another UI policy, return to the UI Policy we already created. <br>
- Under the **UI Policy Actions** tab, click **New**.
  ![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Select%20New%20in%20the%20UI%20Policy%20Action.png?raw=true)
- Create another action: <br>
  - **Field Name**: Asset Tag
  - **Visible**: False
  ![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/UI%20Policy%20Action%20Field%20name%20Asset%20Tag%20Visible%20False.png?raw=true)
- After we select **Save**, the UI Policy for **Asset Tag** will now appear under the **UI Policy Actions** tab.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Asset%20Tag%20UI%20Action%20Appears%20in%20UI%20Policy%20Actions%20tab.png?raw=true)

---
**Test Your Work - Verify Laptop Serial Number and Asset Tag Visibility Logic** <br>
- Open an Asset Recovery Request record. <br>
- When **Asset Type** = **Laptop**: <br>
  - **Laptop Serial Number** appears <br>
  - **Asset Tag** disappears <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Asset%20Type%20Laptop%20Laptop%20Serial%20Number%20appears%20and%20Asset%20Tag%20disappears.png?raw=true)
- when  **Asset Type** = **Tablet** (or anything else):
  - **Laptop Serial Number** disappears <br>
  - **Asset Tag** disappears <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Asset%20Type%20Tablet,%20Laptop%20Serial%20Number%20disappears%20.png?raw=true)

------------------------------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------------------------
# Use UI Policy Script to Validate Laptop Serial Number Contains Only Digits

[ We're still working within the **Asset Recovery Request** table, using the same UI Policy condition: *Asset Type = Laptop*. <br>
This step adds script validation to the **Laptop Serial Number** field. ] <br> 

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

We will be creating with the same UI Policy we created: Require LaptopSerial Number <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Click%20on%20the%20Same%20UI%20Policy%20We%20Created.png?raw=true) <br>
The reason we will keep using this is because we still want the Serial Number to appear, the Asset Tags to disappear but, on top of that, we are going to add a script. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Click%20Advanced%20View%20to%20see%20the%20Script%20tab.png?raw=true) <br>
- Inside the Script tab, check the **Run scripts** box to display the **Script Editor** fields. <br>
- In our script, to pull a value from the form, we need `g_form` object and its `getValue()` method.<br>
  - inside the `getValue()` specify the field's name (not the label the client sees) in quotation marks. <br>
  1. **Get the field value**: <br>
    - Use the `g_form.getValue()` method to pull the value from the `u_laptop_serial_number` field on the form. <br>
    - Returns the value **as a string**, even if the field contains numbers.
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/g_form.getValue().png?raw=true) <br>
  2. **Check if it contains letters**: <br>
    - `/[a-zA-Z]/` is a regular expression that matches any uppercase (`A-Z`) or lowercase `(a-z`) letter.  <br>
    - `.test(serial)` checks the `serial` string against the regular expression. <br>
    - `hasLetters` will be: <br>
        - `true` if **at least one letter** is found in the serial number. <br>
        - `false` if there are **no letters** (numbers or symbols only). <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Check%20if%20hasLetters()%20Contains%20Letters.png?raw=true)
  3. **Show or hide error messages based on validation**: <br>
    - `if(hasLetters)` - If the serial number contains any letters (meaning `hasLetters` is true) <br>
    - Use `g_form.showFieldMsg()` to display an error message to the user: <br> 
        - First parameter: field name (`'u_laptop_serial_number'`) <br>
        - Second parameter: the error message text (`'Serial number must contain numbers only.'`) <br>
        - Third parameter: `'error'` - specifies the message type/style (displays as an error with red styling)
    - `else` - If the serial number does NOT contain letters (meaning `hasLetters` is `false`) <br>
    - Use `g_form.hideFieldMsg()` to remove any existing error message:
        - First parameter: field name (`'u_laptop_serial_number'`)
        - Second parameter: `true` (clears the message)
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Form%20Validation%20-%20Serial%20Number%20Numeric%20Check%202.png?raw=true) <br>
---
To test, we'll open any user in the **Asset Recovery Request** table and for **Laptop Serial Number** we'll put letters and digits and we'll try and save. <br>
- We are met with an Error message. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Laptop%20Serial%20Number%20Error%20Message.png?raw=true) <br>
- Without the letters, the error message disppears. <br>
![](https://github.com/CodeWithLuwam/ServiceNow-UI-Policy-and-UI-Policy-Actions/blob/main/Images/Error%20Message%20Disappears.png?raw=true)
