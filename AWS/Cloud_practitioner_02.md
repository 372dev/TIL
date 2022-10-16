# AWS Cloud practitioner 02

## Ultimate AWS Certified Cloud Practitioner by Stephane Maarek - study note 02

## IAM : Identity and Access Management, Global service
* Root account created by default, shouldn't be used or shared
* Users are people within your organization, and can be grouped
* Groups only contain users, not other groups
* Users don't have to belong to a group, and user can belong to multiple groups

### Permissions
* Users or Groups can be assigned JSON documents called policies
* These policies define the permissions of the users
* In AWS you apply the least privilege principle; don't give more permissions than a user need

### Policies inheritance
* Policies are inherited to all the members of the group that the policies are assigned to
* A users can inherit multiple policies if the user is in multiple groups
* If the user is not in any group, the user can assigned policies with something called inline policy

### Policies structure
* Consists of
  * Version: policy language version, always include "2012-10-17" or an older version "2008-10-17" which lacks some of the newer features.
  * Id: an identifier for the policy (optiional)
  * Statement: one or more individual statements (required)
* Statements consists of
  * Sid: an identifier for the statement (optional)
  * Effect: whether the statement allows or denies access (Allow, Deny)
  * Principal: account/user/role to which this policy applied to
  * Action: list of actions this policy allows or denies
  * Resource: list of resources to which the actions applied to
  * Condition: conditions for when this policy is in effect (optional)

### MFA : Multi Factor Authentication
* Users have access to your account and can possibly change configurations or delete resources in your AWS account
* You want to protect your Root Accounts and IAM users
* MFA = password you know + security device you own
* Main benefit of MFA: if a password is stolen or hacked,  the account is not compromised

### MFA devices options in AWS
* Virtual MFA device
  * Google Authenticator (phone only)
  * Authy (multi-device)
* Universal 2nd Factor (U2F) Security Key
* Hardware Key Fob MFA Device
  * Gemalto (3rd party)
  * SurePassID (3rd party - for AWS GovCloud US)

### How can users access AWS?
* The three ways to access AWS
  * AWS Management Console (protected by password + MFA)
  * AWS Command Line Interface (CLI): protectedy by access keys
  * AWS Software Developer Kit (SDK): for code, protected by access keys
* Access keys are generated through the AWS Console
* Users manage their own access keys
* Access keys are secret, just like a password. Don't share them
  * Access key ID ~= username
  * Secret access key ~= password

### What's the AWS CLI?
* A tool that enables you to interact with AWS services using commands in you command-line shell
* Direct access to the public APIs of AWS services
* You can develop scripts to manage your resources
* It's open-source https://github.com/aws/aws-cli
* Alternative to using AWS Management Console


- Study note reference : Udemy course [Ultimate AWS Certified Cloud Practitioner](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/) by Stephane Maarek
