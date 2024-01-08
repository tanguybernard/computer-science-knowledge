# Storage and Databases

## Amazon Elastic Block Store (EBS)

It's like a place to store files. It's like hardrive.

You can define Size, Type and configuration of EBS you want.

Designed for use with and Only Amazon EC2 Not Lambda.

Only one EBS on EC2 instance at the same time.

EBS Volume Types:
- SSD - Solid-State Drive
- HDD - Hard Disk Drive

Characteristics of the Amazon EBS service:
- Best for data that requires retention
- Separate drives from the host computer of an EC2 instance

Notes :

__EBS Snapshots__ : Les instantanés EBS sont une copie instantanée de vos données et peuvent être utilisés pour permettre la reprise après sinistre, migrer les données entre les régions et les comptes, et améliorer la conformité des sauvegardes.

An EBS snapshot is an incremental backup. Incremental backups back up only the changed data since the last backup activity — a full or incremental backup.

Full backups comprise entire data backup sets, regardless of already existing backups or data change circumstances.


When you launch ec2 Instance, an instance store is physically attached.

An instance store provides temporary block-level storage for an Amazon EC2 instance.

When the instance is terminated, you lose any data in the instance store.

## Amazon S3 - Amazon Simple Storage Service 

Store and retrieve unlimited amount of data.

- Store data as objects (like file sitting on your hard drive).
- Store objects in buckets (like file directory).
- Upload a maximum object size of 5 TB.
- Verison objects.
- Create multiple buckets.
- Create permissions.

A bucket is a container for objects. An object is a file and any metadata that describes that file. To store an object in Amazon S3, you create a bucket and then upload the object to the bucket.

In object storage, each object consists of data, metadata, and a key.

The data might be an image, video, text document, or any other type of file. Metadata contains information about what the data is, how it is used, the object size, and so on. An object’s key is its unique identifier.

File Example:  photos/puppy.jpeg

Main use: Storing large amounts of static data and ideal for data backups.

Can be used with EC2 or Lambda.

### Amazon S3 storage classes

Write Once, Read Many Technique.

#### Amazon S3 Standard
- Designed for frequently accessed data
- Stores data in a minimum of three Availability Zones

#### Amazon S3 static website hosting
#### Amazon S3 Standard-Infrequent Access (S3 Standard-IA)

Less frequently, long term storage like backup

Amazon S3 Standard-IA is ideal for data infrequently accessed but requires high availability when needed. 
 
#### S3 One Zone-Infrequent Access (S3 One Zone-IA)

Stores data in a single Availability Zone

#### S3 Glacier Instant Retrieval

- Works well for archived data that requires immediate access
- Can retrieve objects within a few milliseconds
- 
#### Amazon S3 Glacier Flexible Retrieval
- Low-cost storage designed for data archiving
- Able to retrieve objects within a few minutes to hours

#### S3 Glacier Deep Archive
- Lowest-cost object storage class ideal for archiving
- Able to retrieve objects within 12 hours

#### S3 Outposts
– Creates S3 buckets on Amazon S3 Outposts
- Makes it easier to retrieve, store, and access data on AWS Outposts

Amazon S3 Outposts delivers object storage to your on-premises AWS Outposts environment.

### Notes

Amazon S3 Lifecycle management: Move data automatically between tiers

## Amazon Elastic File System (EFS)

Amazon Elastic File System (Amazon EFS) provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance. 

On-Premises Servers can use EFS through AWS Direct Connect or AWS VPN


### Configuration EC2 <> EFS

1. Create a security group
2.  Choose VPC that receive NFS files (EC2 instances are)
3.  Add Inbound Type NFS And Source : Security Group WebServers
4.  ...

### Amazon Relational Database Service (RDS)

Using multiple AZ's means : high availability and disaster recovery, not increased performance

Doing read-intensive workloads ? Solution : A read replica


## DynamoDB

DynamoDB supports key/value and document data models.

__Read/Write Capacity Modes:__

__Provisioned capacity__ allows you to specify the number of read/write operations your application requires per second, ahead of time.
This mode is typically suitable for use cases with predictable traffic patterns or if an organization plans to increase traffic gradually.

__On Demand Capacity__, DynamoDB resources scale automatically when the workloads fluctuate.
As a pay-as-you-use model, on-demand capacity is typically suitable for applications with unpredictable traffic or unknown workloads. 


Feature: You can implement Trigger , which for example trigger AWS Lambda and Lambda can for example send notification in response !

Feature: PITR (Point-in-time-recovery) , provide Backup

## Amazon Redshift

Power data driven decisions with the best price-performance cloud data warehouse.
