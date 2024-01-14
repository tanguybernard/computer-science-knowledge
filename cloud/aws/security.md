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
