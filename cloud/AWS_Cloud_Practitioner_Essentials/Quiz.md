# Quiz


### A global company is building a simple time-tracking mobile app. The app needs to operate globally and must store collected data in a database. Data must be accessible from the AWS Region that is closest to the user. What should the company do to meet these data storage requirements with the LEAST amount of operational overhead?

    A. Use Amazon EC2 in multiple Regions to host separate databases
    B. Use Amazon RDS cross-Region replication
    C. Use Amazon DynamoDB global tables [Most Voted]
    D. Use AWS Database Migration Service (AWS DMS)


Note: 

B is wrong because RDS replication is applied when there is too many read and write request that will affect the performance of the RDS. We can use the replicated RDS for read purpose.

Global tables build on the global Amazon DynamoDB footprint to provide you with a fully managed, multi-Region, and multi-active database that delivers fast, local, read and write performance for massively scaled, global applications. Global tables replicate your DynamoDB tables automatically across your choice of AWS Regions.


### A company has a database server that is always running. The company hosts the server on Amazon EC2 instances. The instance sizes are suitable for the workload. The workload will run for 1 year. Which EC2 instance purchasing option will meet these requirements MOST cost-effectively?

    A. Standard Reserved Instances [Most Voted]
    B. On-Demand Instances
    C. Spot Instances
    D. Convertible Reserved Instances


"Standard Reserved Instances provide you with a significant discount (up to 72%) compared to On-Demand Instance pricing, and can be purchased for a 1-year or 3-year term. Customers have the flexibility to change the Availability Zone, the instance size, and networking type of their Standard Reserved Instances.

Purchase Convertible Reserved Instances if you need additional flexibility, such as the ability to use different instance families, operating systems, or tenancies over the Reserved Instance term. Convertible Reserved Instances provide you with a significant discount (up to 66%) compared to On-Demand Instances and can be purchased for a 1-year or 3-year term."

https://docs.aws.amazon.com/whitepapers/latest/cost-optimization-reservation-models/standard-vs.-convertible-offering-classes.html
