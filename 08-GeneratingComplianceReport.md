# Prisma Cloud Hands on Lab - Secure The Infrastructure
## Generating Compliance Report
As part of providing Visibility & Control with Prisma Cloud, you can use the Compliance Dashboard as a tool for risk oversight across all the supported cloud platforms and gauge the effectiveness of the security processes and controls you have implemented to keep your enterprise secure. You can also create compliance reports and run them immediately, or schedule them on a recurring basis to measure your compliance over time.

The Compliance Dashboard supports you whether you’ve spent a lot of time designing and establishing internal regulations and devising the right policies, or you use the built-in regulatory compliance standards available on Prisma Cloud.

For the list of out-of-the-box regulatory compliance standards that Prisma Cloud supports, you can refer to the list [here](https://docs.prismacloud.io/en/classic/cspm-admin-guide/prisma-cloud-compliance/compliance-dashboard).

In this section, we will provide a step by step guide to generate a compliance report based on PCI-DSS, which can be used as a reference within organization for internal or external audit. 

1. In Prisma Cloud portal, click on Reports > Create Report. 
![alt text](/resources/pc-compliancereport-3.png?raw=true)

2. Input & choose the following:
    * Name - (use your initial, ```bechong-PCIDSS-report```)
    * Cloud Type - AWS
    * Date - Most recent
    * Compliance standard - PCI DSS v4.0
    * Account Group - ```<choose your own account group>```
    * Leave everything else as default
    * Use One Time to generate the report, and click Save Report
![alt text](/resources/pc-compliancereport-2.png?raw=true)

_Note: We can support generating report through recurring basis such as daily, weekly, and monthly. An email notification can be sent when a report is ready for viewing with the configured interval. You can look into Recurring to see what are the options available._

3. Once done, it will take awhile till the report is ready for download, and usually it will take up to 5 minutes. Once it is ready, click the Download icon to download the compliance report in PDF.
![alt text](/resources/pc-compliancereport-4.png?raw=true)

4. Take a look with the compliance report and see what are the items covered within the report.

_Note: As your AWS account is empty, you might not see any resources in the PCI DSS report which only covers your AWS account. Re-run the steps in this section with Default Account Group instead, which covers other demo AWS accounts._

Once you are reviewed the compliance report, you can move on to the next section by clicking [here](/07-ScanningwithTerraformCloud.md)).
