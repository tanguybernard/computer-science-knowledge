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

An EBS snapshot is an __incremental backup__. Incremental backups back up only the changed data since the last backup activity — a full or incremental backup.

Full backups comprise entire data backup sets, regardless of already existing backups or data change circumstances.


When you launch ec2 Instance, an instance store is physically attached.

An instance store provides __temporary block-level__ storage for an Amazon EC2 instance.

When the instance is terminated, you lose any data in the instance store.

- Volumes do not automatically scales
- Need to be in same AZ to attach EC2 instances

An EBS volume must be located in the same Availability Zone as the Amazon EC2 instance to which it is attached.

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

![Which-S3-Storage-Class-is-right-for-me-Infograhic](https://github.com/tanguybernard/computer-science-knowledge/assets/14818169/16f75a03-7ad7-4a1a-b3a4-e663770b22a1)


source: https://www.pluralsight.com/resources/blog/cloud/s3-glacier-instant-retrieval-deep-dive-which-s3-storage-class-is-right-for-me

#### Amazon S3 Intelligent-Tiering storage class

Automates storage cost savings by moving data when access patterns change

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
- You can choose from expedited retrievals in 1-5 minutes, standard retrievals in 3-5 hours, and free bulk retrievals in 5-12 hours. 

https://aws.amazon.com/about-aws/whats-new/2021/11/amazon-s3-glacier-storage-class-amazon-s3-glacier-flexible-retrieval/?nc1=h_ls

#### S3 Glacier Deep Archive
- Lowest-cost object storage class ideal for archiving
- Able to retrieve objects within 12 hours; data retrieval from 12-48 hours.

#### S3 Outposts
– Creates S3 buckets on Amazon S3 Outposts
- Makes it easier to retrieve, store, and access data on AWS Outposts

Amazon S3 Outposts delivers object storage to your on-premises AWS Outposts environment.

### Notes

Amazon S3 Lifecycle management: Move data automatically between tiers

## Amazon Elastic File System (EFS)

Amazon Elastic File System (Amazon EFS) provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance. 

On-Premises Servers can use EFS through AWS Direct Connect or AWS VPN

- Multiple instances reading and wrinting simultaneous
- Linux file system
- Regional resource
- Automatically scales


### Configuration EC2 <> EFS

1. Create a security group
2.  Choose VPC that receive NFS files (EC2 instances are)
3.  Add Inbound Type NFS And Source : Security Group WebServers
4.  ...


### Amazon Relational Database Service (RDS)

Amazon RDS is a service that enables you to run relational databases in the AWS Cloud.

Amazon RDS is a managed service that automates tasks such as hardware provisioning, database setup, patching, and backups. 


Amazon RDS database engines:
- Amazon Aurora
- Mysql
- PostgresSQL
- Oracle
- Microsoft SQL Server
- And many more...

Characteristics :

- Automated patching
- Backups
- Redundancy
- Failover (basculement)
- Disaster recovery

Using multiple AZ's means : high availability and disaster recovery, not increased performance

Doing read-intensive workloads ? Solution : A read replica


#### Aurora

Amazon Aurora (Aurora) is a fully managed relational database engine that's compatible with MySQL and PostgreSQL.

Consider Amazon Aurora if your workloads require high availability. It replicates six copies of your data across three Availability Zones and continuously backs up your data to Amazon S3.

- MySQL
- Postgres
- Data Replication
- 1/10th the cost of commercial databases
- Up to 15 read replicas
- Continuous Backup to S3
- Point in time recovery

## DynamoDB

DynamoDB supports key/value and document data models.

DynamoDB is serverless, which means that you do not have to provision, patch, or manage servers. 

Scaling up to 10 trillion requests per day.

Can stores json-type documents.

__Read/Write Capacity Modes:__

__Provisioned capacity__ allows you to specify the number of read/write operations your application requires per second, ahead of time.
This mode is typically suitable for use cases with predictable traffic patterns or if an organization plans to increase traffic gradually.

__On Demand Capacity__, DynamoDB resources scale automatically when the workloads fluctuate.
As a pay-as-you-use model, on-demand capacity is typically suitable for applications with unpredictable traffic or unknown workloads. 


Feature: You can implement Trigger , which for example trigger AWS Lambda and Lambda can for example send notification in response !

Feature: PITR (Point-in-time-recovery) , provide Backup

## Amazon Redshift

Amazon Redshift is a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and helps you to understand relationships and trends across your data.

Power data driven decisions with the best price-performance cloud data warehouse.

## Amazon Database Migration Service (DMS)


AWS Database Migration Service (AWS DMS)(opens in a new tab) enables you to migrate relational databases, nonrelational databases, and other types of data stores.

Use cases

- Development and test database migrations: Enabling developers to test applications against production data without affecting production users
- Database consolidation: Combining several databases into a single database
- Continuous replication: Sending ongoing copies of your data to other target sources instead of doing a one-time migration


## AWS Application Migration Service (AWS MGN)

AWS MGN is an automated lift-and-shift solution. This solution can migrate physical servers and any databases or applications that run on them to EC2 instances in AWS.

## Additional Database Services

### Amazon DocumentDB

Amazon DocumentDBis a document database service that supports MongoDB workloads. 

(MongoDB is a document database program.)

### Amazon Neptune

Amazon Neptuneis a graph database service. 

### Amazon Managed Blockchain

Amazon Managed Blockchain is a service that you can use to create and manage blockchain networks with open-source frameworks. 
Blockchain is a distributed ledger system that lets multiple parties run transactions and share data without a central authority.

Example: A supply chain, that you have to track with assurances that nothing is lost.

### Amazon Quantum Ledger Database (Amazon QLDB)

Amazon QLDB is a ledger (FR: registre) database service. 

An immutable system of record where any entry can never be removed from the audits. 

You can use Amazon QLDB to review a complete history of all the changes that have been made to your application data.

### Amazon ElastiCache

Amazon ElastiCache is a service that adds caching layers on top of your databases to help improve the read times of common requests. 

It supports two types of data stores: Redis and Memcached.

### Amazon DynamoDB Accelerator (DAX)

DAX is an in-memory cache for DynamoDB. 

It helps improve response times from single-digit milliseconds to microseconds.


### Microsoft SQL Server

- Aurora ? No beacause only support mysql and postgres
- Ec2 And purchase license ? Yes you could.
- RDS ? Yes you could, but its a managed service, so it can cost more than ec2.
