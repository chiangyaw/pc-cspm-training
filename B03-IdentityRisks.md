# Work in Progress
# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Investigating Identity Risk

Identity is the new perimeter. Prisma Cloud IAM security capabilities help you evaluate the effective permissions assigned to users, workloads, and data (also called entitlements) on your cloud provider so that you can properly administer identity and access management (IAM) policies and enforce access using the principle of least privilege.

The IAM Security module runs a proprietary algorithm to calculate effective permissions of the users across your cloud service providers. For example, the algorithm combines various cloud sources such as AWS IAM roles, AWS IAM policies, AWS IAM groups, AWS resource based policies, and AWS service control policies (SCPs) to compute the net effective permissions of cloud resources. It extends the Config query in RQL ( config from iam where ) to help you gain visibility into the entities in your cloud environment.

For example, with the net effective permissions calculation you can now discover the permissions for a specific user in your AWS, Azure, or GCP environment, such as, a user who has access to a AWS S3 bucket, Azure storage account, or Google storage bucket.

Note: IAM Security has to be enabled for new tenant as part of the initial configuration. To enable IAM Security module, refer [here](https://docs.prismacloud.io/en/classic/cspm-admin-guide/prisma-cloud-iam-security/enable-iam-security) for more details.

This section will cover a high level details on looking into a single IAM alert in Prisma Cloud.

1. On the same attack path alert in the previous section, click on the Primary Asset > View Details.
![alt text](/resources/pc-identityalert-1.png?raw=true)

2. Click on IAM Details, and look into the details:
    * What is the name role attached to the EC2 Instance?
    * What are the inline policies that are attached to this role?
    * Which actions are not being accessed in the tracking period?

3. Click on Alerts, and look into the details:
    * Is there any IAM alerts generated for this EC2 Instance?
    * What are the severity of these alerts?

Prisma Cloud is able to calculate net effective permissions for specific users or machines in your cloud accounts. With this information, Prisma Cloud is also able to provide information on permission usage and recommendation on least privilege access, which ultimate reduce identity risks in your cloud environment.

Once you are done reviewing the identity risks, you can continue to the next section [here](/B04-IaCSecurity.md).