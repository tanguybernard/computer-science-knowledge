# Storage and Databases


## Amazon S3 - Amazon Simple Storage Service 

A bucket is a container for objects. An object is a file and any metadata that describes that file. To store an object in Amazon S3, you create a bucket and then upload the object to the bucket.

File Example:  photos/puppy.jpeg

Main use: Storing large amounts of static data and ideal for data backups.

Can be used with EC2 or Lambda



## Amazon Elastic File System (EFS)

Amazon Elastic File System (Amazon EFS) provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance. 

On-Premises Servers can use EFS through AWS Direct Connect or AWS VPN


### Configuration EC2 <> EFS

1. Create a security group
2.  Choose VPC that receive NFS files (EC2 instances are)
3.  Add Inbound Type NFS And Source : Security Group WebServers
4.  ...

## Amazon Elastic Block Store (EBS)

Designed for use with and Only Amazon EC2 Not Lambda.

Only one EBS on EC2 instance at the same time

EBS Volume Types:
- SSD - Solid-State Drive
- HDD - Hard Disk Drive

Notes :

__EBS Snapshots__ : Les instantanés EBS sont une copie instantanée de vos données et peuvent être utilisés pour permettre la reprise après sinistre, migrer les données entre les régions et les comptes, et améliorer la conformité des sauvegardes.

## DynamoDB

DynamoDB supports key/value and document data models.

__Read/Write Capacity Modes:__

__Provisioned capacity__ allows you to specify the number of read/write operations your application requires per second, ahead of time.
This mode is typically suitable for use cases with predictable traffic patterns or if an organization plans to increase traffic gradually.

__On Demand Capacity__, DynamoDB resources scale automatically when the workloads fluctuate.
As a pay-as-you-use model, on-demand capacity is typically suitable for applications with unpredictable traffic or unknown workloads. 


Feature: You can implement Trigger , which for example trigger AWS Lambda and Lambda can for example send notification in response !

Feature: PITR (Point-in-time-recovery) , provide Backup
