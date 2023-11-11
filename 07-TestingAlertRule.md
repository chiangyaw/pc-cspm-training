# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Testing Alert Rule with Security Group
As part of this workshop, you will need to configure and test out the alert rule that you have created, with the associated cloud account & account group. 

Your cloud account should be onboarded, and you should be able to see your cloud assets in Prisma Cloud by now. If you are still not able to see them in Prisma Cloud, you can skip and come back to this section later. 

In this section, we will provide a step by step guide to create a Security Group which allows inbound traffic on port 23, for any IPv4 address. 

1. Login to your AWS account, and in the AWS console, search for ec2 on the search bar, click on EC2.
![alt text](/resources/aws-securitygroup-1.png?raw=true)

2. Click on Security Groups under Network & Security. And Click Create Security Group.
![alt text](/resources/aws-securitygroup-2.png?raw=true)

3. Input the Security Group name & Description, and choose the default VPC. Add an inbound rule by clicking Add rule, put 23 as the Port range, Source as Anywhere-IPv4.
![alt text](/resources/aws-securitygroup-3.png?raw=true)

4. Scroll down and click Create security group.

_Note: After creating the Security Group, the details will not be reflected immediately on Prisma Cloud. Prisma Cloud will take up to 15 minutes to reflect the changes, and trigger the alert notifications. Depending on the email security that is being used, it might take another 10-15 minutes to reach your mailbox. If you don’t see the alerts and the email notification, you can proceed to the next section while waiting._

5. Back to the Prisma Cloud tenant, go to Alerts > Alerts Overview. Click on Add Filter, and choose Policy Name. Type in your initials (for example, ```bechong```). This will filter down to the policy name that is created by you. Tick on the policy name, and you should be able to see the alert generated. Look through the resources, you should be able to see the security group you created in this section.
![alt text](/resources/pc-alertfilter-1.png?raw=true)
![alt text](/resources/pc-alertfilter-2.png?raw=true)

6. You should also receive an email notification which looks like this:
![alt text](/resources/pc-emailnotification-1.png?raw=true)

Once you are able to see the alert on the Prisma Cloud Alert Overview, and receive the email notification, you can continue to the next section [here](/08-GeneratingComplianceReport.md).