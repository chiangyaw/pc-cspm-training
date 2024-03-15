# Prisma Cloud Hands on Lab - Secure The Infrastructure
## IAC Security
As more and more enterprise users starting to adopt Infrastructure as Code (IaC), such as Terraform, which enables engineers to version control, deploy, and improve cloud infrastructure while leveraging DevOps processes. This also presents an opportunity to proactively improve the posture of cloud infrastructure and reduce the burden on security and operations teams.

Prisma Cloud scans IaC templates for misconfigurations and exposed secrets across the development lifecycle, embedding security in integrated development environments, continuous integration tools, repositories and runtime environments. Prisma Cloud enforces policy-as-code early through automation, preventing deploying security issues and providing automated fixes.

### Creating a Terraform repository in GitHub
In this section, you will be creating a Terraform repository in GitHub, which the terraform script will be used later to deploy a S3 bucket in your AWS account. Make sure you have logged into your GitHub personal account before the following action.

1. Head over to your [GitHub dashboard](https://github.com/dashboard), and click "New".
![alt text](/resources/github-new-repo.png?raw=true)

2. Give your new repository a name ```simpleenv```. Tick "Add a README file" and click "Create repository".
![alt text](/resources/github-new-repo-6.png?raw=true)

3. Click "creating a new file" to create a new file.
![alt text](/resources/github-new-file.png?raw=true)

4. Set the path to ```simpleenv/s3.tf```. Add the following code:
```
provider "aws" {
  region = "ap-southeast-1"
}

resource "aws_s3_bucket" "prismaclouds3" {
  bucket_prefix = "prismacloud-s3"

  tags = {
    Name                 = "Prisma Cloud"
    Environment          = "Dev"
  }
}

```

5. Click "Commit changes". On the popped up window, click "Commit changes".
![alt text](/resources/github-commit-1.png?raw=true)

Now you have created a terraform file in your GitHub repository!

### Setting Up Github Action with Yor
Yor is an open-source tool that automatically tags infrastructure as code (IaC) templates with attribution and ownership details, unique IDs that get carried across to cloud resources, and any other need-to-know information. It can run locally, as a pre-commit hook, or in a CI/CD pipeline.

For drift detection, the important tag is yor_trace. It’s a unique identifier that helps us trace from a cloud runtime configuration back to the IaC that provisioned it. To do that we need 3 elements:
* Yor automated tagging (this page)
* Integration with the VCS that stores the IaC (Adding Repository to PRisma Cloud, done in the previous section)
* Cloud integration (Onboarding your AWS account to Prisma Cloud, done in the previous section)

#### Adding Yor GitHub Action
1. In your “simpleenv” GitHub repository, click "Add file" > "Create new file".
![alt text](/resources/github-create-action-1.png?raw=true)

2. Set the path to ```simpleenv/.github/workflows/yor.yaml```. Add the following code below. Click Commit Changes and Save.

```
name: IaC trace

on:
  push:
  pull_request:
  workflow_dispatch:

jobs:
  yor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        name: Checkout repo
        with:
          fetch-depth: 0
          ref: ${{ github.head_ref }}
      - name: Run yor action and commit
        uses: bridgecrewio/yor-action@main
```

3. Navigate to Settings > Actions > General, under Workflow permissions, change to "Read and write permissions" and click "Save".
![alt text](/resources/github-create-action-2.png?raw=true)

This will run Yor to automatically tag your IaC resources every time you perform a push or pull request. The result will look something like this:
![alt text](/resources/github-yor-tags.png?raw=true)
The ```yor_trace``` tag will be used to track drift in your resources. 

#### Trying out Yor with GitHub Action
Let’s make a pull request to see how Yor is making changes to your existing Terraform code.

1. Go back to the ```simpleenv``` Github repository, click on s3.tf. On the next page, click on the edit file icon.
![alt text](/resources/github-edit-file-1.png?raw=true)

2. Make changes to the file, such as the one below, and click on “Commit changes”. On the pop up window, choose “Create a new branch for this commit and start a pull request. Leave the branch name as default, and click Propose changes.
![alt text](/resources/github-edit-file-2.png?raw=true)
![alt text](/resources/github-edit-file-3.png?raw=true)

3. On the next page, click “Create pull request”.
![alt text](/resources/github-pull-request-1.png?raw=true)

4. On the next page, wait for the IaC trace / yor to complete its action, and click “Merge pull request”, and then “Confirm merge”.
![alt text](/resources/github-pull-request-3.png?raw=true)

5. Move back to the Code tab, and click on s3.tf, you will notice that your code has been updated, with your new added code, and also the tags added by Yor:
![alt text](/resources/github-pull-request-2.png?raw=true)

### Onboarding your Terraform Repository to Prisma Cloud
In this section, you will be onboarding the Terraform repository to Prisma Cloud, so that Prisma Cloud is able to:
* Include your Infrastructure-as-Code files in daily scans.
* Scan changed resources in Infrastructure-as-Code files for every new build generated, (before the branch is merged into the main branch) and provide an actionable view of the results via GitHub checks.
* Open Pull Requests to Fix build-time issues detected in your branch.

1. In Prisma Cloud, go to Settings > Connect Provider > Code & Build Providers. Choose GitHub.
![alt text](/resources/pc-add-repo-1.png?raw=true)
![alt text](/resources/pc-add-repo-2.png?raw=true)

2. On the popped out window, click Previous. On the Configure Account window, click Authorize. You will be redirected to your GitHub page to install Prisma Cloud DevSecOps integration, choose the organization, choose Only select repositories, and select your ```simpleenv``` repository, and click Install & Authorize.
![alt text](/resources/pc-add-repo-3.png?raw=true)
![alt text](/resources/pc-add-repo-4.png?raw=true)
![alt text](/resources/github-install-pc-2.png?raw=true)

3. Once redirected back to Prisma Cloud, make sure "All current repositories" is ticked, and click Next. On the next page, click Done.
![alt text](/resources/pc-add-repo-5.png?raw=true)

Now you have onboarded your GitHub repository to Prisma Cloud. Prisma Cloud will now scan through for any misconfiguration. While waiting for the scan result, you can proceed to the next step to scan misconfiguration locally on your IDE.

#### Running through the misconfiguration of your S3 Bucket & Generating a pull request as fix
Once your Terraform code repository has been scanned, the misconfiguration will be flagged out in Prisma Cloud. This is how you as a Security Professional able to minimize misconfiguration on your IaC code with Prisma Cloud. 

By utilizing Prisma Cloud, you can also create a pull request as a suggestion for fix to the code repository. This will help to minimize the manual effort required for fix for the security professionals.

1. Choose Application Security > Home > Repositories. Filter the repository to your own Organization. Click on the number on IaC (this indicates the number of misconfiguration found in the IaC).
![alt text](/resources/pc-appsec-1.png?raw=true)

2. This page shows the misconfiguration in details, where you are able to click and run through the details, to understand the risk and the recommended fix.
![alt text](/resources/pc-appsec-2.png?raw=true)

3. Click on the resource name under AWS S3 Object Versioning is disabled, then click on the "+" icon at the end of the column. Then click the Submit button.

Note: It will take a couple of section for a pull request to be generated. Once completed, you will see a pull request generated on your code repository in GitHub. 

With this, you have reviewed a security alert due to a misconfiguration on your IaC code, and Prisma Cloud has provided a recommmendation to fix the misconfiguration!


### Deploying with Terraform
Now you have a Terraform code repository, it is time to deploy it to your AWS environment. For production, it will always go through an infrastructure pipeline, which can be tools like Terraform Cloud/Enterprise, Jenkins, Gitlabs, etc. For this lab, you will be using AWS CloudShell to deploy the S3 bucket with your terraform code.

#### Setup Github Access Token
1. First, go to github settings page [https://github.com/settings/profile](https://github.com/settings/profile)

2. Click on developers settings.
![alt text](/resources/github-add-access-key-1.png?raw=true)

3. Generate new token (classic). Put up a Note and tick repo as below. Click Generate token. 
![alt text](/resources/github-add-access-token-2.png?raw=true)
![alt text](/resources/github-add-access-token-3.png?raw=true)

4. Copy the access token which will be used later.
![alt text](/resources/github-add-access-token-4.png?raw=true)


#### Git Clone Your Repository & Deploy with Terraform
1. In your AWS console, click the AWS CloudShell icon.
![alt text](/resources/aws-cloudshell-1.png?raw=true)

2. In the AWS CloudShell, run the following to git clone your repository:
```
git clone https://github.com/<Your Git Account Name>/simpleenv.git
cd simpleenv
```
Note: you will need to replace the clone URL to your own code repository.
![alt text](/resources/github-clone-url-1.png?raw=true)
![alt text](/resources/aws-cloudshell-2.png?raw=true)

3. Install Terraform in your CloudShell:
```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
```
Note: you might need to run the commands above line by line to have terraform installed.

4. Run ```terraform --version``` to verify that terraform is installed.
![alt text](/resources/aws-cloudshell-3.png?raw=true)

5. Run ```terraform init``` & ```terraform apply --auto-approve```.
![alt text](/resources/aws-cloudshell-4.png?raw=true)

6. Verify that the s3 bucket has been created by searching for S3 on the top search bar in your AWS console page, and clicking into S3. You should see the S3 bucket created with the same ID in your AWS CloudShell.

With that, you have created a S3 bucket with your Terraform code repository!
Note: The installation of Terraform on your AWS CloudShell is temporary. If *you are disconnected from your CloudShell, you might need to reinstall Terraform to re-apply the code or destroy the S3 bucket later. 


#### Creating an alert for Drift
Before we proceed, make sure your AWS account has been onboarded to the Prisma Cloud tenant.

1. In Prisma Cloud > Cloud Security > Alerts > View Alert Rules. Click on Add Alert Rule on the side car window.
![alt text](/resources/pc-alert-1.png?raw=true)

2. Input an alert rule name (put in your name/initial, such as bechong-drift-detection). Enable Alert Notification, and click Next.
![alt text](/resources/pc-alert-2.png?raw=true)

3. Select your Account Group and click Next.
![alt text](/resources/pc-alert-3.png?raw=true)

4. In the Assign Policies window, in the search bar, type "aws traced" and you should see the policy show up in the list, select the "AWS traced resources are manually modified", and click Next.
![alt text](/resources/pc-add-alert-rule-4.png?raw=true)

5. Enable email notification by clicking Emails, input your email address and click Next.
![alt text](/resources/pc-add-alert-rule-5.png?raw=true)

6. In the Summary window, just Click Save.

#### Create Drift
Make sure that you have applied the Terraform resources from the Pull Request section, and confirm in your AWS console that your new S3 bucket is up. Go to the [S3 console](https://s3.console.aws.amazon.com/s3/home) and confirm that there is a new bucket running. 

1. In the S3 AWS Console, click on the newly created S3 bucket, and click on "Properties" tab. 
![alt text](/resources/aws-s3-properties.png?raw=true)

2. Scroll down to "Tags" and click Edit.
![alt text](/resources/aws-s3-properties-2.png?raw=true)

3. Click "Add tag", type in "Drift for key, and "ThisisTheDrift" for value. Click Save changes.
![alt text](/resources/aws-s3-properties-3.png?raw=true)

You have now created a simple drift in your s3 bucket. Now, time to wait until Prisma Cloud notices the change and generate the alert. This can take anywhere from 15 minutes to an hour, depending on the scan cycle. Once the drift is detected, you can either run ```terraform apply``` again in Terraform Cloud to fix the drift by matching it back to the IaC configuration. If the cloud configuration is correct, the changes on the IaC template can be made by submitting a PR through Prisma Cloud. In the Projects page, you will be able to find the drift by filtering IaC Categories to "Drift". Click on the policy and the "+" icon, and click Submit.

You're at the end of the Prisma Cloud Hands On Lab. You can proceed to the clean up section [here](/12-CleaningUp.md) to clean things up before you leave the session. Once again, thank you for joining us in the Prisma Cloud Hands On Lab!