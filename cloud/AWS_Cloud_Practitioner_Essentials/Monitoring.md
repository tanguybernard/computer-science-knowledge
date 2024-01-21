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

Trusted Advisor compares its findings to AWS best practices in five categories:

- cost optimization
- performance
- security
- fault tolerance
- service limits


__Cost optimization Example__: I do have some RDS instances that are idle, as well as some underutilized EC2 instances and EBS volumes. 

__Performance__: Checks for EBS volumes whose performance might've been affected by the throughput capability of the EC2 instance that it's attached to. 

__Security Example__: I have weak password policies for IAM users, multi-factor authentication is not turned on for the root user, and there are security groups allowing public access to EC2 instances.

__Fault tolerance Example__: There are EBS volumes without snapshots in this account. Remember, a snapshot is a backup. So without backups, if I had an EBS volume fail, I would lose that data. Or my EC2 instances are not properly launched across AZs.

__Service limits__:I can see that I have five VPCs, which is the regional limit. So I've hit that specific service limit. 


