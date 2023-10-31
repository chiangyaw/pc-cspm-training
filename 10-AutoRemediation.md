# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Alert Rules with Auto-Remediation
To facilitate rapid incident response, configure Prisma Cloud to automatically remediate cloud Security policy violations in your cloud environments using multi-step CLI commands in one-click. You can also configure Prisma Cloud to automatically resolve policy violations, such as misconfigured security groups, you can configure Prisma Cloud for automated remediation. To automatically resolve a policy violation, Prisma Cloud runs the CLI command associated with the policy in the cloud environments where it discovered the violation. 

To enable automated remediation, identify the set of policies that you want to remediate automatically and verify that Prisma Cloud has the required permissions in the associated cloud environments. Then Create an Alert Rule for Run-Time Checks that enables automated remediation for the set of policies you identified.

In this section, we will provide a step by step guide to configure an alert rule with auto-remediation enabled, to remediate a security group with an inbound rule on port 22 for any IPv4 address, which will be created as part of this section as well.

1. Click on Alert > View Alert Rules. Click on Add Alert Rule on the pop up window.
![alt text](/resources/pc-alertrule-1.png?raw=true)
![alt text](/resources/pc-alertrule-2.png?raw=true)

2. Input a Alert Rule Name (you can use your initials on this as well, ```bechong-sg-22-alert-auto-remediation-rule```). Enable Alert Notifications & Auto-Remediation (click Confirm when asked to continue), and then click Next.
![alt text](/resources/pc-alertruleaa-1.png?raw=true)

3. Assign the same Account Group that you have created with your AWS account, and add include Resource Tags with the following input, and click Next.
    * Key - Type
    * Value - PrismaCloudTest

![alt text](/resources/pc-alertruleaa-2.png?raw=true)

_Note: The reason why we are adding a tag is because we don’t want the auto-remediation to affect all the Security Group resources in your current AWS account for this particular section. We just want to test out the Auto-Remediation capabilities with Prisma Cloud for a specific Security Group_

4. In the Assign Policies window, choose the following policy:
```
AWS Security Group allows all traffic on SSH port (22)
```
![alt text](/resources/pc-alertruleaa-3.png?raw=true)


5. Configure email notification the same as before. Click Next.
![alt text](/resources/pc-alertrule-6.png?raw=true)

6. Click Save on the summary page.

## Testing Auto-Remediation with Security Group

7. Login to your AWS account, and in the AWS console, search for ec2 on the search bar, click on EC2.
![alt text](/resources/aws-securitygroupaa-1.png?raw=true)

8. Click on Security Groups under Network & Security. And Click Create Security Group.
![alt text](/resources/aws-securitygroupaa-2.png?raw=true)

9. Input the Security Group name & Description, and choose the default VPC. Add an inbound rule by clicking Add rule, put 22 as the Port range, Source as Anywhere-IPv4.
![alt text](/resources/aws-securitygroupaa-3.png?raw=true)

10. Scroll down and click Create security group.

_Note: Similar as before, after creating the Security Group, the details will not be reflected immediately on Prisma Cloud. Prisma Cloud will take up to 15 minutes to reflect the changes, and trigger the alert notifications. Depending on the email security that is being used, it might take another 10-15 minutes to reach your mailbox. If you don’t see the alerts and the email notification, you can proceed to the next section while waiting._

11. Back to the Prisma Cloud tenant, go to Alerts >  Overview. Click on Add Filter, and choose Policy Name. Type in the policy name ```AWS Security Group allows all traffic on SSH port (22)```, and tick on the policy. Change Alert Status from Open to Resolved, and you should see a list of assets with the alert resolved. Look through the resources, you should be able to see the security group you created in this section.

![alt text](/resources/pc-alertruleaa-4.png?raw=true)

12. Click on the Asset Name, and Audit Trail on the pop up window. You should be able to see the resource state was updated by Prisma Cloud / Redlock.

![alt text](/resources/pc-alertruleaa-5.png?raw=true)

13. You should also receive an email notification that the alert is being remediated. 

14. Back to AWS console, choose the Security Group you have created, look into Inbound rules. You will notice that the inbound rule that you have created for port 22 has now been removed.
![alt text](/resources/aws-securitygroupaa-4.png?raw=true)

Once you are able to see the alert remediated on Alert Overview, and inbound rules removed by Prisma Cloud, you can move on to the next section by clicking [here](/07-ScanningwithTerraformCloud.md).