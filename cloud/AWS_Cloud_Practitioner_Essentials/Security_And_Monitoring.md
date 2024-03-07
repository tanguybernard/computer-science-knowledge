# Security 

## AWS Shared Responsability Model

- Customer: Responsible for security "in" the cloud
- AWS: Responsible for security "of" the cloud

### Example With EC2

| Who ?            | Responsiblity     | 
| :--------------- |:-----------------:|
| Customer  | OS, Application, Data    |
| AWS  |   Physical, Network, Hypervisor|

_You can think of this model as being similar to the division of responsibilities between a homeowner and a homebuilder. The builder (AWS) is responsible for constructing your house and ensuring that it is solidly built. As the homeowner (the customer), it is your responsibility to secure everything in the house by ensuring that the doors are closed and locked._

### Customers: Security in the cloud

- Selecting, configuring, and patching the operating systems that will run on Amazon EC2 instances
- Configuring security groups
- Managing user accounts
- Setting permissions for Amazon S3 objects
- ...

### AWS: Security Of the cloud

AWS manages the security of the cloud, specifically the physical infrastructure that hosts your resources, which include:

- Physical security of data centers
- Hardware and software infrastructure
- Network infrastructure
- Virtualization infrastructure

## User Permissions and Access


### Account

Think of an account as just a container. A container containing your resources, users and account settings.

You can create multiple of these containers. In fact, it is best practice to separate your different workloads (for example test and production) into different accounts.

The root user is the master of your account.

Credits: https://blog.jannikwempe.com/aws-accounts-iam-users-root-user


### AWS Identity and access management (AWS IAM)

AWS Identity and Access Management (IAM) enables you to manage access to AWS services and resources securely.   

### AWS account root user

AWS Account root user: Access and control any resource in the account.


### IAM Users

Principle of least privilege: A user is granted access only to what they need.


An IAM user is an identity that you create in AWS. It represents the person or application that interacts with AWS services and resources. It consists of a name and credentials.

By default, when you create a new IAM user in AWS, it has no permissions associated with it.


### Policies 

An IAM policy is a document that allows or denies permissions to AWS services and resources.  

__Policies__ describe permissions that you can attach to users or groups.

IAM policies provide you with the flexibility to customize users’ levels of access to resources. For instance, you can allow users to access all the Amazon S3 buckets in your AWS account or only a specific bucket.

### IAM groups

An IAM group is a collection of IAM users. When you assign an IAM policy to a group, all users in the group are granted permissions specified by the policy.

### IAM roles

An IAM role is an identity that you can assume to gain temporary access to permissions.  

AWS IAM Roles:
- Associated permissions
- Allow or Deny
- Assumed for temporary amounts of time
- No username or password
- Access to temporary permissions
- For AWS ressources, users, external identities, applications, other aws services


Examples:

1. First, the coffee shop owner grants the employee permissions to the "Cashier" and "Inventory" roles so they can switch between these two workstations.

2. The employee begins their day by assuming the “Cashier” role. This grants them access to the cash register system.

3. Later in the day, the employee needs to update the inventory system. They assume the “Inventory” role. 
This grants the employee access to the inventory system and also revokes their access to the cash register system.

Notes:

As a best practice for granting AWS credentials and authorizations to a web application, you should use an **IAM role**. IAM roles are a secure way to grant permissions to AWS resources, such as services or applications, without the need for long-term access keys (access key ID and secret access key). Roles are typically **assumed by trusted entities**, like AWS services or EC2 instances, to securely delegate access to resources.

### Multi-factor authentication

In IAM, multi-factor authentication (MFA) provides an extra layer of security for your AWS account.

## AWS organizations



Suppose that your company has multiple AWS accounts. You can use AWS Organizations(opens in a new tab) to consolidate and manage multiple AWS accounts within a central location.

When you create an organization, AWS Organizations automatically creates a __root__, which is the parent container for all the accounts in your organization. 

In AWS Organizations, you can centrally control permissions for the accounts in your organization by using __service control policies (SCPs)__. SCPs enable you to place __restrictions__ on the AWS services, resources, and individual API actions that users and roles in each account can access.

In AWS Organizations, you can __apply__ service control policies __(SCPs)__ to the __organization root__, an __individual member account__, or an __OU__. An SCP affects all IAM users, groups, and roles within an account, including the AWS account root user.

You can __apply__ IAM __policies__ to IAM __users, groups, or roles__. You __cannot__ apply an IAM policy to the AWS account __root__ user.

Note: Consolidated billing is another feature of AWS Organizations.


### SCPs

Service control policies (SCPs) enable you to centrally control permissions for the accounts in your organization.

### Organizational units (OU)

