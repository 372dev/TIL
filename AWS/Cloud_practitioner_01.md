# AWS Cloud practitioner 01

## Ultimate AWS Certified Cloud Practitioner by Stephane Maarek - study note 01

### The Five Characteristics of Cloud Computing
* On-demand self service
  * Users can provision resources without a human interaction
* Broad network access
  * Resources can be accessed by diverse client platforms
* Multi-tenancy and resource pooling
  * Multiple customers share the same infrastructure
* Rapid elasticity and scalability
  * Automatically and quickly acquire and dispose resources when needed
* Measured service
  * pay-as-you-go pricing

### Six Advantages of Cloud Computing
* Trade capital expense (CAPEX) for operational expense (OPEX)
  * Pay On-demand; don't own a hardware
  * Reduced total cost of ownership (TCO) & operational expense (OPEX)
* Benefit from massive economies of scale
  * Prices are reduced as AWS is more efficient due to large scale
* Stop guessing capacity
  * Sacle based on actual measured usage
* Increase speed and agility
* Stop spending money running and maintaining data centers
* Go global in minutes; leverage the AWS global infrastructure

### Problems solved by the Cloud
* Flexibility: change resource types when needed
* Cost-Effectiveness: pay as you go, for what you use
* Scalability: accomodate larger loads by making hardware stronger or adding additional nodes
* Elasticity: ability to scale out and scale in when needed
* Agility: rapidly develop, test and launch software applications

### Types of Cloud Computing
* Infrastructure as a Service (IaaS)
  * Provides building blocks for cloud IT
  * Provides networking, computers, data storage space
  * Highest level of flexibility
  * Easy parallel with traditional on-permises IT
* Platform as a Service (PaaS)
  * Removes the need for your organization to manage the underlying infrastructure
  * Focus on the deployment and management of your application
* Software as a Service (SaaS)
  * Completed product that is run and managed by the service provider

### Examples of Cloud Computing Types
* IaaS
  * Amazon EC2 (on AWS)
  * GCP(Google cloud platform), Microsoft Azure, Rackspace, DIgital Ocean, Linode
* PaaS
  * Elastic Beanstalk (on AWS)
  * Heroku, Google App Engine (GCP), Windows Azure (MS)
* SaaS
  * Many AWS services (Rekognition for Machine Learning etc.)
  * Google Apps (Gmail etc.), Dropbox, Zoom

### Pricing of the Cloud, a Quick Overview
* AWS has 3 pricing fundamentals, following the pay-as-you-go pricing model
  * Compute : Pay for compute time
  * Storage : Pay for data stored in the Cloud
  * Data transfer OUT of the Cloud
    * Data transfer IN is free
* Solves the expensive issue of traditional IT

### AWS Regions
* AWS has Regions all around the world
* Names can be us-east-1, eu-west-3...
* A region is a cluster of data centers
* Most AWS services are region-scoped

### AWS Availability Zones
* Each region has many availability zones(usually 3, min is 2, max is 6). For example, Sydney; ap-southeast-2 has following AZs
  * ap-southeast-2a
  * ap-southeast-2b
  * ap-southeast-2c
* Each availability zone (AZ) is one or more discrete data centers with redundant power, networking, and connectivity

- Study note reference : [Ultimate AWS Certified Cloud Practitioner by Stephane Maarek](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/)
