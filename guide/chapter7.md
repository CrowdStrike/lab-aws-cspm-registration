Cloud Security Lab Series
# AWS CSPM Registration 101
## Chapter 7 - Organization Registration

Now that we understand how CSPM works, let's consider how this process changes in an AWS Organization context.

The core functionality requires the same resources to enable IOM, IOA and Sensor Management regardless of deployment method.  An API call is made against the /cloud-connect-cspm-aws/entities/account/v1 endpoint (via bash or terraform provider), the response contains role names, external id and eventbus target unique to that registration event, and those attributes are configured in the resources in the customers account. 

However when onboarding an entire org, the reader role has a new purpose and there are additional resources created to deploy and configure our core resources in every account of the org.  

### The Reader Role

The readonly role to enable IOMs has permissions to make the `organizations:List*` call which enables the role to list the account Ids in an organization.  When you register an organization with any method, this role is created in the AWS Organziations Management account.  CrowdStrike uses this role in the management account to list all account ids and automatically register them.  This is why after performing an org registration you will very quickly see all account ids in the org show up in the Cloud Accounts registration page in Falcon, even if they are inactive.  They have been *registered* but not *onboarded*.  At this point they are all registered to your CID and cannot be registered to a different CID.

### StackSets

Whether using the Bash method or Terraform, CloudFormation Stacks and StackSets are created to onboard every child account and ensure new accounts are automatically onboarded upon creation.

|Type|Name|Purpose|Regions|
|---|---|---|---|
|Stack|CrowdStrike-CSPM-Integration|Create IAM Roles and Sensor Management resources in Root Account|Single Region - Current Context|
|Stackset|CrowdStrike-CSPM-Integration|Create IAM Roles and Sensor Management resources in child accounts|Single Region - Current Context|
|Stackset|CrowdStrike-CSPM-Integration-Root-EB|Create EventBridge Rules in Root Account|Multi Region - All enabled regions|
|Stackset|CrowdStrike-CSPM-Integration-EB|Create EventBridge Rules in child accounts|Multi Region - All enabled regions|

**Note**: The multi-region stacksets will deploy stack instances to every enabled region per AWS Organizations settings.  It has no way of assessing whether regions are enabled via SCP or STS.  A future chapter will cover how to handle these scenarios.

### External ID

One of the benefits of Org registration is you are only making the registration API call once.  This means there is only one reader role name, only one external id and only one eventbus target ARN for many accounts.  This allows us to easily register child accounts by passing the same values to the CloudFormation templates against every account.

### A note on troubleshooting StackSets

It is important to understand what a stackset is to easily troubleshoot it in the event of a failure.  StackSets deploy Cloudformation templates against other regions and/or child accounts.  Within the target region or account there is a typical CloudFormation stack deployed, just as though you were to Create Stack within that account.

This is important to understand to aid in troubleshooting.  Let's say you run the Bash and it fails with a vague error message or succeeds but everything still shows inactive in the Falcon console.  You do not need to rely on the bash output to troubleshoot.  Log into the Org Management account and review the following items:

- Management Account
- - CrowdStrike-CSPM-Integration Stack
- - - Events
- - CrowdStrike-CSPM-Integration Stackset (or any other stackset for that matter)
- - - Stack Instances
- - - - Status Reason for each Region/Account
- - Switch role into an Account that failed in the Stackset
- - - CrowdStrike-CSPM-Integration Stack
- - - - Events

You will get much more context by looking at the events in each stack!

### A note on CIDs

When you register the AWS organization, every AWS Account in the org is registered to the CID.  If you need to register accounts within the same AWS Organization to multiple CIDs, please review the Multiple Account method in the next chapter.

[Continue to Chapter 8](./chapter8.md)

[Back to Table of Contents](../README.md)
