# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Creating Custom Policy
Create a custom policy to meet your specific needs for compliance or monitoring of cloud resources. Create a custom policy with remediation rules that are tailored to meet the requirements of your organization. When creating a new policy, you can either build the query using RQL or you use a saved search to automatically populate the query you need to match on your cloud resources. In this section, we will provide you a step by step guide on creating a custom policy.

1. In Prisma Cloud portal, go to Governance, click Add Policy > Config.
![alt text](/resources/pc-custompolicy-1.png?raw=true)

2. In the create new policy window, put in the policy name (use your initial to identify this policy of yours): ```Bechong - AWS Security Group allows all traffic on port 23```. For Severity, select High, click Next.
![alt text](/resources/pc-custompolicy-2.png?raw=true)

3. Input the following query into the Query section, and click Search. If input correctly, you should see the query returning some results. Click Search. You should see the query returns some result. Then, click Next.
```
config from cloud.resource where cloud.type = 'aws' AND api.name= 'aws-ec2-describe-security-groups' AND json.rule = isShared is false and (ipPermissions[?any((ipRanges[*] contains 0.0.0.0/0 or ipv6Ranges[*].cidrIpv6 contains ::/0) and ((toPort == 23 or fromPort == 23) or (toPort > 23 and fromPort < 23)))] exists)
```
![alt text](/resources/pc-custompolicy-3.png?raw=true)

_Note: In the event where Next button is greyed out, you will need to click Previous, enable & disable Build under Policy Subtype, and click Next again. This is a known UI bug for the current release._

4. On the Compliance Standards, click Next. On Remediation, leave everything as blank and click Submit. 

Once you have done creating the custom policy, continue with the next step [here](/06-AddingCustomPolicy.md).