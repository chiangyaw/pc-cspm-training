# Prisma Cloud Hands on Lab - Secure The Source
## Software Composition Analysis
Software Composition Analysis (SCA) empowers you with information on open source software used in source code that has the potential to expose your organization to critical vulnerabilities, license compliance or legal and compliance issues. On Prisma Cloud, you can view the latest contextualized SCA information from continuous scans across all your integration integrations of IDE, VCS repositories and CI/CD pipelines.

In this section, you will be acting as a developer where you will need to create a new feature branch, where you new code can be created and tracked. At the same time, Prisma Cloud provides details on the security risks, helping the approver to make informative decision on the feature rollout. 

### Cloning the repository in GitHub
1. Fork the code repository [here](https://github.com/try-panwiac/vulnerable-front-end) to your own github account.
![alt text](/resources/github-sca-1.png?raw=true)

![](/resources/github-sca-2.png?raw=true)


2. Once forked, you will need to create a codespace environment by clicking Code > Codespaces > Create codespace on main. 
![](/resources/github-sca-3.png?raw=true)


3. Once the codespace environment is provisioned completely, you will be able to access the files, which look exactly like a VS code. If you would like to challenge yourself, you can use VS code instead. However, you will need to install components such as ```node```, ```npm```, ```yarn```, ```git``` separately.
![](/resources/github-sca-4.png?raw=true)

4. On the terminal, run the following to switch to ```cas-feature-branch```.
```
git switch -c cas-feature-branch
```
![](/resources/github-sca-5.png?raw=true)

5. To add a new logging functionality for the web app, we will be using a third party open source software package called 'morgan'. This package provides HTTP request logger middleware functionality. Typically developer uses package manager like ```yarn``` to manage JavaScript packages. To add the new software package, run the following on the terminal:
```
yarn add morgan@1.0.0 -E
```
![](/resources/github-sca-6.png?raw=true)

### Viewing Vulnerability in VS Code
One of the integration with Prisma Cloud would be with VS Code. To integrate with Prisma Cloud on VS Code, you will need to install an extersion called ```checkov```. Once installed, you will need to put up the Prisma Cloud access and secret keys so that VS Code is able to poll the policies configured, and inform the developers if there is any security issue within their code. 
1. To integrate with Prisma Cloud, you will first need to generate a Prisma Cloud Access & Secret Key. Go to Prisma Cloud > Settings > Access Control > Add > Access Key. Put up a name and click Save. Download the csv file for reference later, and click Done.
![](/resources/pc-accesskey-1.png?raw=true)
![](/resources/pc-accesskey-2.png?raw=true)
![](/resources/pc-accesskey-3.png?raw=true)

2. On Codespace or VS Code, click on Extension, search for ```checkov```, and click Install.
![](/resources/codespace-checkov-1.png?raw=true)

3. Once installed, click on the settings icon, and click on Extension Settings.
![](/resources/codespace-checkov-2.png?raw=true)

4. Put up the following details:
    * Checkov: Prisma URL - ```https://api.sg.prismacloud.io```
    * Checkov: Token - ```<YourGeneratedAccessKey>::<YourGeneratedSecretKey>```
Note: If you are running this hands on lab in a different region, you might have a different Prisma Cloud URL. You can cross check this when you're logging into your Prisma Cloud tenant. For more details on the API URL, refer [here](https://pan.dev/prisma-cloud/api/cspm/api-urls/).

5. Once done, open the package.json file, you will notice that it says Checkov scanning at the bottom of the codespace. It will take some time in codespace as the compute resource is limited. Once the scan is completed, you can hover your mouse to the line of code which is flagged as security risk. You can also view the list of risks under "Problems".
![](/resources/codespace-checkov-3.png?raw=true)

As a developer, you will be able to view any security risks introduced to your code while coding on the IDE. This helps organizations to minimize security risks through secure coding practice, starting on the developer's IDE.

### Viewing Vulnerability in Pull Request
If the developer tend to ignore the security risks flagged out in the IDE, they will just commit the code to the feature branch. Whenever a branch is created, the new code in the branch is is required to be merged into the main code with a process called Pull Request. Through Pull Request, an approver (typicaly senior developer or manager) would be looking into the new code, and decide whether the new code can be merged into the main code. Prisma Cloud is also able to flag out the security risks as comments in the same Pull Request, helping the approver making a much more information decision.

1. On Codespace terminal, run the following to commit your new code to ```cas-feature-branch```.
```
git add .
git commit -m "added morgan 1.0.0"
git push origin cas-feature-branch
```

2. Once done, go back your the github code repository page, refresh the page, you will notice that there is a branch created by clicking "main".
![](/resources/github-pr-1.png?raw=true)

3. To generate a Pull Request, click Pull Requests > New Pull Request. On the next page, choose your code repository as the base repository and base as ```main```, and compare as ```cas-feature-branch```. Then, click "Create pull request" twice. 
![](/resources/github-pr-2.png?raw=true)
![](/resources/github-pr-3.png?raw=true)

4. On the pull request page, you will start to see prisma-cloud-devsecops analyzing the code, and then provide the details of vulnerabilities discovered. 
![](/resources/github-pr-4.png?raw=true)

These details helps the approver to make a much more informative decision. If the new code introduces some serious vulnerabilities, it will potentially lead to an exploit in production application. Therefore, in this situation, the approver can choose not to merge and provide comments on why not to merge. 

### Reviewing Vulnerabilities in Prisma Cloud
While Prisma Cloud is able to help developers to make a much more informative decision, Prisma cloud is also able to assist on fixing those vulnerabilities. 

1. Sign in to Prisma Cloud, move to Application Security > Projects. Use the filter and choose your repository.
![](/resources/pc-appsec-3.png?raw=true)
![](/resources/pc-appsec-4.png?raw=true)

2. Click on the search icon, and type in "morgan". Once the search is completed, you will be able to see all the different CVEs associated with "morgan".
![](/resources/pc-appsec-5.png?raw=true)
![](/resources/pc-appsec-6.png?raw=true)

3. To submit a fix, click on the "+" icon for CVE-2019-5413, and click "Submit". The fix is submitted to your repository as a Pull Request. As this is a batch job, it will take a few minutes before the PR appears in your repository.
![](/resources/pc-appsec-7.png?raw=true)

4. Once completed, move back to your code repository in Github, look into the additional Pull Request that have been submitted by Prisma Cloud. Click on "Files changed". On the "Files changed" tab, you will be able to see all the changes that Prisma Cloud is recommending as part of this Pull Request.
![](/resources/pc-appsec-8.png?raw=true)
![](/resources/pc-appsec-9.png?raw=true)

Why is this important? By being able to generate a fix via Pull Request, it save up a lot of manual effort and time to have the vulnerabilities fixed on application code. Without Prisma Cloud, the user will need to manually research on the vulnerability, knowing which version has the vulnerability fixed, and at the same time, generating the pull request manually. With Prisma Cloud, the approver just need to look into the details, and approve the pull request. Once done, the CI/CD process will take its place, building the package with the fixed version.

You're at the end of the Prisma Cloud Hands On Lab. You can proceed to the clean up section [here](/E01-CleaningUp.md) to clean things up before you leave the session. Once again, thank you for joining us in the Prisma Cloud Hands On Lab!