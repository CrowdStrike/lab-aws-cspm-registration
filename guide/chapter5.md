Cloud Security Lab Series
# AWS CSPM Registration 101
## Chapter 5 - Using a Custom Template for Commercial AWS to GovCloud Falcon

In this lab we will use a custom template to address the need for a Permissions Boundary attached to all roles which will resolve the failed onboarding phase and complete registration.  But there are many reasons why a customer may want to use an open-source CloudFormation template.  They may want to add tags to every resource, change the name of the EventBridge IAM Role or simply have the code stored in their source control.

Here's a list of what a customer can change in our templates:
- EventBridge Role name
- Tags on Resources
- Permissions Boundary on IAM Roles

Generally speaking we should not indicate that any other aspects of the templates can change because additional changes will likely break the functionality of CSPM.

### Retrieve and Upload the Custom Templates

1. View the AWS templates [here](../code/register-gov-falcon.json) and [here](../code/register-gov-falcon-ioa.json)

These are the same templates that are provided in the Falcon Console, but with a conditional Permissions Boundary Attribute applied to all IAM Roles.  **register-gov-falcon.json** is the parent template, it references and creates an additional stack from **register-gov-falcon-ioa.json**

2. Click the download icon for each template.

![](../images/download-template.png)

3. Navigate back to CloudFormation in the AWS Console.
4. Select our failed stack and click on the Parameters tab.

Our new template won't have these parameters pre-filled so we will need to enter them in.  To have them handy, we will continue in another tab.

5. Search for "S3" in the AWS Services search bar
6. Right click on **S3** and **Open Link in New Tab**
7. In the new tab, open the S3 Bucket cf-templates-{randomstring}
8. Upload the files you downloaded in the prior step: **register-gov-falcon.json** & **register-gov-falcon-ioa.json**
9. We will use the S3 URL (NOT S3 URI) for register-gov-falcon.json in the next step

### Launch Template
1. Search for "CloudFormation" in the AWS Services search bar
2. Right click on **CloudFormation** and **Open Link in New Tab**
3. In the new tab, click **Create Stack** and select **With new resources (standard)**
4. Under the specify template section, paste the S3 URL for **register-gov-falcon.json**
5. Click Next
6. Give the Stack a unique Name and fill in the Parameters using the information from your failed stack in the other tab.
7. A new Parameter is available `S3Bucket`. The value should be the name of the bucket where you uploaded the template files (cf-templates-{randomstring})

**Note**:  Be wary of trailing spaces when copying and pasting information into parameters.  These must be removed to prevent failures.

9. A new Parameter is available `PermissionsBoundary`.  The value should be BoundaryForAdministratorAccess
10. Click Next
12. In the Stack Failure options section of this page, select `Preserve successfully provisioned resources`

This will allow you to easily update the stack if any additional failures occur.

13. Click Next
14. Check the box in the Capabilities section and click Submit

Once this stack finishes, the onboarding phase is complete.

### Confirm Registration

Navigate back to the Falcon Console and check the Cloud accounts registration page.  You should see the IOM, IOA and 1Click services become Active soon. 


[Continue to Chapter 6](./chapter6.md)

[Back to Table of Contents](../README.md)