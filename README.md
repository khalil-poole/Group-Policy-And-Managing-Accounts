# Group-Policy-And-Managing-Accounts

In this section of Active Directory, we are going to create a policy regarding password resets, enabling, and disabling accounts. 

1. To get started we're going to login to the domain controller VM with the admin credentials that we used last time.

2. Go to the Start Menu, the go to "Windows Administrative Tools", then scroll down and click on "Active Directory Users and Computers". Expand "mydomain.com" and then click "_EMPLOYEES" and you should see a bunch of users.
  
3. Pick a random user account we created previously with the Powershell script. As a reminder, that the password for all the generated users created is "Password1" with no quotations.

5. Remote desktop the client vm and attempt to log in with it 10 times with a bad password

