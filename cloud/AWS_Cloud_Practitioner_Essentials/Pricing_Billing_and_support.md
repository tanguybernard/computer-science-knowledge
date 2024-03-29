# Pricing, Billing and Support

## AWS Free Tier

The AWS Free Tier enables you to begin using certain services without having to worry about incurring costs for the specified period. 

Three types of offers are available: 

- Always Free
- 12 Months Free
- Trials

## AWS Pricing Concepts

### How AWS pricing works


#### Pay for what you use.

For each service, you pay for exactly the amount of resources that you actually use, without requiring long-term contracts or complex licensing. 

#### Pay less when you reserve.

Some services offer reservation options that provide a significant discount compared to On-Demand Instance pricing.

For example, suppose that your company is using Amazon EC2 instances for a workload that needs to run continuously. You might choose to run this workload on Amazon EC2 Instance Savings Plans, because the plan allows you to save up to 72% over the equivalent On-Demand Instance capacity.

#### Pay less with volume-based discounts when you use more.

Some services offer tiered pricing, so the per-unit cost is incrementally lower with increased usage.

For example, the more Amazon S3 storage space you use, the less you pay for it per GB.

### AWS Pricing Calculator

The AWS Pricing Calculator lets you explore AWS services and create an estimate for the cost of your use cases on AWS. 

### AWS Pricing Example

#### Lambda

For AWS Lambda, you are charged based on the number of requests for your functions and the time that it takes for them to run.

AWS Lambda allows 1 million free requests and up to 3.2 million seconds of compute time per month.

You can save on AWS Lambda costs by signing up for a Compute Savings Plan. A Compute Savings Plan offers lower compute costs in exchange for committing to a consistent amount of usage over a 1-year or 3-year term. This is an example of paying less when you reserve. 

#### EC2

With Amazon EC2, you pay for only the compute time that you use while your instances are running.

For some workloads, you can significantly reduce Amazon EC2 costs by using Spot Instances. For example, suppose that you are running a batch processing job that is able to withstand interruptions. Using a Spot Instance would provide you with up to 90% cost savings while still meeting the availability requirements of your workload.


You can find additional cost savings for Amazon EC2 by considering Savings Plans and Reserved Instances.

#### S3

For Amazon S3 pricing, consider the following cost components:

- Storage - You pay for only the storage that you use. 
- Requests and data retrievals - You pay for requests made to your Amazon S3 objects and buckets. For example, suppose that you are storing photo files in Amazon S3 buckets and hosting them on a website. Every time a visitor requests the website that includes these photo files, this counts towards requests you must pay for.
- Data transfer - There is no cost to transfer data between different Amazon S3 buckets or from Amazon S3 to other services within the same AWS Region. However, you pay for data that you transfer into and out of Amazon S3, with a few exceptions. There is no cost for data transferred into Amazon S3 from the internet or out to Amazon CloudFront. There is also no cost for data transferred out to an Amazon EC2 instance in the same AWS Region as the Amazon S3 bucket.
- Management and replication - You pay for the storage management features that you have enabled on your account’s Amazon S3 buckets. These features include Amazon S3 inventory, analytics, and object tagging.

## Billing Dashboard

Use the AWS Billing & Cost Management dashboard(opens in a new tab) to pay your AWS bill, monitor your usage, and analyze and control your costs.

- Compare your current month-to-date balance with the previous month, and get a forecast of the next month based on current usage.
- View month-to-date spend by service.
- View Free Tier usage by service.
- Access Cost Explorer and create budgets.
- Purchase and manage Savings Plans.
- Publish AWS Cost and Usage Reports.

## Consolidated billing for AWS Organizations

You can use the consolidated billing feature in AWS Organizations to consolidate billing and payment for multiple AWS accounts or multiple Amazon Web Services India Private Limited (AWS India) accounts.

Consolidated billing has the following benefits:

- One bill – You get one bill for multiple accounts.
- Easy tracking – You can track the charges across multiple accounts and download the combined cost and usage data.
- Combined usage – You can combine the usage across all accounts in the organization to share the volume pricing discounts, Reserved Instance discounts, and Savings Plans. This can result in a lower charge for your project, department, or company than with individual standalone accounts.
- No extra fee – Consolidated billing is offered at no additional cost.



### Example:

Suppose that you are the business leader who oversees your company’s AWS billing. 

Your company has three AWS accounts used for separate departments. In this example, Account 1 owes $19.64, Account 2 owes $19.96, and Account 3 owes $20.06. Instead of paying each location’s monthly bill separately, you decide to create an organization and add the three accounts. 

You manage the organization through the primary account.

Each month AWS charges your primary payer account for all the linked accounts in a consolidated bill. Through the primary account, you can also get a detailed cost report for each linked account. 

The monthly consolidated bill also includes the account usage costs incurred by the primary account. 

The primary account incurred $14.14.

The consolidated bill shows the costs associated with any actions of the primary account (such as storing files in Amazon S3 or running Amazon EC2 instances). The total charged to the paying account, including the primary account and accounts one through three, is $73.80.

19.64 + 19.96 + 20.06 + 14.14 = 73.8

## AWS Budgets

In AWS Budgets, you can create budgets to plan your service usage, service costs, and instance reservations.

The information in AWS Budgets updates three times a day. This helps you to accurately determine how close your usage is to your budgeted amounts or to the AWS Free Tier limits.

In AWS Budgets, you can also set custom alerts when your usage exceeds (or is forecasted to exceed) the budgeted amount.

