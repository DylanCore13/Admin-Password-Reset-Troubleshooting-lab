# Admin-PW-Reset

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

<h3>Create a New Local Admin Account (the one you'll "forget"):</h3>

- Inside your VM (via RDP):
  - Right-click on the Start button and select "Computer Management".
  - Navigate to Local Users and Groups > Users.
  - Right-click in the empty space and select "New User...".
  - User name: ForgottenAdmin (or something descriptive)
  - Password: TestPassword123! (Set a simple password for now, and write it down for a moment).
  - Uncheck: "User must change password at next logon".
  - Check: "Password never expires".
  - Click "Create", then "Close".
  - Add to Administrators Group:
    - Double-click on ForgottenAdmin (or right-click > "Properties").
    - Go to the "Member Of" tab.
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

<h3>Attempt to Login (Demonstrate Failure):</h3>

- Try to log in as ForgottenAdmin with the original password (TestPassword123!).
- Expected Result: It will fail with an "Incorrect password" or "The user name or password is incorrect" message.
- CRITICAL STEP: Take a screenshot of this failed login attempt. This is your "problem" screenshot.
