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