## AWS Cost Explorer

AWS Cost Explorer is a tool that lets you visualize, understand, and manage your AWS costs and usage over time.

AWS Cost Explorer includes a default report of the costs and usage for your top five cost-accruing AWS services.

Forecast future costs and usage of your AWS resources based on your past consumption.

## AWS Cost and Usage Report

The AWS Cost and Usage Reports (CUR) contains the most comprehensive set of cost and usage data available. You can use Cost and Usage Reports to export your cost and usage data to an Amazon S3 bucket that you own. You can receive exports that break down your costs by the hour, day, or month, by product or product resource, or by tags that you define yourself. 

Provides the most __granular__ data.

source: https://aws.amazon.com/fr/aws-cost-management/aws-cost-and-usage-reporting/faqs/

## Using AWS cost allocation tags

A tag is a label that you or AWS assigns to an AWS resource. Each tag consists of a key and a value. For each resource, each tag key must be unique, and each tag key can have only one value. You can use tags to organize your resources, and cost allocation tags to track your AWS costs on a detailed level. After you activate cost allocation tags, AWS uses the cost allocation tags to organize your resource costs on your cost allocation report, to make it easier for you to categorize and track your AWS costs. 

## AWS Support Plans

![aws_support_plans](https://github.com/tanguybernard/computer-science-knowledge/assets/14818169/793bb28a-0d2f-4324-acd7-b8694c84340d)


### Basic

Every customer automatically gets AWS Basic Support, no cost at all. Any customer can access support functions like 24/7 access to customer service, documentation, whitepapers, support forums, AWS Trusted Advisor, and the AWS Personal Health Dashboard.

### Developer Support

- Basic Support
- Email customer support directly with a 24-hour response time on any questions you have. And responses of less than 12 hours in case your systems are impaired (défaillance de vos systèmes).

This is a great plan for businesses that are experimenting with AWS or setting up tests or proofs of concept. 

### Business Support

- Developer Support
- All AWS Trusted Advisor checks
- Direct phone access to our support team. They have a 4-hour response time if your production system is impaired, and a 1-hour response time for when you production system is down.

### AWS Enterprise On-Ramp Support

- Business Support
- A pool of Technical Account Managers to provide proactive guidance and coordinate access to programs and AWS experts
- A Cost Optimization workshop (one per year)
- A Concierge support team for billing and account assistance
- Tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard

A pool of Technical Account Managers fo:

- Consultative review and architecture guidance (one per year)
- Infrastructure Event Management support (one per year)
- Support automation workflows
- 30 minutes or less response time for business-critical issues


### Entreprise

- Enterprise On-Ramp Support
- A designated Technical Account Manager to provide proactive guidance and coordinate access to programs and AWS experts
- A Concierge support team for billing and account assistance
- Operations Reviews and tools to monitor health
- Training and Game Days to drive innovation
- Tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard

The Enterprise plan also provides full access to proactive services, which are provided by a designated Technical Account Manager:

- Consultative review and architecture guidance
- Infrastructure Event Management support
- Cost Optimization Workshop and tools
- Support automation workflows
- 15 minutes or less response time for business-critical issues

### Notes 

__Technical Account Manager (TAM)__

The Enterprise On-Ramp and Enterprise Support plans include access to a Technical Account Manager (TAM).

The TAM is your primary point of contact at AWS. If your company subscribes to Enterprise Support or Enterprise On-Ramp, your TAM educates, empowers, and evolves your cloud journey across the full range of AWS services. TAMs provide expert engineering guidance, help you design solutions that efficiently integrate AWS services, assist with cost-effective and resilient architectures, and provide direct access to AWS programs and a broad community of experts.

For example, suppose that you are interested in developing an application that uses several AWS services together. Your TAM could provide insights into how to best use the services together. They achieve this, while aligning with the specific needs that your company is hoping to address through the new application.


## AWS Marketplace

AWS Marketplace is a digital catalog that includes thousands of software listings from independent software vendors. You can use AWS Marketplace to find, test, and buy software that runs on AWS. 


## Savings Plans

Les Savings Plans sont un modèle de tarification flexible qui offre des tarifs inférieurs à la tarification à la demande en échange d'un engagement d'utilisation donné (mesuré en USD/heure) sur une période de un ou trois ans. 


AWS offers two types of Savings Plans:

- Compute Savings Plans provide the most flexibility and help to reduce your costs by up to 66% (just like Convertible RIs). These plans automatically apply to EC2 instance usage regardless of instance family, size, AZ, Region, operating system, or tenancy, and also apply to Fargate and Lambda usage.

- EC2 Instance Savings Plans provide the lowest prices, offering savings up to 72% (just like Standard RIs) in exchange for commitment to usage of individual instance families in a Region (for example, M5 usage in N. Virginia). 

https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-reservation-models/savings-plans.html

### AWS concierge 

When you subscribe to an Enterprise plan or qualified Reseller Support plan, your Amazon Web Services Concierge will be assigned to your account. The global customer service team is available to assist you 24/7, 365 days a year.

https://www.watsonmedia.net/question/what-is-aws-concierge/

## QUESTIONS:

https://www.examtopics.com/discussions/amazon/view/79266-exam-aws-certified-cloud-practitioner-topic-1-question-16/


## Cost and Usage Reports

This solution consolidates the billing in a report, but it will work only for the individual accounts (without cross-account billing). 
