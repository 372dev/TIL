# AWS Cloud practitioner 04

## Ultimate AWS Certified Cloud Practitioner by Stephane Maarek - study note 04

## Amazon EC2 - Instance Storage

### What's an EBS Volume?
* An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run
* It allows your instances to persist data, even afer their termination
* They can only be mounted to one instance at a time (at the CCP level)
* They are bound to a specific availability zone  

* Analogy: Think of them as a "network USB stick"
* Free tier: 30GB of free EBS storage of type General Purpose (SSD) or Magnetic per month

### EBS Volume
* It's a network drive (i.e. not a physical drive)
  * It uses the network to communicate the instance, which means there might be a bit of latency
  * It can be detached from an EC2 instance and attached to another one quickly

* It's locked to an Availability Zone(AZ)
  * An EBS Volume in us-east-1a cannot be attached to us-east-1b
  * To move a volume across, you first need to snapshot it

* Have a provisioned capacity (size in GBs, and IOPS)
  * You get billed for all the provisioned capacity
  * You can increase the capacity of the drive over time

### EBS - Delete on Termination attribute
* Controls the EBS behaviour when an EC2 instance terminates
  * By default, the root EBS volume is deleted (attribute enabled)
  * By default, any other attached EBS volume is not deleted (attribute disabled)
* This can be controlled by the AWS console / AWS CLI
* Use case: preserve root volume when instance is terminated

### EBS Snapshots
* Make a backup (snapshot) of your EBS volume at a point in time
* Not necessary to detach volume to do snapshot, but recommended
* Can copy snapshots across AZ or Region

* EBS Snapshot Archive
  * Move a Snapshot to an "archive tier" that is 75% cheaper
  * Takes within 24 to 72 hours for restoring the archive  

* Recycle Bin for EBS Snapshots
  * Setup rules to retain deleted snapshots so you can recover them after an accidental deletion
  * Specify retention (from 1 day to 1 year)

### AMI Overview
* AMI = Amazon Machine Image
* AMI is a customization of an EC2 Instance
  * You add your own software, configuration, operating system, monitoring
  * Faster boot / configuration time because all your software is pre-packaged
* AMI is built for a specific region (and can be copied across regions)
* You can launch EC2 instances from:
  * A Public AMI: AWS provided
  * Your own AMI: you make and maintain them yourself
  * An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

### AMI Process (from an EC2 Instance)
* Start an EC2 instance and customize it
* Stop the instance (for data integrity)
* Build an AMI - this will also create EBS snapshots
* Launch instances from other AMIs

### EC2 Image Builder
* Used to automate the creation of Virtual Machines or container images
* Automate the creation, maintain, validate and test EC2 AMIs
* Can be run on a schedule (weekly, whenever packages are updated, etc...)
* Free service (only pay for the underlying resources)

### EC2 Instance Store
* EBS volumes are network drives with good but "limited" performance
* If you need a high-performance hardware disk, use EC2 Instance Store
* Better I/O performance
* EC2 Instance Store lose their storage if they're stopped (ephemeral)
* Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails

### EFS - Elastic File System
* Managed NFS (network file system) that can be mounted on 100s of EC2
* EFS works with Linux EC2 instances in multi-AZ
* Highly available, scalable, expensive (3X gp2), pay per use, no capacity planning

### EBS vs EFS
* EBS you make a snapshot of EBS from one AZ and restore the snapshot at another AZ
* EFS you can have many Instances in many AZs to share EFS through EFS Mount Target

### EFS Infrequent Access (EFS-IA)
* Storage class that is cost-optimized for files not accessed every day
* Up to 92% lower cost compared to EFS Standard
* EFS will automatically move your files to EFS-IA
* Enable EFS-IA with a Lifecycle Policy
* Example: move files that are not accessed for 60 days to EFS-IA
* Transparent to the applications accessing EFS

### Shared Responsibility Model for EC2 Storage
* AWS
  * Infrastructure
  * Replication for data for EBS volumes & EFS drives
  * Replacing faulty hardware
  * Ensuring their employees cannot access your data
* User
  * Setting up backup / snapshot procedures
  * Setting up data encryption
  * Responsibility of any data on the drives
  * Understanding the risk of using EC2 Instance Store

### Amazon FSx - Overview
* Launch 3rd party high-performance file system on AWS
* Fully managed service
* Options:
  * FSx for WIndows File Server
  * FSx for Lustre
  * FSx for NetApp ONTAP

### Amazon FSx for WIndows File Server
* A Fully managed, highly reliable, and scalable Windows native shared file system
* Built on WIndows File Server
* Supports SMB protocol & Windows NTFS
* Integrated with Microsoft Active Directory
* Can be accessed from AWS or your on-permise infrastructure

### Amazon FSx for Lustre
* A fully managed, high-performance, scalable file storage for High Performance Computing (HPC)
* The name Lustre is derived form "Linux" and "cluster"
* Machine Learning, Analystics, Video Processing, Financial Modeling, ...
* Scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## EC2 Instance Storage - Summary
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


- Study note references
  - Udemy course [Ultimate AWS Certified Cloud Practitioner](https://www.udemy.com/course/aws-certified-cloud-practitioner-new/) by Stephane Maarek
