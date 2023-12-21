# Notes


## Cloud Concepts

https://coderjony.com/blogs/cloud-computing-concepts-high-availability-scalability-elasticity-agility-fault-tolerance-and-disaster-recovery

## AWS General Info

AWS 22 Regions (Separate Geographic area), and inside there are multiple Availability Zones (AZ), at least 2 per region. Each AZ is fully isolated.

Each AZ have one or more physical data centers.

AZ : Logical Data center

Partition: A partition is a grouping of Regions. 

## AWS Migration strategy (approach)

A migration strategy is the approach used to migrate a workload into the AWS Cloud. There are seven migration strategies for moving applications to the cloud, known as the 7 Rs:

- Retire
- Retain
- Rehost
- Relocate
- Repurchase
- Replatform
- Refactor or re-architect

https://docs.aws.amazon.com/prescriptive-guidance/latest/large-migration-guide/migration-strategies.html

## AWS Services

### Storage

#### Amazon S3 - Amazon Simple Storage Service 

A bucket is a container for objects. An object is a file and any metadata that describes that file. To store an object in Amazon S3, you create a bucket and then upload the object to the bucket.

File Example:  photos/puppy.jpeg

Main use: Storing large amounts of static data and ideal for data backups.

Can be used with EC2 or Lambda

#### Amazon Elastic File System (EFS)

Amazon Elastic File System (Amazon EFS) provides serverless, fully elastic file storage so that you can share file data without provisioning or managing storage capacity and performance. 

On-Premises Servers can use EFS through AWS Direct Connect or AWS VPN


##### Configuration EC2 <> EFS

1. Create a security group
2.  Choose VPC that receive NFS files (EC2 instances are)
3.  Add Inbound Type NFS And Source : Security Group WebServers
4.  ...

#### Amazon Elastic Block Store (EBS)

Designed for use with and Only Amazon EC2 Not Lambda.

Only one EBS on EC2 instance at the same time

EBS Volume Types:
- SSD - Solid-State Drive
- HDD - Hard Disk Drive

Notes :

__EBS Snapshots__ : Les instantanés EBS sont une copie instantanée de vos données et peuvent être utilisés pour permettre la reprise après sinistre, migrer les données entre les régions et les comptes, et améliorer la conformité des sauvegardes.

### DynamoDB

DynamoDB supports key/value and document data models.

Read/Write Capacity Mode
- Provisioned (Set capacity Read and write)
- On Demand

Feature: You can implement Trigger , which for example trigger AWS Lambda and Lambda can for example send notification in response !

Feature: PITR (Point-in-time-recovery) , provide Backup

### Amazon EC2 - Amazon Elastic Compute Cloud

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


Burstable

Traditional Amazon EC2 instance types provide fixed CPU resources, while burstable performance instances provide a baseline level of CPU utilization with the ability to burst CPU utilization above the baseline level. 


### AWS Systems Manager

AWS Systems Manager provides configuration management, which helps you maintain consistent configuration of your Amazon EC2 or on-premises instances. With Systems Manager, you can control configuration details such as server configurations, anti-virus definitions, firewall settings, and more.



### AWS VPC

Control Virtual Network Environment (Ip Adress range, subnets, route tables, Network Gateways)

A __subnet__ is a range of IP addresses in your VPC. You can create AWS resources, such as EC2 instances, in specific subnets.

#### Internet Gateway vs NAT Gateway

- Internet Gateway (IGW) allows instances with public IPs to access the internet.
- NAT Gateway (NGW) allows instances with no public IPs to access the internet.

https://medium.com/awesome-cloud/aws-vpc-difference-between-internet-gateway-and-nat-gateway-c9177e710af6

#### Security

##### NACL 

Network Access Control List == Firewall at the subnet boundary

You can dispose of multiple subnets to a NACL but only one NACL per subnet

Subnet * -- 1 NACL

##### Seurity Group (Virtual Firewall at Instance Level)

By DEfault Denies all Inbound Traffic and Allows all Outbound Traffic

Security Group are Stateful


__Security group as Source for a rule in another Security Group:__

"When you specify a security group as the source for a rule, traffic is allowed from the network interfaces that are associated with the source security group for the specified protocol and port. Incoming traffic is allowed based on the private IP addresses of the network interfaces that are associated with the source security group (and not the public IP or Elastic IP addresses). Adding a security group as a source does not add rules from the source security group."


https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html#SecurityGroupRules

#### Internet connectivity

An internet gateway is a VPC component that allows communication between your VPC and the internet.

### VPC Peering

A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. 

VPC Peering supports peering between multiple accounts



#### Configuration

1. Add VPC Peering
2. VPC Peering > Actions > Accept Request
1. ec2 Instance (Requester)  > Subnet > Route table > Route > Edit Routes > Add route > Copy CIDR (Finance) from VPC on Destination (ex: 172.31.0.0/16) AND Peering Conection (pcx- ...)
2. ec2 Instance (Accepter) > Subnet > Route table > Route > Edit Routes > Add route > Copy CIDR (Marketing) from VPC on Destination (ex: 192.168.0.0/20) AND Peering Conection (pcx- ...)
1. ec2 Instance Finance (Accepter) > update security > ADD ICMP - IPv4 (Copy CIDR 192.168.0.0/20) 
2. ec2 Instance DeveloperInstance > Connect > Session Manager > "ping 172.31.1.163"


### Amazon Relational Database Service (RDS)

Using multiple AZ's means : high availability and disaster recovery, not increased performance

Doing read-intensive workloads ? Solution : A read replica

### AWS CloudFormation

AWS CloudFormation is a service that helps you model and set up your AWS resources

### AWS CloudFront (CDN)

Amazon CloudFront is a web service that speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, to your users. CloudFront delivers your content through a worldwide network of data centers called edge locations. 

Note : 

__AWS Shield Standard__ is included automatically and transparently to Amazon CloudFront distributions providing:
- Active Traffic Monitoring with Network flow monitoring and Automatic always-on detection.
- Attack Mitigations with Protection from common DDoS attacks

Note :

__Edge locations__ are AWS data centers designed to deliver services with the lowest latency possible.

CloudFront, which uses edge locations to cache copies of the content that it serves, so the content is closer to users and can be delivered to them faster.

### AWS CloudTrail

AWS CloudTrail is an AWS service that helps you enable operational and risk auditing, governance, and compliance of your AWS account. Actions taken by a user, role, or an AWS service are recorded as events in CloudTrail. Events include actions taken in the AWS Management Console, AWS Command Line Interface, and AWS SDKs and APIs.


### AWS IAM

Manage access to AWS Resources

Free Service



## Credits

https://cloudtips.dev/2022/12/17/what-is-region-availability-zone-edge-locations-pop-in-aws/
