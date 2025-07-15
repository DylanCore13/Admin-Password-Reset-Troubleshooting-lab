#  Admin Password Reset & Troubleshooting Lab

![image](https://github.com/user-attachments/assets/c691465c-c4a1-47c7-bcfb-c2d9f495968d)    ![image](https://github.com/user-attachments/assets/4de7fca3-1d1f-437f-8081-a5c422d0ca67)

<h2>Objective</h2>

- This project simulates a critical help desk scenario: a user or administrator has forgotten or lost the password for a local account on an Azure Virtual Machine, preventing them from logging in. You will demonstrate how to use Azure's built-in "Reset password" functionality to regain access to the VM.


<h2>Azure Services Used:</h2>

- Azure Virtual Machine (VM): Your existing Windows VM.
- Azure VM Access Extension: The tool Azure uses to perform the password reset.
- Azure Resource Groups: For organization.



<h2>Part 1: Prepare Your Azure VM</h2>

<h3>Start and Connect to your Azure VM (if not already running):</h3>

- Go to the Azure Portal (portal.azure.com).
- Search for "Virtual machines" and find your ResetVM (or whatever you named your Windows VM).
- If its status is "Deallocated," click on the VM name, then click the "Start" button at the top. Wait for it to start ("Running").
- Connect via RDP using your AzureAdmin credentials.

  ![image](https://github.com/user-attachments/assets/d8144754-7bb6-48d0-8b81-2d54c0e43ca7)


<h3>Create a New Local Admin Account (the one you'll "forget"):</h3>

- Inside your VM (via RDP):
  - Right-click on the Start button and select "Computer Management".
  - Navigate to Local Users and Groups > Users.
  - Right-click in the empty space and select "New User...".

![image](https://github.com/user-attachments/assets/4d2286af-d613-41c2-9604-8cad3aeb1058)


  - User name: ForgottenAdmin (or something descriptive)
  - Password: TestPassword123! (Set a simple password for now, and write it down for a moment).
  - Uncheck: "User must change password at next logon".
  - Check: "Password never expires".
  - Click "Create", then "Close".
  - Add to Administrators Group:
    - Double-click on ForgottenAdmin (or right-click > "Properties").
    - Go to the "Member Of" tab.
   
      ![image](https://github.com/user-attachments/assets/203da9ba-4b47-4355-8e3e-7201955de4f3)

    - Click "Add...".
    - Type Administrators and click "Check Names". It should resolve to your local Administrators group. Click "OK", then "OK" again.
- Log in as ForgottenAdmin once to confirm it works. Log out of AzureAdmin and try logging in as ForgottenAdmin with TestPassword123!. (This confirms the account is set up correctly before you break it). Log out after testing.

<h3>"Forget" the Password (Simulate the Problem):</h3>

- Log back into VM as AzureAdmin.
- In Computer Management > Local Users and Groups > Users.
- Right-click on ForgottenAdmin > "Set Password..."
- Click "Proceed".
- Enter a new, random, incorrect password that you will NOT remember or write down. (e.g., just smash your keyboard a few times).
- Click "OK".
- Log out of AzureAdmin.

  ![image](https://github.com/user-attachments/assets/49f5a3cd-797d-43d7-9bdf-19b5bd47acae)


<h3>Attempt to Login (Demonstrate Failure):</h3>

- Try to log in as ForgottenAdmin with the original password (TestPassword123!).
- Expected Result: It will fail with an "Incorrect password" or "The user name or password is incorrect" message.
- CRITICAL STEP: Take a screenshot of this failed login attempt. This is your "problem" screenshot.

  ![image](https://github.com/user-attachments/assets/92528a02-62f9-4ec4-9f43-2b5a4a096001)


  

<h2>Part 2: Use Azure's Password Reset Feature (Corrected Navigation)</h2>


- You should be on your host machine, using your web browser to access the Azure Portal.

<h3>Navigate to your VM in the Azure Portal:</h3>

  - In the Azure Portal search bar at the top, type "Virtual machines" and select it.
  - Click on your VM (or the name of your Windows VM).
  - Access the "Reset password" feature:

- In the left-hand menu of your VM's blade, scroll down.
- You should see a section titled "Support + troubleshooting".
- Under "Support + troubleshooting", click on "Reset password".

![image](https://github.com/user-attachments/assets/8d276030-5af3-422f-9d72-5fc38223301b)

<h3>Configure the Password Reset:</h3>

- On the "Reset password" blade that appears:
  - Username: Type ForgottenAdmin (the local user account whose password you want to reset on the VM).
  - New password: Enter a new, strong password that you will remember and use to log in later (e.g., NewPassword123!@#).
  - Confirm new password: Re-enter the exact same new password.
- Take a screenshot of this "Reset password" blade with the username and new password entered, before you click "Update". This is a good "before" screenshot for your documentation.

![image](https://github.com/user-attachments/assets/87162dec-e6a5-4c2b-a41f-46a5fb9e8cf7)


<h3>Initiate the Update:</h3>

- Click the blue "Update" button at the bottom of the blade.

<h3>Monitor the Operation:</h3>

- You will see notifications pop up in the top-right corner of the Azure Portal (click the bell icon to view them).
- It will say "Deploying" or "Updating" and specifically mention the "VMAccessExtension". This is the Azure tool that performs the password reset on the VM.
- This operation can take a few minutes to complete. Please be patient.
- Take a screenshot of the notification showing the successful completion of the "VMAccessExtension" deployment or the password reset operation. This serves as your "during/after" screenshot in the Azure Portal.





<h2>Part 3: Verify the Password Reset</h2>


<h3>Initiate a NEW RDP Connection from the Azure Portal:</h3>


- Log in with the NEW Password for ForgottenAdmin:

  ![image](https://github.com/user-attachments/assets/098b6f19-4d77-4daa-82fc-2615c0ad2cec)


- When the Windows Security prompt asks for your credentials:
  - User name: Type ForgottenAdmin
  - Password: Enter the NEW strong password you set in the Azure Portal just moments ago (e.g., NewPassword123!@#).
- Click "OK" or "Connect".
- Confirm Successful Login

  ![image](https://github.com/user-attachments/assets/5f7dc680-7660-462b-a23c-5310493ede6b)


Expected Result: You should now successfully log in to the VM and see the desktop for the ForgottenAdmin user!

