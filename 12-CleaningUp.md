# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Cleaning Up

Congratulations for reaching till this stage as part of the workshop. If you still have additional time to spare and you would like to explore more on Prisma Cloud, you can head over to the bonus section [here](/B01-AgentlessSecurity.md).

To complete the lab session, clean up and remove the following:
In Prisma Cloud:
1. Delete your AWS account in Settings > Providers.
2. Delete the alert rule you have created in Alerts > View Alert Rules.
3. Delete the GitHub integration in Settngs > Providers > Repositories.

In AWS Account:
1. Delete both of the Security Groups that you have created.
2. Delete the Cloud Formation deployed as part of Prisma Cloud integration.
3. Run ```terraform destroy --auto-approve``` to destroy the S3 bucket created in [IaC Security lab](/B04-IaCSecurity.md). 

In GitHub Account:
1. Delete the Prisma Cloud DevSecOps integration in your GitHub account [here](https://github.com/settings/installations).

You have reached the end of the workshop. Thank you for your time and hope to see you again!