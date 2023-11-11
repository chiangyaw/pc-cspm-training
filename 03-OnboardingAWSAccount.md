# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Onboard AWS Account to Prisma Cloud
For Prisma Cloud to provide visibility & control to cloud accounts that are onboarded to Prisma Cloud. As part of this lab, you will need to onboard an AWS account to the Prisma Cloud lab tenant. This section will provide a step by step guide to onboard AWS account to Prisma Cloud.

1. On the Prisma Cloud tenant, Click on Settings (top right corner). On the next page, click on "Provider", then "Connect Provider" > "Cloud Account". 
![alt text](/resources/pc-onboarding-1.png?raw=true)
2. Choose Amazon Web Services on the pop up window. Click on Accounts, untick on Agentless Workload Scanning, and then click Next.
![alt text](/resources/pc-onboarding-2.png?raw=true)

3. Input your AWS Account ID, and Account Name (put in your name/initial, such as *bechong*-AWS-Account). Enable Remediation by ticking the checkbox. Click “Create IAM Role”. This will prompt a new tab to create a CloudFormation stack for the IAM role.
![alt text](/resources/pc-onboarding-3.png?raw=true)
**Note: Once you click on "Create IAM Role", you will be re-directed to us-east-1 N.Virginia region on AWS console. On the same page, click on top right region selection, change it back to ap-southeast-1 Singapore region.**

4. Tick on “I acknowledge that AWS CloudFormation might create IAM resources with custom names”, and click Create Stack.
![alt text](/resources/aws-onboarding-1.png?raw=true)

5. Once creation is completed, go to the Outputs tab, copy the value of PrismaCloudRoleARN, paste it into the Prisma Cloud onboarding window in the IAM Role ARN textbox. Click Next.
![alt text](/resources/aws-onboarding-2.png?raw=true)

6. Wait for the authentication check to be completed, you should see everything as green tick except those which are not enabled. Click Save and Close to proceed.
![alt text](/resources/pc-onboarding-4.png?raw=true)

Your AWS assets information will not be available in Prisma Cloud immediately. It will take up to 24 hours to be reflected, but for small environments, you should be able to see it in less than 1 hour. In the meantime, feel free to proceed to the next step [here](/04-CreatingAccountGroup.md))