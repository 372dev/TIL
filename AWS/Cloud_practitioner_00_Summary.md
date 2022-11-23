# AWS Cloud practitioner 00 Summary

## Ultimate AWS Certified Cloud Practitioner by Stephane Maarek - study note summary

## 01 Cloud and Regions
* Characteristics and Beneifts of Cloud Computing
  * On-demand self service
  * Broad network access
  * Multi-tenancy and resource pooling
  * Rapid elasticity and scalability
  * Trade capital expense (CAPEX) for operational expense (OPEX) - Stop spending money running and maintaining data centers
  * Cost-Effectiveness(Economies of scale) and Measured service(Pay-as-you-go pricing)
  * Go global in minutes(leverage the AWS global infrastructure)
* Types of Cloud Computing
  * Infrastructure as a Service (IaaS)
    * Amazon EC2 (on AWS)
  * Platform as a Service (PaaS)
    * Elastic Beanstalk (on AWS)
  * Software as a Service (SaaS)
    * Many AWS services (Rekognition for Machine Learning etc.)
    * Google Apps (Gmail etc.), Dropbox, Zoom
* AWS has 3 pricing fundamentals: Compute, Storage, Data transfer OUT
* AWS Regions: A region is a cluster of data centers and most AWS services are region-scoped
* Regions > many availability zones > one or more data centers

## 02 IAM
* Users: mapped to a physical user, has a password for AWS Console
* Groups: contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: for EC2 instances or AWS services
* Security: MFA + Password Policy
* AWS CLI: manage your AWS services using the command-line
* AWS SDK: manage your AWS services using a programming language
* Access Keys: access AWS using the CLI or SDK
* Audit: IAM Credintial Reports & IAM Access Advisor

## 03 EC2
* EC2 Instance: AMI(OS) + Instance Size(CPU + RAM) + Storage + security groups + EC2 User Data
* Security Groups: Firewall attached to the EC2 instance
* EC2 User Data: Script launched at the first start of an instance
* SSH: start a terminal into our EC2 Instances (port 22)
* EC2 Instance Role: link to IAM roles
* Purchasing Options: On-Demand, Spot, Reserved(Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance, Capacity Reservation

## 04 EC2 Instance Storage
* EBS volumes:
  * network drives attached to one EC2 instance at a time
  * Mapped to an Availability Zones
  * Can use EBS Snapshots for backups / transferring EBS volumes across AZ
* AMI: create ready-to-use EC2 instances with our customizations
* EC2 Image Builder: automatically build, test and distribute AMIs
* EC2 Instance Store:
  * High perofrmance hardware disk attached to our EC2 instance
  * Lost if our instance is stopped / terminated
* EFS: network file system, can be attached to 100s of instances in a region
* EFS-IA: cost-optimized storage class for infrequent accessed files
* FSx for WIndows: Network FIle System for Windows servers
* FSx for Lustre: High Performance Computing Linux file system
