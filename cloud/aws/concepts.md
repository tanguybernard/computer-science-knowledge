# Notes


## Cloud Concepts

https://coderjony.com/blogs/cloud-computing-concepts-high-availability-scalability-elasticity-agility-fault-tolerance-and-disaster-recovery

## AWS General Info

AWS 22 Regions (Separate Geographic area), and inside there are multiple Availability Zones (AZ), at least 2 per region. Each AZ is fully isolated.

Each AZ have one or more physical data centers.

AZ : Logical Data center

Partition: A partition is a grouping of Regions. 

## Amazon S3 - Amazon Simple Storage Service 

A bucket is a container for objects. An object is a file and any metadata that describes that file. To store an object in Amazon S3, you create a bucket and then upload the object to the bucket.

File Example:  photos/puppy.jpeg

Main use: Storing large amounts of static data and ideal for data backups.

## Amazon EC2 - Amazon Elastic Compute Cloud

Instance -> Virtual Server

There are different types of instance (ex: t2) and different size.

AMI : Amazon Machine Image = Information To Launch one or many instances.

AMI is composed of: OS, Applications and App Server

EC2 Storage Possibility:
- EBS (Persistant)
- EFS
- Instant Storre (Temporary)

How To Connect ?

- EC2 Instant Connect
- Session Manager (a capability of AWS Systems Manager)
- ssh client

## Amazon Elastic File System (EFS)

## Amazon Elastic Block Store (EBS)

Designed for use with Amazon EC2.

Only once EBS on EC2 instance at the same time

EBS Volume Types:
- SSD - Solid-State Drive
- HDD - Hard Disk Drive

## AWS Systems Manager

## AWS Migration strategy

A migration strategy is the approach used to migrate a workload into the AWS Cloud. There are seven migration strategies for moving applications to the cloud, known as the 7 Rs:

- Retire
- Retain
- Rehost
- Relocate
- Repurchase
- Replatform
- Refactor or re-architect

https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-guide/migration-strategies.html

## AWS VPC
