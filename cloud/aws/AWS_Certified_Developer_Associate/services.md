

Tuto

https://github.com/ExamProCo/TheFreeAWSDeveloperAssociate/tree/master

# Services


ASG : Auto Scalling group

Blue/Green deployment is when you run two identical production envs and shift traffic from Blue (old) to Green (new).



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

- Similar to rolling updates but you spin up new instances to move the
batch (so the old application is still available)

#### Immutable

- Spins up new instances in a new ASG, deploys versions to these
instances and then swaps all the instances when everything is healthy
- Like blue/green deployment but it's under the same load balancer, a new autoscaling group is created alongside the old one.

#### Blue/Green for EB

- A new environment is created from scratch (so another load balancer). The switch is performed at DNS level routing the traffic from the OLD to the NEW when the new environment is ready and healthy.

#### Configuration files

Add deployment policy in it and others stuff...

https://youtu.be/TTcyhhH2FWE?t=3301

#### EB Traffic spliting (Deployment Policy) => it's Canary deployment

https://youtu.be/TTcyhhH2FWE?t=3340

Allows you to forward a portion of your traffic to the new env and after a priod a time then move the rest.

### Environment Manifest (env.yml)

environment, stack (ruby, nodejs)...

### Linux server configuration

- You can configure packages, ruby dependencies for example 
- Create Linux users, groups, files with permissions...
- Create services like nginx
- Execute commands

### CLI

Manage your eb envs...

### Custom image

https://youtu.be/TTcyhhH2FWE?t=3714

### Configuring RDS

A database can be added inside ou outside your environment.

Inside for development.

Outside for production.
