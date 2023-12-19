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

Control Virtual Network Environment (Ip Adress range, subnets, route tables, Network Gateways)

A __subnet__ is a range of IP addresses in your VPC. You can create AWS resources, such as EC2 instances, in specific subnets.


### Security

#### NACL 

Network Access Control List == Firewall at the subnet boundary

You can dispose of multiple subnets to a NACL but only one NACL per subnet

Subnet * -- 1 NACL

#### Seurity Group (Virtual Firewall at Instance Level)

By DEfault Denies all Inbound Traffic and Allows all Outbound Traffic

Security Group are Stateful


__Security group as Source for a rule in another Security Group:__

"When you specify a security group as the source for a rule, traffic is allowed from the network interfaces that are associated with the source security group for the specified protocol and port. Incoming traffic is allowed based on the private IP addresses of the network interfaces that are associated with the source security group (and not the public IP or Elastic IP addresses). Adding a security group as a source does not add rules from the source security group."


https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html#SecurityGroupRules

### Internet connectivity

An internet gateway is a VPC component that allows communication between your VPC and the internet.

## VPC Peering

A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses. 

VPC Peering supports peering between multiple accounts



### Configuration

1. Add VPC Peering
2. VPC Peering > Actions > Accept Request
1. ec2 Instance (Requester)  > Subnet > Route table > Route > Edit Routes > Add route > Copy CIDR (Finance) from VPC on Destination (ex: 172.31.0.0/16) AND Peering Conection (pcx- ...)
2. ec2 Instance (Accepter) > Subnet > Route table > Route > Edit Routes > Add route > Copy CIDR (Marketing) from VPC on Destination (ex: 192.168.0.0/20) AND Peering Conection (pcx- ...)
1. ec2 Instance Finance (Accepter) > update security (Copy CIDR 192.168.0.0/20)
2. ec2 Instance DeveloperInstance > Connect > Session Manager > "ping 172.31.1.163"

