# AWS Cloud practitioner 02 IAM

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
  * Id: an identifier for the policy (optional)
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

### One-Time Password (OTP)?
*  is an automatically generated password for a single transaction or session

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
* It's an open-source(https://github.com/aws/aws-cli)
* Alternative to using AWS Management Console

### What's the AWS SDK?
* AWS Software Development Kit (AWS SDK)
* Language-specific APIs(set of libraries)
* Enables you to access and manage AWS services programmatically
* Embedded within your application
* Supports
  * SDKs (JavaScript, Python, PHP, .NET, Ruby, Java, Go, Node.js, C++)
  * Mobile SDKs (Android, iOS)
  * IoT Devices SDKs(Embedded C, Arduino)
* Example: AWS CLI is built on AWS SDK for Python

### What's the AWS CLI?
* With the AWS Command Line Interface, you can manage your multiple AWS services from the command line and automate them through scripts.
* Usage
  * >aws help
  * >aws --version
  * >aws configure
  * >aws iam list-users
  * >aws ec2 describe-instances
  * >aws ec2 start-instances --instance-ids i-1348636c

### What's the AWS CloudShell?
* AWS CloudShell is a browser-based shell that makes it easy to securely manage, explore, and interact with your AWS resources. CloudShell is pre-authenticated with your console credentials.
* Benefits
  * No extra credentials to manage; CloudShell inherits the credentials of the user signed in to the Console.
  * Automatically updated; Fully managed Amazon Linux 2 environment that has the recent versions of popular tools already installed and updated.
  * No cost; It includes 1 GB of persistent storage per Region at no extra cost to you.
  * Customizable; With 1GB of storage per Region, you can store scripts, files, configuration preferences, and additional tools in your home directory.

### IAM Roles for Services
* Some AWS service will need to perform actions on your behalf
* To do so, we will assign permissions to AWS services with IAM Roles
* Common roles
  * EC2 Instance Roles
  * Lambda Function Roles
  * Roles for CloudFormation

### IAM Security Tools
* IAM Credentials Report (account-level)
  * a report that lists all your account's users and the status of their various credentials

* IAM Access Advisor (user-level)
  * Access advisor shows the service permissions granted to a user when those services were last accessed
  * You can use this information to revise your policies

### IAM Guidelines & Best Practices
* Don't use the root account except for AWS account setup
* One physical user = One AWS user
* Assign users to groups and assign permissions to groups
* Create a strong password policy
* Use and enforce the use of Multi Factor Authentication (MFA)
* Create and use Roles for giving permissions to AWS services
* Use Access Keys for Programmatic Access (CLI/SDK)
* Audit permissions of your account with the IAM Credentials Report
* Never share IAM users & Access Keys

### Shared Responsibility Model for IAM
* AWS
  * Infrastructure (global network security)
  * Configuration and vulnerability analysis
  * Compliance validation
* Customer
  * Users, Groups, Roles, Policies management and monitoring
  * Enable MFA on all accounts
  * Rotate all your keys often
  * Use IAM tools to apply appropriate permissions
  * Analyze access patterns & review permissions

## IAM section - Summary
* Users: mapped to a physical user, has a password for AWS Console
* Groups: contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: for EC2 instances or AWS services
* Security: MFA + Password Policy
* AWS CLI: manage your AWS services using the command-line
* AWS SDK: manage your AWS services using a programming language
* Access Keys: access AWS using the CLI or SDK
* Audit: IAM Credintial Reports & IAM Access Advisor

- Study note references
  - Udemy course [Ultimate AWS Certified Cloud Practitioner](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/) by Stephane Maarek
  - [AWS] (https://aws.amazon.com/)
