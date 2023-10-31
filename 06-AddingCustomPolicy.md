# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Adding Custom Policy to an Alert Rule
In order for a policy to generate alert, it has to be added to an alert rule. Users can create an alert rule that associates all of the cloud accounts in an account group with the set of policies for which you want Prisma Cloud to generate alerts. You can view the alerts for all of your cloud environments directly from Prisma Cloud and drill down in to each to view specific policy violations. You can also send these alert notifications to a third party tools, such as e-mail, ticketing systems and more. In this section, we will cover a step by step guide on creating the alert rule, associating it with your account group, and enable e-mail notification.

1. Click on Alert > View Alert Rules. Click on Add Alert Rule on the pop up window.
![alt text](/resources/pc-alertrule-1.png?raw=true)
![alt text](/resources/pc-alertrule-2.png?raw=true)

2. Input a Alert Rule Name (you can use your initials on this as well, ```bechong-sg-23-alert-rule```). Enable Alert Notifications, and then click Next.
![alt text](/resources/pc-alertrule-3.png?raw=true)

3. To assign a target, choose the Account Group that you have created with your AWS account, and click Next.
![alt text](/resources/pc-alertrule-4.png?raw=true)

4. To assign policies to this alert rule, enable the custom policy that you have created, and click Next.
![alt text](/resources/pc-alertrule-5.png?raw=true)

5. On Configure Notifications, click on Emails, put in your email address under Emails, tick Enabled, and click Next.
![alt text](/resources/pc-alertrule-6.png?raw=true)

6. Run through the Summary page, and click Save. 

_Note: We are using Emails as a notification in this example. Email is not the best approach from notification perspective as there is usually delay when a notification is triggered, which can be due to email security installed in the customer’s email account/server. For actual deployment, typical notifications can be AWS Security Hub, SNS, etc._

Once you have done creating the alert rule, continue with the next step [here](/07-ScanningwithTerraformCloud.md))