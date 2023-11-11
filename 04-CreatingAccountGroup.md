# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Creating Account Group in Prisma Cloud
You can use Account Groups to combine access to multiple cloud accounts with similar or different applications that span multiple divisions or business units, so that you can manage administrative access to these accounts from Prisma Cloud.

When you onboard a cloud account to Prisma Cloud, you can assign the cloud account to one or more account groups, and then assign the account group to Prisma Cloud Administrator Roles. Assigning an account group to an administrative user on Prisma Cloud allows you to restrict access only to the resources and data that pertain to the cloud account(s) within an account group. Alerts on Prisma Cloud are applied at the cloud account group level, which means you can set up separate alert rules and notification flows for different cloud environments. In addition, you can also create nested account groups which provides you more flexibility in mapping out your internal hierarchy.

This section will provide a step by step guide on creating an Account Group, and then adding your AWS account to the created Account Group.

1. Go to Settings > Account Groups. Click Add Account Group. Input a Account Group name (you can put in your name/initial, such as bechong-Account-Group). Add your newly added AWS account into the Account Group, and click Save.
![alt text](/resources/pc-accountgroup-1.png?raw=true)
![alt text](/resources/pc-accountgroup-2.png?raw=true)

Once you have created the Account Group, continue with the next step [here](/05-CreatingCustomPolicy.md))