In AWS Organizations, you can __group accounts__ into organizational units (OUs) to make it easier to manage accounts with similar business or security requirements. When you apply a policy to an OU, all the accounts in the OU automatically inherit the permissions specified in the policy. 

By organizing separate accounts into OUs, you can more easily isolate workloads or applications that have specific security requirements.

## Compliance

### AWS Artifact

AWS Artifact is a service that provides on-demand access to AWS security and compliance reports and select online agreements. AWS Artifact consists of two main sections: AWS Artifact Agreements and AWS Artifact Reports.

AWS Artifact provides access to AWS security and compliance documents, such as AWS ISO certifications, Payment Card Industry (PCI) reports, and Service Organization Control (SOC) reports.

#### AWS Artifact Agreements

In AWS Artifact Agreements, you can review, accept, and manage agreements for an individual account and for all your accounts in AWS Organizations. Different types of agreements are offered to address the needs of customers who are subject to specific regulations, such as the Health Insurance Portability and Accountability Act (HIPAA).

#### AWS Artifact Reports

AWS Artifact Reports provide compliance reports from third-party auditors. 

### Customer Compliance Center

The Customer Compliance Center(opens in a new tab) contains resources to help you learn more about AWS compliance. 

In the Customer Compliance Center, you can read customer compliance stories to discover how companies in regulated industries have solved various compliance, governance, and audit challenges.

Additionally, the Customer Compliance Center includes __an auditor learning path__.

## Denial-of-Service Attacks

A denial-of-service (DoS) attack is a deliberate attempt to make a website or application unavailable to users.

### Distributed denial-of-service attacks

In a distributed denial-of-service (DDoS) attack, multiple sources are used to start an attack that aims to make a website or application unavailable. This can come from a group of attackers, or even a single attacker. The single attacker can use multiple infected computers (also known as “bots”) to send excessive traffic to a website or application.

To help minimize the effect of DoS and DDoS attacks on your applications, you can use __AWS Shield__.

### AWS Shield

AWS Shield is a service that protects applications against DDoS attacks. AWS Shield provides two levels of protection: Standard and Advanced.

#### AWS Shield Standard

AWS Shield Standard automatically protects all AWS customers at no cost. It protects your AWS resources from the most common, frequently occurring types of DDoS attacks. 

As network traffic comes into your applications, AWS Shield Standard uses a variety of analysis techniques to detect malicious traffic in real time and automatically mitigates it. 

#### AWS Shield Advanced

AWS Shield Advanced is a paid service that provides detailed attack diagnostics and the ability to detect and mitigate sophisticated DDoS attacks.

It also integrates with other services such as Amazon CloudFront, Amazon Route 53, and Elastic Load Balancing. Additionally, you can integrate AWS Shield with AWS WAF by writing custom rules to mitigate complex DDoS attacks.


## Additional Security Services

### AWS Key Management Service (AWS KMS)

AWS Key Management Service (AWS KMS)(opens in a new tab) enables you to perform encryption operations through the use of cryptographic keys. 

You can use AWS KMS to create, manage, and use cryptographic keys. You can also control the use of keys across a wide range of services and in your applications.

### Amazon WAF

AWS WAF is a web application firewall that lets you monitor network requests that come into your web applications. 

AWS WAF works together with Amazon CloudFront and an Application Load Balancer. Recall the network access control lists that you learned about in an earlier module. AWS WAF works in a similar way to block or allow traffic. However, it does this by using a web access control list (ACL) to protect your AWS resources. 

### Amazon Inspector

Amazon Inspector helps to improve the security and compliance of applications by running automated security assessments (FR: des évaluations de sécurité automatisées). It checks applications for security vulnerabilities and deviations from security best practices, such as open access to Amazon EC2 instances and installations of vulnerable software versions. 

Amazon Inspector uses a set of predefined rules to assess the security state of your resources. It analyzes the network activity, operating system configurations, and application behavior to identify potential security issues. The assessment report provides detailed findings and recommendations for remediation.

### Amazon GuardDuty

Amazon GuardDutyis a service that provides intelligent threat detection for your AWS infrastructure and resources. It identifies threats by continuously monitoring the network activity and account behavior within your AWS environment.

### Amazon Macie (Security, Identity & Compliance)

Amazon Macie discovers sensitive data using machine learning and pattern matching, provides visibility into data security risks, and enables automated protection against those risks.

Use Case: Discover sensitive data across your S3 environment to increase visibility and automated remediation of data security risks.

# Monitoring

## Amazon CloudWatch

Amazon CloudWatch is a web service that enables you to monitor and manage various metrics and configure alarm actions based on data from those metrics.

