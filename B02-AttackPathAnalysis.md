# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Identifying Cloud Environment Risk through Attack Path Analysis

To understand the true security risk of an application or infrastructure requires a complete assessment and correlation of a broad set of security signals. For example, if a virtual machine or an application is vulnerable to CVE-1234 that is network exploitable, is internet exposed, and has overly permissive IAM access to sensitive data, then this combination presents a relatively critical or high risk compared to an instance that contains the same vulnerability but is not internet exposed.

The Attack Path policies are out-of-the-box policies that are enabled by default. These policies identify the confluence of issues that increase the likelihood of a security breach and are based on relationships such as, overly permissive identities, permissions, network exposure, infrastructure misconfiguration, and vulnerabilities that would enable an attacker to target your application. Prisma Cloud helps you identify attack paths and presents them in a graph view, offering valuable security context to protect against high-risk threats, which often requires you to take immediate action.

This section will cover a high level details on looking into a single Attack Path alert.

1. Move to Cloud Security > Alerts > Risky Attack Paths.
![alt text](/resources/pc-attackpath-1.png?raw=true)

2. Click on Add Filter, choose Policy Name, and input the following, and tick the policy name. Click on any of the Alert ID.
```
Data exfiltration risk due to a publicly exposed AWS EC2 instance with s3:GetObject and s3:ListBucket permissions and not configured to use Metadata Service v2 (IMDSv2)
```
![alt text](/resources/pc-attackpath-2.png?raw=true)

3. On the popped up window, on Evidence tab, look into the details:
    * Is the EC2 instance internet reachable? If yes, how?
    * What misconfiguration does the EC2 instance has? 
    * Does the instance has access to S3 bucket? If yes, what is the name of the S3 bucket?

4. Click on the S3 bucket and click View Details.
![alt text](/resources/pc-attackpath-3.png?raw=true)

5. On the popped up window, click on Objects tab, and look into the details:
    * Is there a malware in this S3 bucket?
    * Is there any PII data in this S3 bucket as well?

With Attack Path policies, users are able to focus on prioritized alerts that increase the likelihood of a security breach. Also, with the information and investigation capabilities provided by Prisma Cloud, Security team can easily identify the risks involved and remediate the risks accordingly. 

Once you are done reviewing the attack path alert details, you can continue to the next section [here](/B03-IdentityRisks.md).
