# Migration To AWS Why and How ?

## AWS Cloud Adoption Framework (AWS CAF)

Six Core Perspectives:

Business capabilities :

- The Business Perspective ensures that IT aligns with business needs and that IT investments link to key business results.
- The People Perspective supports development of an organization-wide change management strategy for successful cloud adoption.
- The Governance Perspective focuses on the skills and processes to align IT strategy with business strategy. This ensures that you maximize the business value and minimize risks.

Technical capabilities:

- The Platform Perspective includes principles and patterns for implementing new solutions on the cloud, and migrating on-premises workloads to the cloud.
- The Security Perspective ensures that the organization meets security objectives for visibility, auditability, control, and agility.
- The Operations Perspective helps you to enable, run, use, operate, and recover IT workloads to the level agreed upon with your business stakeholders.

## Migration Strategies

6 strategies for migration

When migrating applications to the cloud, six of the most common migration strategies(opens in a new tab) that you can implement are:

### Rehosting

Rehosting also known as “lift-and-shift” involves moving applications without changes. 


### Replatforming

Replatforming, also known as “lift, tinker, and shift,” involves making a few cloud optimizations to realize a tangible benefit. Optimization is achieved without changing the core architecture of the application.

### Refactoring/re-architecting

Refactoring (also known as re-architecting) involves reimagining how an application is architected and developed by using cloud-native features.

### Repurchasing

Repurchasing involves moving from a traditional license to a software-as-a-service model. 

For example, a business might choose to implement the repurchasing strategy by migrating from a customer relationship management (CRM) system to Salesforce.com.

### Retaining

Retaining consists of keeping applications that are critical for the business in the source environment. This might include applications that require major refactoring before they can be migrated, or, work that can be postponed until a later time.

### Retiring

Retiring is the process of removing applications that are no longer needed.

## AWS Snow Family

The AWS Snow Familyis a collection of physical devices that help to physically transport up to exabytes of data into and out of AWS. 

### AWS Snowcone 

AWS Snowcone is a small, rugged, and secure edge computing and data transfer device. 

### AWS Snowball

Snowball Edge Storage Optimized devices are well suited for large-scale data migrations and recurring transfer workflows, in addition to local computing with higher capacity needs. 

Snowball Edge Storage Optimized is a device that enables you to transfer large amounts of data into and out of AWS. It provides 80 TB of usable HDD storage.


Snowball Edge Compute Optimized provides powerful computing resources for use cases such as machine learning, full motion video analysis, analytics, and local computing stacks.

### AWS Snowmobile

AWS Snowmobile is an exabyte-scale data transfer service used to move large amounts of data to AWS. 

You can transfer up to 100 petabytes of data per Snowmobile, a 45-foot long ruggedized shipping container, pulled by a semi trailer truck.




