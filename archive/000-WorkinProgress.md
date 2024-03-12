### Work in Progress
### Integrating Prisma Cloud to your IDE
Integrating Prisma Cloud to your IDE, such as Visual Studio Code (VScode) makes it possible for you to identify misconfigurations before you commit your code, and avoid pull requests that can potentially fail builds due to undetected misconfigurations. This section covers the integration with your IDE.

1. In your GitHub page, click into your ```simpleenv``` code repository. Click Code and Create codespace on main.
![alt text](/resources/github-code-1.png?raw=true)

2. On the popped out tab, you will see an IDE environment with 



#### Running through the misconfiguration of your S3 Bucket & Generating a pull request as fix
Once your Terraform code repository has been scanned, the misconfiguration will be flagged out in Prisma Cloud. This is how you as a Security Professional able to minimize misconfiguration on your IaC code with Prisma Cloud. 

1. Choose Application Security > Home > Repositories. Filter the repository to your own Organization. Click on the number on IaC (this indicates the number of misconfiguration found in the IaC).
![alt text](/resources/pc-appsec-1.png?raw=true)

2. This page shows the misconfiguration in details, where you are able to click and run through the details, to understand the risk and the recommended fix.
![alt text](/resources/pc-appsec-2.png?raw=true)

3. Click on the resource name under AWS S3 Ob