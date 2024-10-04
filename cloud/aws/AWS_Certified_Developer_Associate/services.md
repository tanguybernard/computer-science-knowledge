
# Services

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

#### All At once

https://youtu.be/TTcyhhH2FWE?t=2520
