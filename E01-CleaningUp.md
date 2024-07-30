# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Cleaning Up

Congratulations for reaching till this stage as part of the workshop. 

To complete the lab session, clean up and remove the following:
In Prisma Cloud:
1. Delete your AWS account in Settings > Providers.
2. Delete the alert rule you have created in Alerts > View Alert Rules.
3. Delete the GitHub integration in Settngs > Providers > Repositories.

In AWS Account:
1. Delete both of the Security Groups that you have created.
2. Delete the Cloud Formation deployed as part of Prisma Cloud integration.
3. Run ```terraform destroy --auto-approve``` to destroy the S3 bucket created in [IaC Security lab](/15-IaCSecurity.md). 

In GitHub Account:
1. Delete the Prisma Cloud DevSecOps integration in your GitHub account [here](https://github.com/settings/installations).
2. Delete the code repository that you have created in Settings > Delete this repository. 

You have reached the end of the workshop. Thank you for your time and hope to see you again!