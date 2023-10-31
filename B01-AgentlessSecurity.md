# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Identifying Vulnerabilities & Compliance Risk through Agentless Security
Agentless scanning lets you inspect the risks and vulnerabilities of a cloud workload without having to install an agent or affecting the execution of your workload. Prisma Cloud gives you the flexibility to choose between agentless and agent-based security using Defenders. Prisma Cloud supports agentless scanning of cloud workloads on AWS, Azure, GCP, and OCI for vulnerabilities and compliance.

In AWS, Azure, and GCP you can also use agentless scanning for container images as well as Serverless functions.

To understand more on how Agentless Scanning works with Prisma Cloud, refer to the weblink [here](https://docs.prismacloud.io/en/classic/compute-admin-guide/agentless-scanning/agentless-scanning) for more details.

This section provides a high level guide on how to identify vulnerabilities & compliance risks via Prisma Cloud.

_Note: This section does not include a step by step guide to enable Agentless Security in your AWS account, as agentless scanning will cost a very minimal amount of cost to your AWS account. If you are looking to try out Agentless Scanning with your AWS account, move on to this section [here](/00-Introduction.md)._

1. In Prisma Cloud portal, choose Runtime Security > Monitor > Vulnerabilities > Host. Look into the hosts that are identified by Prisma Cloud.
![alt text](/resources/pc-agentless-1.png?raw=true)

2. Review the details on the findings:
    * Can you tell which hosts are identified by Agentless or Agent?
    * Look into any of the host identified by Agentless Scanning, what are the critical vulnerabilities found on the host?

3. Click on Images on the same vulnerabilities window. Look into the container images that are identified by Prisma Cloud.
![alt text](/resources/pc-agentless-2.png?raw=true)

4. Review the details on the findings:
    * Can you tell which images are identified by Agentless or Agent?
    * Look into any of the images identified by Agentless Scanning, what are the critical vulnerabilities found on the image?

5. Go to Monitor > Compliance > Hosts. Look into the hosts that are identified by Prisma Cloud. Review the details on the findings on critical compliance items. Perform the same for images.
![alt text](/resources/pc-agentless-2.png?raw=true)

Once you are done reviewing the vulnerabilities & compliance risks, you can continue to the next section [here](/07-ScanningwithTerraformCloud.md).