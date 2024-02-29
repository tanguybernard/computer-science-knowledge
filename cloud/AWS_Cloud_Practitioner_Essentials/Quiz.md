# Quiz


### A global company is building a simple time-tracking mobile app. The app needs to operate globally and must store collected data in a database. Data must be accessible from the AWS Region that is closest to the user. What should the company do to meet these data storage requirements with the LEAST amount of operational overhead?

    A. Use Amazon EC2 in multiple Regions to host separate databases
    B. Use Amazon RDS cross-Region replication
    C. Use Amazon DynamoDB global tables [Most Voted]
    D. Use AWS Database Migration Service (AWS DMS)


Note: 

B is wrong because RDS replication is applied when there is too many read and write request that will affect the performance of the RDS. We can use the replicated RDS for read purpose.

Global tables build on the global Amazon DynamoDB footprint to provide you with a fully managed, multi-Region, and multi-active database that delivers fast, local, read and write performance for massively scaled, global applications. Global tables replicate your DynamoDB tables automatically across your choice of AWS Regions.

