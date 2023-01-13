# AWS Cloud practitioner 06

## Ultimate AWS Certified Cloud Practitioner by Stephane Maarek - study note 06

## Amazon S3

### Section introduction
* Amazon S3 is one of the main building blocks of AWS
* It's advertised as "infinitely scaling" storage
* Many websites use Amazon S3 as a backbone
* Many AWS services use Amazon S3 as an integration(meaning to stitch subsystems together to work as one) as well

### Amazon S3 Use cases
* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application hosting
* Media hosting
* Data lakes & big data analytics
* Software delivery
* Static website

### Amazon S3 - Buckets
* Amazon S3 allows people to store objects (files) in "buckets" (directories)
* Buckets must have a globally unique name (across all regions all accounts)
* Buckets are defined at the region level
* S3 looks like a global service but buckets are created in a region
* Naming convention
  * No uppercase, No underscore
  * 3-63 characters long
  * Not an IP
  * Must start with lowercase letter or number
  * Must NOT start with the prefix xn--
  * Must NOT end with the suffix -s3alias

### Amazon S3 - Objects
* Objects (files) hava a key
* The "key" is the FULL path
  * s3://my-backet/"my_file.txt"
  * s3://my-bucket/"my_folder1/another_folder/my_file.txt"
* The key is composed of "prefix" + "object name"
  * s3://my-bucket/"my_folder1/another_folder/"+"my_file.txt"
* There's no real concept of directories within buckets (although the UI will trick you to think otherwise)
* Just keys with very long names that contain slashes ("/")
* Object values are the content of the body:
  * Max. Object Size is 5TB (5000GB)
  * If uploading more than 5GB, must use "multi-part upload"
* Metadata (list of text key / value pairs - system or user metadata)
* Tags (Unicode key / value pair - up to 10) - useful for security / lifecycle
* Version ID (if versioning is enabled)

### Amazon S3 - Security
* User-Based
  * IAM Policies - which API calls should be allowed for a specific user from IAM
* Resource-Based
  * Bucket Policies - bucket wide rules from the S3 console - allows cross account
  * Object Access Control List (ACL) - finer grain (can be disabled)
  * Bucket Access Control List (ACL) - less common (can be disabled)
* Note: an IAM Principal can access an S3 object if
  * The user IAM permissions ALLOW it OR the resource policy ALLOWS it
  * AND there's no explicit DENY
* Encryption: encrypt object in Amazon S3 using encryption keys

### S3 Bucket Policies
* JSON based policies
  * Resources: buckets and objects
  * Effect: Allow / Deny
  * Actions: Set of API to Allow or Deny
  * Principal: The account or user to apply the policy to
* Use S3 bucket for policy to:
  * Grant public access to the bucket
  * Force objects to be encrypted at upload
  * Grant access to another account (Cross Account)

### Examples:
* Public Access - Use Bucket Policy
  * Anonymous www website visitor --> S3 bucket with S3 Bucket Policy that Allows Public Access
* User Access to S3 - IAM permissions
  * IAM User with IAM Policy --> S3 Bucket
* EC2 instance access - Use IAM Roles
  * EC2 Instance with EC2 Instance Role that has IAM permissions --> S3 Bucket
* (Adanced) Cross-Account Access - Use Bucket Policy
  * IAM User from Other AWS account --> S3 Bucket with S3 Bucket Policy that Allows Cross-Account

### Bucket setting for Block Public Access
* Block all public access (On / Off)
* These settings were created to prevent company data leaks
* If you know your bucket should never be public, leave these on
* Can be set at the account level

### Amazon S3 - Static Website Hosting
* S3 can host static websites and have them accessible on the Internet
* The website URL will be (depending on the region)
  * http://bucket-name.s3-website-aws-region.amazonaws.com OR
  * http://bucket-name.s3-website.aws-region.amazonaws.com
* If you get a 403 Forbidden error, make sure the bucket policy allows public reads

### Amazon S3 - Versioning
* You can version your file in Amazon S3
* It is enabled at the bucket level
* Same key overwrite will change the "version": 1,2,3,...
* It is best practice to version your buckets
  * Protect against unintended deletes (ability to restore a version)
  * Easy roll back to previous version
* Notes:
  * Any file that is not versioned prior to enabling versioning will have version "null"
  * Suspending versioning does not delete the previous versions

### Amazon S3 - Replication (CRR & SRR)
* Must enable Versioning in source and destination buckets
* Cross-Region Replication (CRR)
* Same-Region Replication (SRR)
* Buckets can be in different AWS accounts
* Copying is asynchronous
* Must give proper IAM permissions to S3
* Use cases:
  * CRR - compliance, lower latency access, replication across accounts
  * SRR - log aggregation, live replication between production and test accounts

