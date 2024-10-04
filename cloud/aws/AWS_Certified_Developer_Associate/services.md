
# Services


ASG : Auto Scalling group



## Elastic Beanstalk

Cloudformation setups for you :

- ELB
- Autoscaling group
- RDS
- EC2 
- Monotiroing
- ...
- Can Run Dockerized environments


### Web Environment vs Worker Environment

Web Environment => ex: Web app

Worker Environment => ex: long running jobs


#### Web environment types

- Load Balanced Env  (with ELB, designed to scale)
- Single Instance Env (without ELB to save cost, use public ip Address)


### Deployment Policies

#### All At once (Downtime)

https://youtu.be/TTcyhhH2FWE?t=2520

- Deploys the new version to all instances
- Take all instances out of service during deployment

Fast but dangerous

#### Rolling

- Deploys the new version to a batch of instances at a time
- Offline during deployment

#### Rolling with additional Batch

#### Immutable

- Spins up new instances in a new ASG, deploys versions to these
instances and then swaps all the instances when everything is healthy
- Like blue/green deployment
