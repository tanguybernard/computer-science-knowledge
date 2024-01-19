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


Example:

1. First, the coffee shop owner grants the employee permissions to the "Cashier" and "Inventory" roles so they can switch between these two workstations.

2. The employee begins their day by assuming the “Cashier” role. This grants them access to the cash register system.

3. Later in the day, the employee needs to update the inventory system. They assume the “Inventory” role. 
This grants the employee access to the inventory system and also revokes their access to the cash register system.

### Multi-factor authentication

In IAM, multi-factor authentication (MFA) provides an extra layer of security for your AWS account.

## AWS organizations



Suppose that your company has multiple AWS accounts. You can use AWS Organizations(opens in a new tab) to consolidate and manage multiple AWS accounts within a central location.

When you create an organization, AWS Organizations automatically creates a __root__, which is the parent container for all the accounts in your organization. 

In AWS Organizations, you can centrally control permissions for the accounts in your organization by using __service control policies (SCPs)__. SCPs enable you to place __restrictions__ on the AWS services, resources, and individual API actions that users and roles in each account can access.

In AWS Organizations, you can __apply__ service control policies __(SCPs)__ to the __organization root__, an __individual member account__, or an __OU__. An SCP affects all IAM users, groups, and roles within an account, including the AWS account root user.

You can __apply__ IAM __policies__ to IAM __users, groups, or roles__. You __cannot__ apply an IAM policy to the AWS account __root__ user.

Note: Consolidated billing is another feature of AWS Organizations.

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