### S3 Storage Classes
* Amazon S3 Standard - General Purpose
* Amazon S3 Standard-Infrequent Access (IA)
* Amazon S3 One Zone-Infrequent Access
* Amazon S3 Glacier Instant Retrieval
* Amazon S3 Glacier Flexible Retrieval
* Amazon S3 Glacier Deep Archive
* Amazon S3 Intelligent Tiering
* Can move between classes manually or using S3 Lifecycle configurations

### S3 Durability and Availability
* Durability:
  * High durability (99.999999999%, 11 9's) of objects across multiple AZ
  * If you store 10,000,000 objects with Amazon S3, you can on average expect to incur a loss of a single object once every 10,000 years
  * Same for all storage classes
* Availability:
  * Measures how readily available a service is
  * Varies depending on storage class
  * Example: S3 standard has 99.99% availability = not available 53 minutes a year

### S3 Standard - General Purpose
* 99.99% Availability
* Used for frequently accessed data
* Low latency and high throughput
* Sustain 2 concurrent facility failures
* Use Cases: Big Data analytics, mobile & gaming applications, content distribution...

### S3 Storage Classes - Infrequent Access
* For data that is less frequently accessed, but requires rapid access when needed
* Lower cost than S3 Standard
* Amazon S3 Standard-Infrequent Access (S3 Standard-IA)
  * 99.9% Availability
  * Use cases: Disaster Recovery, backups
* Amazon S3 One Zone-Infrequent Access (S3 One Zone-IA)
  * High durability (99.999999999%) in a single AZ; data lost when AZ is destroyed
  * 99.5% Availability
  * Use cases: Storing secondary backup copies of on-premise data, or data you can recreate

### Amazon S3 Glacier Storage Classes
* Low-cost object storage meant for archiving / backup
* Pricing: price for storage + object retrieval cost
* Amazon S3 Glacier Instant Retrieval
  * Millisecond retrieval, great for data accessed once a quarter
  * Minimum storage duration of 90 days
* Amazon S3 Glacier Flexible Retrieval (formerly Amazon S3 Glacier)
  * Expedited (1 to 5 minutes), Standard(3 to 5 hours), Bulk(5 to 12 hours) - free
  * Minimum storage duration of 90 days
* Amazon S3 Glacier Deep Archive - for long term storage
  * Standard (12 hours), Bulk (48 hours)
  * Minimum storage duration of 180 days

### S3 Intelligent-Tiering
* Small monthly monitoring and auto-tiering fee
* Moves objects automatically between Access Tiers based on usage
* There are no retrieval charges in S3 Intelligent-Tiering
  * Frequent Access tier (automatic): defult tier
  * Infrequent Access tier (automatic): object not accessed for 30 days
  * Archive Instant Access tier (automatic): object not accessed for 90 days
  * Archive Access tier (optional): configurable from 90 days to 700+ days
  * Deep Archive Access tier (optional): configurable from 90 days to 700+ days

### S3 Encryption
* No Encryption
* Server-Side Encryption : User uploads a file and Server encrypts the file after receiving it
* Client-Side Encryption : User encrypts a file before uploading it

### Shared Responsibility Model for S3
* AWS
  * Infrastructure (global security, durability, availability, sustain concurrent loss of data in two facilities)
  * Configuartion and vulnerability analysis
  * Compliance validation
* Client
  * S3 Versioning
  * S3 Bucket Policies
  * S3 Replication Setup
  * Logging and Monitoring
  * S3 Storage Classes
  * Data encryption at rest and in transit

### AWS Snow Family
* Highly-secure, portable devices to collect and process data at the edge, and migrate data into and out of AWS
* Data migration: Snowcone, Snowball Edge, Snowmobile
* Edge computing: Snowcone, Snowball Edge

### Data Migrations with AWS Snow Family
* Challenges of migrations: (e.g. client to Amazon S3 bucket by www: 10Gbit/s)
  * Limited connectivity
  * Limited bandwidth
  * High network cost
  * Shared bandwidth (can't maximize the line)
  * Connection stability
* AWS Snow Family: offline devices to perform data migrations
  * If it takes more than a week to transfer over the network, use Snowball devices!

### Snowball Edge (for data transfers)
* Physical data transport solution: move TBs or PBs of data in or out of AWS
* Alternative to moving data over the network (and paying network fees)
* Pay per data transfer job
* Provide block storage and Amazon S3-compatible object storage
* Snowball Edge Storage Optimized
  * 80TB of HDD capacity for block volume and S3 compatible object storage
* Snowball Edge Compute Optimized
  * 42TB of HDD capacity for block volume and S3 compatible object storage
* Use cases: large data cloud migrations, DC decommission, disaster recovery

### AWS Snowcone
* Small, portable computing, anywhere, rugged & secure, withstands harsh environments
* Light (4.5 punds, 2.1 kg)
* Device used for edge computing, storage, and data transfer
* 8TB of usable storage
* Use Snowcone where snowball does not fit (space-constrained environment)
* Must provide your own battery / cables
* Can be sent back to AWS offline, or connect it to internet and use AWS DataSync to send data

### AWS Snowmobile
* Transfer exabytes of data (1EB = 1,000 PB = 1,000,000 TB)
* Each Snowmobile has 100 PB of capacity (use multible in parallel)
* High security: temperature controlled, GPS, 24/7 video surveillance
* Better than Snowball if you transfer more than 10 PB

### AWS Snow Family for Data Migrations
* Snowcone
  * Storage Capacity : 8TB usable
  * Migration Size : Up to 24TB, online and offline
  * DataSync agent Pre-installed
* Snowball Edge
  * Storage Capacity : 80TB usable
  * Migration Size : Up to petabytes, offline
* Snowmobile
  * Storage Capacity : < 100PB
  * Migration Size : Up to exabytes, offline
  * Storage Clustering Up to 15 nodes

### Snow Family - Usage Process
1. Request Snowball devices from the AWS console for delivery
2. Install the snowball client / AWS OpsHub on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you're done (goes to the right AWS facility)
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped


### What is Edge Computing?
* Process data while it's being created on an edge location
  * A truck on the road, a ship on the sea, a mining station underground...
* These locations may have
  * Limited / no internet access
  * Limited / no easy access to computing power
* We setup a Snowball Edge / Snowcone devices to do edge computing
* Use cases of Edge Computing
  * Preprocess data
  * Machine learning at the edge
  * Transcoding media streams
* Eventually (if need be) we can ship back the device to AWS (for transferring data for example)

### Snow Family - Edge Computing
* Snowcone (smaller)
  * 2 CPUs, 4GB of memory, wired or wireless access
  * USB-C power using a cord or the optional battery
* Snowball Edge - Computing Optimized
  * 52 vCPUs, 208 GB of RAM
  * Optional GPU (useful for video processing or machine learning)
* All: Can run EC2 Instances & AWS Lambda functions (using AWS IoT Greengrass)
* Long-term deployment options: 1 and 3 years discounted pricing

### AWS OpsHub
* Historically, to use Snow Family devices, you needed a CLI (Command LIne Interface tool)
* Today, you can use AWS OpsHub (a software you install on your computer / laptop) to manage your Snow Family Device
  * Unlocking and configuring single or clustered devices
  * Transferring files
  * Launching and managing instances running on Snow Family Devices
  * Monitor device metrics (storage capacity, active instances on your device)
  * Launch compatible AWS services on your devices (i.e. Amazon EC2 instances, AWS DataSync, Network File System)

### Hybrid Cloud for Storage
* AWS is pushing for "hybrid cloud"
  * Part of your infrastructure is on-premises
  * Part of your infrastructure is on the cloud
* This can be due to
  * Long cloud migrations
  * Security requirements
  * Compliance requirements
  * IT strategy
* S3 is a proprietary(meaning private) storage technology (unlike EFS/NFS), so how do you expose the S3 on-premise?
  * AWS Storage Gateway!

### AWS Storage Cloud Native Options
* BLOCK
  * Amazon EBS
  * EC2 Instance Store
* FILE
  * Amazon EFS
* OBJECT
  * Amazon S3
  * Glacier

### AWS Storage Gateway
* Bridge between on-premise data and cloud data in S3
* Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud
* Use cases: disaster recovery, backup & restore, tiered storage
* Types of Storage Gateway
  * File Gateway
  * Volume Gateway
  * Tape Gateway
* No need to know the types at the exam

### Amazon S3 - Summary
* Buckets vs Objects: global unique name, tied to a region
* S3 security: IAM policy, S3 Bucket Policy (public access), S3 Encryption
* S3 Websites: host a static website on Amazon S3
* S3 Versioning: multiple versions for files, prevent accidental deletes
* S3 Replication: same-region or cross-region, must enable versioning
* S3 Storage Classes: Standard, IA, OZ-IA, Intelligent Tiering, Glacier (Instant, Flexible, Deep)
* Snow Family: import data onto S3 through a physical device, edge computing
* OpsHub: desktop application to manage Snow Family devices
* Storage Gateway: hybrid solution to extend on-premises storage to S3

- Study note references
  - Udemy course [Ultimate AWS Certified Cloud Practitioner](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/) by Stephane Maarek
