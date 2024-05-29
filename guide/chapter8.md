Cloud Security Lab Series
# AWS CSPM Registration 101
## Chapter 8 - Multiple Account Registration

While Org registration is the most convenient way to onboard AWS Accounts, there are cases when the the customer requires that not all accounts are registered to the CID, or that accounts within an AWS organization will be registered to multiple CIDs.  In those cases the appropriate solution is Multiple Account registration.

Multiple Account registration is a method to execute account registration against a list of account IDs defined in a CSV.  Consider the following scenario:

### Multiple CID Scenario

Customer's AWS Org
- OU A
- - Account 1
- - Account 2
- OU B
- - Account 3
- - Account 4

Customer procures two Falcon CIDs and wants the following registration approach:
- Accounts in OU A registered to CID A
- Accounts in OU B registered to CID B

In this scenario the customer **cannot** use the Organization registration covered in chapter 6.  They must register these accounts as single accounts to ensure they can be registered to different CIDs despite existing in a shared AWS Organization.

Single account registration can be time consuming, especially when customers have many accounts.  This is where Multiple Account registration should be used.  The customer will follow the folllowing process:

1. Login to CID A
2. Navigate to Cloud Accounts Registration
3. Add new account and choose Multiple Accounts option
4. List account IDs from OU A in CSV file
5. Download bash or terraform and execute registration with your CSV
6. Login to CID B
7. Navigate to Cloud Accounts Registration
8. Add new account and choose Multiple Accounts option
9. List account IDs from OU B in CSV file
10. Download bash or terraform and execute registration with your CSV


[Continue to Chapter 9](./chapter9.md)

[Back to Table of Contents](../README.md)