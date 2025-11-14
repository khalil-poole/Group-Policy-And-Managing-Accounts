# Group-Policy-And-Managing-Accounts

In this section of Active Directory, we are going to create a policy regarding password resets, enabling, and disabling accounts. 

To get started we're going to login to the domain controller VM with the admin credentials that we used last time.

# Setting up Group Policy

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

<img width="980" height="700" alt="image" src="https://github.com/user-attachments/assets/97d4f8de-7b2c-457a-84ff-6fbb9daa23e0" />



4. Configure Account Lockout Policy Settings
You will see three primary settings that you need to configure:

Account Lockout Duration:

**Definition:** The time in minutes that an account remains locked before it is automatically unlocked.

**Configuration:** Double-click on this setting, select Define this policy setting, and then set the duration for 30 minutes, click apply and click ok twice.

Account Lockout Threshold:

**Definition:** The number of failed logon attempts that will trigger an account lockout.

**Configuration:** Double-click on this setting, select Define this policy setting, and then set the threshold to 5 failed login attempts, click apply and click ok..

Allow Administrator account lockout:

**Definition:** This allows the administrator to lock an account from the overall domain (i.e. account user no longer works at the company).

**Configuration:** Double-click on this setting, select Define this policy setting to "Enabled", click apply and click ok.

Reset Account Lockout Counter After:

**Definition:** The time in minutes after which the failed logon attempts counter is reset to 0, assuming there are no additional failed logon attempts.

**Configuration:** Double-click on this setting, select Define this policy setting, and then set the time for 10 minutes, click apply and click ok..



5. Update Group Policy
You can wait for the Group Policy to propagate automatically, or you can force an update immediately. Login to the client vm as jane_admin, open Command Prompt by typing in "cmd" in the search bar on the bottom left, and type gpupdate /force, then press Enter.


<img width="1028" height="374" alt="image" src="https://github.com/user-attachments/assets/ade2a56e-b380-42ff-befc-6b92304565e2" />



6. Verify the Policy (Optional)
   
To verify the policy, you can use the rsop.msc (Resultant Set of Policy) tool on a client machine to see the applied settings.


Alternatively, you can also check the settings using the Group Policy Management Console.

***Important Considerations***

Account Lockout Threshold: Setting this too low (e.g., 1 or 2 attempts) can lead to unnecessary lockouts.

Account Lockout Duration: Setting this too high can be inconvenient for users but increases security.

Reset Account Lockout Counter After: Setting this too short could allow attackers to repeatedly attempt to log in without triggering a lockout.

# Login Attempts

1. In the domain controller vm, go to the Start Menu, the go to "Windows Administrative Tools", then scroll down and click on "Active Directory Users and Computers". Expand "mydomain.com" and then click "_EMPLOYEES" and you should see a bunch of users.


   <img width="942" height="656" alt="image" src="https://github.com/user-attachments/assets/810a573c-e10f-40c4-a2c8-ae6dc651a347" />


  
2. Pick a random user account we created previously with the Powershell script. As a reminder, that the password for all the generated users created is "Password1" with no quotations.

3. Exit and reenter back into the client vm and attempt to log in using "mydomain.com\firstname.lastname" with it 5 times with a bad password.


<img width="684" height="173" alt="image" src="https://github.com/user-attachments/assets/04a530a6-a041-4167-9098-d45a8e1ee167" />



After 5 attempts, go back to the domain controller and observe the user account that attempted to login by double clicking on the user. As you can see it's been locked, but of course it can be unlocked easily by checking the box, then clicking apply then ok.



<img width="505" height="667" alt="image" src="https://github.com/user-attachments/assets/a6e603e9-3b80-4991-ace6-9d1ea0e74d13" />


After unlocking the account, attempt to login the client vm with the credentials associated with the user.


# Password Reset

One thing that will occur in a real life scenario is resetting a password for a user to log back in to their account. Back in the domain vm with Active Directory Users and Computers (ADUC) opened, right click on the user that's been the test subject for this lab, and then click on "Reset Password."


<img width="458" height="478" alt="image" src="https://github.com/user-attachments/assets/e3dc78d1-09cd-48a0-bc0b-4607ec386f88" />


From there, type in the new password as "Password2" and the check the box that says "Unlock the users account" then cick ok.

<img width="472" height="317" alt="image" src="https://github.com/user-attachments/assets/6ff8a752-30c6-4e36-92d5-d4e3f88c7726" />

Exit and reenter the client vm with the user and their new password.


# Enabling and Disabling Accounts

This can be done by right clicking on the user, and enable / disable the account.

<img width="527" height="478" alt="image" src="https://github.com/user-attachments/assets/3edec0a6-5abc-4f89-aab1-fd32b7cf02cc" />


This concludes the lab! Great work! We seen how important Group Policy is as a concept, and how it handles day to day operations for enterprises across the globe. Without it, it would be very difficult for employees and clients within an organization to ensure smooth operations using computers and networks.

Remember, do not forget to stop the VM!! 

![image](https://github.com/user-attachments/assets/92abfa3a-0dc5-4284-8fde-ab364f9f546d)
