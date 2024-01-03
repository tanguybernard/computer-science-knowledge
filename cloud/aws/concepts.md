# Notes

##  Certification

https://stormacq.com/2020/08/31/bien-demarrer.html

## Cloud Computing

Definition: On-demand delivery of IT resources and applications through the internet with pay-as-you-go pricing

3 Models:
- Cloud Based
- On-Premise
- Hybrid

__Upfront expense__ refers to data centers, physical servers, and other resources that you would need to invest in before using them.

__Variable expense__ means you only pay for computing resources you consume.


__How does the scale of cloud computing help you to save costs?__
The aggregated cloud usage from a large number of customers results in lower pay-as-you-go prices.


## AWS Well-Architected 

AWS Well-Architected  helps cloud architects and developers build secure, high-performing, resilient, and efficient infrastructure for a variety of applications and workloads.

https://aws.amazon.com/getting-started/cloud-essentials/?nc1=h_ls


## Cloud Concepts

https://coderjony.com/blogs/cloud-computing-concepts-high-availability-scalability-elasticity-agility-fault-tolerance-and-disaster-recovery

## AWS General Info


Key concept : You only pay for what you use !

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

Burstable:

Traditional Amazon EC2 instance types provide fixed CPU resources, while burstable performance instances provide a baseline level of CPU utilization with the ability to burst CPU utilization above the baseline level. 


#### Family

- General Purpose: Balanced ressources - Ideal for Web Services, backend servers for enterprise applications...
- Compute optimized: high-performance processors - Ideal for Web, gaming servers...
- Memory optimized: fast performance for workloads that process large datasets in memory (ex: high-performance databases)
- Accelerated computing: use hardware accelerators, or coprocessors, to perform some functions more efficiently than is possible in software running on CPUs
- Storage optimized: high performance for locally stored data. (ex: data warehousing applications)

#### Amazon EC2 pricing

- On Demand
- Savings Plans
- Reserved Instances (predictable )
- Spot Instances (can be reclaim, can be interrupted)
- Dedicated hosts (physical servers with Amazon EC2 instance capacity that is fully dedicated to your use)

Notes:

EC2 Instance Savings Plans reduce your EC2 instance costs when you make an hourly spend commitment to an instance family and Region for a 1-year or 3-year term.

__What is the difference between EC2 Savings Plan and Reserved Instances (RIs)?__

__Reserved instances__ provide a discount when you reserve a certain amount of __computing power__ (measured per hour) for a one- or three-year period while __Savings Plans__ provide a discount when you commit to spending a __certain amount__ (measured in dollars per hour) for a one-or three-year period.


### AWS EC2 Auto Scaling and Healing

#### Scaling

Two approaches:

- Dynamic scaling responds to changing demand. 
- Predictive scaling automatically schedules the right number of Amazon EC2 instances based on predicted demand.


##### Auto Scaling group

An Auto Scaling group contains a collection of EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. 

You can set:
- minimum capacity (number of Amazon EC2 instances that launch immediately after you have created the Auto Scaling group)
- desired capacity
- maximum capacity

###### How Configure ?

You can capture the content of an instance and its volume into AMI :

1. Click to an Instance
2. Actions
3. Image and template
4. Create Image

By default, an AMI that you create is available only within the AWS Region of creation.


Create a Launch Template

For example, a launch template can contain the AMI ID, instance type (ex: t2.nano), and network settings that you typically use to launch instances.

Finally Create an Auto Scaling Group

You can create a __Scheduled scaling__ : 

With scheduled scaling, you can set up automatic scaling for your application based on predictable load changes by creating scheduled actions that increase or decrease your group's desired capacity at specific times.



#### Healing

For example with Load Balancer to Replace or Rebalance.


### AWS Elastic Load Balancing (ELB)

Service that automatically distributes incoming application traffic across multiple resources, such as Amazon EC2 instances.

### Amazon Simple Queue Service (SQS)

Message queuing service. 

In Amazon SQS, an application sends messages into a queue.

### Amazon Simple Notification Service (SNS)

Pub Sub service.

Using Amazon SNS topics, a publisher publishes messages to subscribers.

### AWS Lambda (Serverless Compute)

AWS Lambda is serverless compute service for running code without having to provision or manage servers.

 AWS Lambda has a configurable maximum execution time limit of up to 15 minutes.

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

### AWS CloudWatch

Monitoring and observability service.

Monitor resources. Track metrics CPU, RAM, Network...

Collect metrics on AWS Services and On-Premises

### Amazon Simple Notification Service (SNS)

A web service that coordinates and manages message delivery from publishers to subscribers.

### AWS Elasctic Load Balancing (ELB)

Distributes incoming traffic.

To do that, we must create Listener, that define rules.

Load Balancer Types (for High Availability, Automatic Scaling, Robust Security, Fault Tolerance) :
- Application LB (Layer 7 - App, http, https, gRPC)
- Network LB (Layer 4 - Connetion, TCP, UDP, TLS)
- Gateway LB (Layer 4 And Layer 3 - Gateway, IP)
- Classic LB (Layer 4 - Layer 7, TCP, SSL, TLS, HTTP, HTTPS)

### AWS IAM

Manage access to AWS Resources

Free Service

## Pricing

### Savings Plans

Les Savings Plans sont un modèle de tarification flexible qui offre des tarifs inférieurs à la tarification à la demande en échange d'un engagement d'utilisation donné (mesuré en USD/heure) sur une période de un ou trois ans. 

### AWS concierge 

When you subscribe to an Enterprise plan or qualified Reseller Support plan, your Amazon Web Services Concierge will be assigned to your account. The global customer service team is available to assist you 24/7, 365 days a year.

https://www.watsonmedia.net/question/what-is-aws-concierge/

## Highly Available Web Application

- Minimize service interruptions
- Enable resources to be available when they are needed

Principles for architecting High Availability:

- Design For Failure (solution ex: Services spread over multiple regions and AZs)
- Embrace elasticity and Automation (solution ex: CloudWatch and Auto Scaling Groups)
- Loosely couple components (solution ex: Elastic Load Balancer, Amazon SQS (Queue))
- Become Stateless (Amazon Elasticache, DynamoDB)
- Use Parallelism (ex: Use microservices)
- Security as forethought (ex: Encryption, Principle Of Least Privileges)




## Credits

https://cloudtips.dev/2022/12/17/what-is-region-availability-zone-edge-locations-pop-in-aws/
