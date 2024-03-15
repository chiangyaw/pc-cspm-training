# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Creating an Account Group Read-Only Role and attach to your credentials
Prisma Cloud provides Granular Role-Based Access Control (RBAC) to limit access to Prisma Cloud, such as Account Group Read-Only access. Create Prisma Cloud roles to restrict user access to cloud accounts within an account group.

Roles on Prisma Cloud enable you to specify what permissions an administrator has, and to which cloud accounts they have access, what policies they can apply, and how they interact with alerts and reports, for example.

When you create a cloud account, you can assign one or more cloud account to account group(s) and then attach the account group to the role you create. This flow allows you to ensure the user/administrator who has the role can access the information related to only the cloud account(s) to which you have authorized access.

This section covers a step by step guide to create a Account Group Read-Only Role, and attach it to your own credential. The same steps can be applied to other team members within the organization.

1. In Prisma Cloud tenant, go to Settings > Access Control. Click on Role, and Click Add and choose Roles.
![alt text](/resources/pc-agreadonly-1.png?raw=true)

2. Input the following:
    * Role Name - with your initials to identify them, such as bechong-ag-readonly-role
    * Permission Group - Account Group Read Only
    * Account Group - your account group (the one you created)
	* Leave the rest as default, click Submit.
![alt text](/resources/pc-agreadonly-2.png?raw=true)

3. Click Users and search for your own email address with the search bar. Click on the Edit icon.
![alt text](/resources/pc-agreadonly-3.png?raw=true)

4. Click on Assign Roles, and add in the new role that you have created. Click Save and Close. 
![alt text](/resources/pc-agreadonly-4.png?raw=true)

5. Once you have done this, you should be able to assume the read only role now. Click on the human icon on the top right corner, and choose the role that you have created under Active Role. Click on the new role. 
![alt text](/resources/pc-agreadonly-5.png?raw=true)

6. With the new role, you should only be able to see your own Account Group, and the Cloud Accounts associated with the Account Group. You won’t be able to make any changes since this is a Read Only role. 

Once you are able to assume the Read Only role, you can assume back the System Admin role and move to the bonus sections by clicking [here](/B01-AgentlessSecurity.md).

If you are done with the lab and do not have enough time to proceed to the bonus stages, you can just move on to clean up [here](/E01-CleaningUp.md)