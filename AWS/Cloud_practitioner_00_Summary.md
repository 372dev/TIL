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

## 02 IAM section
* Users: mapped to a physical user, has a password for AWS Console
* Groups: contains users only
* Policies: JSON document that outlines permissions for users or groups
* Roles: for EC2 instances or AWS services
* Security: MFA + Password Policy
* AWS CLI: manage your AWS services using the command-line
* AWS SDK: manage your AWS services using a programming language
* Access Keys: access AWS using the CLI or SDK
* Audit: IAM Credintial Reports & IAM Access Advisor

## 03