CloudWatch uses metrics(opens in a new tab) to represent the data points for your resources. AWS services send metrics to CloudWatch. CloudWatch then uses these metrics to create graphs automatically that show how performance has changed over time. 

With CloudWatch you can :

- Monitor your AWS infrastructure and resources in real time
- View metrics and graphs to monitor the performance of resources
- Configure automatic actions and alerts in response to metrics

### CloudWatch alarms

With CloudWatch, you can create alarms that automatically perform actions if the value of your metric has gone above or below a predefined threshold (seuil prédéfini).

_For example, suppose that your company’s developers use Amazon EC2 instances for application development or testing purposes. If the developers occasionally forget to stop the instances, the instances will continue to run and incur charges._ 

_In this scenario, you could create a CloudWatch alarm that automatically stops an Amazon EC2 instance when the CPU utilization percentage has remained below a certain threshold for a specified period. When configuring the alarm, you can specify to receive a notification whenever this alarm is triggered._

### CloudWatch dashboard

The CloudWatch dashboard feature enables you to access all the metrics for your resources from a single location. For example, you can use a CloudWatch dashboard to monitor the CPU utilization of an Amazon EC2 instance, the total number of requests made to an Amazon S3 bucket, and more.

## AWS CloudTrail

AWS CloudTrail records API calls for your account. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, and more. You can think of CloudTrail as a “trail” of breadcrumbs (or a log of actions) that someone has left behind them.

With CloudTrail you can:

- Track user activities and API requests throughout your AWS infrastructure
- Filter logs to assist with operational analysis and troubleshooting


### CloudTrail Insights

Within CloudTrail, you can also enable CloudTrail Insights(opens in a new tab). This optional feature allows CloudTrail to automatically detect unusual API activities in your AWS account. 

For example, CloudTrail Insights might detect that a higher number of Amazon EC2 instances than usual have recently launched in your account. You can then review the full event details to determine which actions you need to take next.


## AWS Trusted Advisor

AWS Trusted Advisor is a web service that inspects your AWS environment and provides real-time recommendations in accordance with AWS best practices.

The inspection includes security checks, such as Amazon S3 buckets with open access permissions.

Trusted Advisor compares its findings to AWS best practices in five categories:

- cost optimization
- performance
- security
- fault tolerance
- service limits

Trusted Advisor checks security groups for rules that allow unrestricted access to a resource. Unrestricted access increases opportunities for malicious activity, such as hacking, denial-of-service attacks, or loss of data. 


__Cost optimization Example__: I do have some RDS instances that are idle, as well as some underutilized EC2 instances and EBS volumes. 

__Performance__: Checks for EBS volumes whose performance might've been affected by the throughput capability of the EC2 instance that it's attached to. 

__Security Example__: I have weak password policies for IAM users, multi-factor authentication is not turned on for the root user, and there are security groups allowing public access to EC2 instances.

## AWS X-Ray

AWS X-Ray helps developers analyze and debug production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can understand how your application and its underlying services are performing to identify and troubleshoot the root cause of performance issues and errors. X-Ray provides an end-to-end view of requests as they travel through your application, and shows a map of your application’s underlying components.

## CloudWatch vs CloudTrail vs X-Ray

AWS CloudWatch
- Metrics : collecte les métriques intégrés aux services AWS et ceux de votre application
- Logs : collecte et stocke les fichiers journaux (logs)
- Events : envoie de notification en réaction à certains événements
- Alarms : définit des seuils d’activation (alarms) qui déclenche une action
AWS X-Ray
- Aide à l’analyse et au débogage d’applications mêmes celles distribuées
- Produit sous forme graphique le parcours d’une requête et des composants qu’elle traverse avec les erreurs associées
AWS CloudTrail
- Monitoring des appels aux APIs
- Analyse de conformité
- Audit opérationnel

## Waf, Shield, GuardDuty

**Shield** is DDoS protection and also located "at the edge".

**AWS WAF** is a web application firewall which is able to be configured in front of your web application where it will monitor http requests and prevent any halmful ones. This is only for web traffic.

**Amazon GuardDuty** ("neighbourhood watch") is an active intruder detection system which constantly monitors suspected configuration changes and anomalies in your AWS account and notifies relevant parties for further actions.

GuardDuty is like an antivirus for the whole AWS account while WAF is a specialized firewall for web traffic for a configured web application.

GuardDuty is intelligent threat detection. That means without much configuration, it reads your CloudTrail, Config and VPC FlowLogs and notifies if something unexpected happened. That is usually for infrastructure.

**Amazon Inspector** ("building inspector") is more for applications. It's an automated security assessment service that helps improve the security and compliance of applications. 
