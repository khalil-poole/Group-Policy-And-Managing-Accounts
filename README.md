# Group-Policy-And-Managing-Accounts

In this section of Active Directory, we are going to create a policy regarding password resets, enabling, and disabling accounts. 

1. To get started we're going to login to the domain controller VM with the admin credentials that we used last time.

1. Open the Group Policy Management Console (GPMC)
Log in to a machine with Group Policy Management Console installed (typically, a Domain Controller).
Click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.
2. Create or Edit a Group Policy Object (GPO)
In the GPMC, navigate to the Group Policy Objects section. This can be found by expanding the left pane as shown below

<img width="951" height="656" alt="image" src="https://github.com/user-attachments/assets/7fa33eb2-d1d2-4bfc-8717-a54960bb788a" />


Right-click Default Domain Policy and select Edit to modify the exisiting GPO
Give the new GPO a descriptive name if you're creating a new one, like "Account Lockout Policy".


3. Navigate to the Account Lockout Policy Settings
In the Group Policy Management Editor, expand the following:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
4. Configure Account Lockout Policy Settings
You will see three primary settings that you need to configure:
Account Lockout Duration:
Definition: The time in minutes that an account remains locked before it is automatically unlocked.
Configuration: Double-click on this setting, select Define this policy setting, and then set the duration (e.g., 30 minutes).
Account Lockout Threshold:
Definition: The number of failed logon attempts that will trigger an account lockout.
Configuration: Double-click on this setting, select Define this policy setting, and then set the threshold (e.g., 3 invalid attempts).
Reset Account Lockout Counter After:
Definition: The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts.
Configuration: Double-click on this setting, select Define this policy setting, and then set the time (e.g., 15 minutes).
5. Link the GPO to an Organizational Unit (OU)
Once the GPO is configured, you need to link it to the appropriate Organizational Unit (OU) or domain where you want the policy to apply.
In the GPMC, right-click the OU or domain where you want to apply the GPO and select Link an Existing GPO.
Choose the GPO you created or modified earlier and click OK.
6. Update Group Policy
You can wait for the Group Policy to propagate automatically, or you can force an update immediately.
On a client machine or server, open Command Prompt and type gpupdate /force, then press Enter.
7. Verify the Policy
To verify the policy, you can use the rsop.msc (Resultant Set of Policy) tool on a client machine to see the applied settings.
Alternatively, you can also check the settings using the Group Policy Management Console.
Important Considerations
Account Lockout Threshold: Setting this too low (e.g., 1 or 2 attempts) can lead to unnecessary lockouts.
Account Lockout Duration: Setting this too high can be inconvenient for users but increases security.
Reset Account Lockout Counter After: Setting this too short could allow attackers to repeatedly attempt to log in without triggering a lockout.


2. Go to the Start Menu, the go to "Windows Administrative Tools", then scroll down and click on "Active Directory Users and Computers". Expand "mydomain.com" and then click "_EMPLOYEES" and you should see a bunch of users.


   <img width="942" height="656" alt="image" src="https://github.com/user-attachments/assets/810a573c-e10f-40c4-a2c8-ae6dc651a347" />


  
4. Pick a random user account we created previously with the Powershell script. As a reminder, that the password for all the generated users created is "Password1" with no quotations.

5. Remote desktop the client vm and attempt to log in using "mydomain.com\firstname.lastname" with it 10 times with a bad password.


After 10 attempts, go back to the domain controller and observe the user that you used.
