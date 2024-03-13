# Section 18: Account Management, Billing and Support

# 213: Organizations Overview
- Global
- allows to manage multiple AWS account
- the main account is the master account
- cost benefit:
  - consolidated billing
  - pricing benefits from aggregated usage
  - pooling of reserved ec2  instances for optimal savings
- api is available to automate aws account creation
- restrict account privileges using SCP

### Multiaccount Strategies
- create accounts per department, per cost center, per dev, per test, based on regulatory restrictions
- multi account vs one account multivpc
- using tagging for billing
- enable cloud trail on all accounts, send logs to central s3 account

### Organization Units (OU)
- organize them
  - business unit
  - env lifecycle
  - project based

- organization
  - root ou
     - dev ou
     - prod ou
         - hr ou
         - finance ou
      
### SCP Service Control Policies
- whitelist or blacklist IAM actions
- applied at the ou or account level
- does not apply to master account
- is applied to all the users and roles of the account including root
- does not apply to service linked roles
- scp must have an explicit allow
- use cases:
  - restrict access to certain services, for example, cant use EMR
  - enforce PCI compliance

---

# 214: Organizations hands on

---

# 215: Consolidated Billing
- when enabled:
  - combined usage
    - shared the volume pricing
    - reserved instances and savings plan discount
  - one bill
  - example: 2 accounts with one having 5 ec2 reserved instances, if other account is going to use ec2 instance, it will be considered reserved instance if the capacity allows it
  - can turn off this behaviour
 
---

# 216: AWS Control Tower
- automate the setup of environment in a few clicks
- automate ongoing policy management using guardrails
- detect policy violations and remediate them
- monitor compliance through and interactive dashboard
- runs on top of aws organizations.

---

# 217: AWS Control Tower Hands On
- Go to Control tower
- you can deny access to some regions by denying it
- select or create an account for log archive
- same with audit account
- account factory: how you enroll an account in the control tower

---

# 218: AWS Resource Access Manager (AWS RAM)
- share aws resources that you own with other aws account
- share with any account or within your organization
- avoid resource duplication
- supports aurora, vpc subnet, transit gateway, route 53, ec2 dedicated hosts

---

# 219: AWS Service Catelog
- new users have too many options, and what they may create might deviate from requirements/ compliance of the organization
- some users just want a quick self service portal to launch a set of auth products pre-defined by admins
- includes VM, dbs, storage options,
- you as an admin, create products (CF templates), and portfolio of products, control access to them
- users just launch the template if authorized to do so

  ---

# 220: Pricing Models
- 4 models
- Pay as you go
- Save when you reserve: ec3 reserved, dynamoDB, elasticache, rds, redshift
- pay less by using more: volume based discounts
- pay less by AWS grows

### Free services & Free tier
- Free
  - IAM
  - VPC
  - Consolidated Billing
- Free but pay for things they create:
  - Beanstalk
  - CF
  - ASG
- Free Tier

### Compute Pricing : EC2
- only charged for what you use
- \# of instances
- instance config:
  - capacity
  - region
  - os
  - type
  - size
- ELB run time and amount of data proc
- detailed monitoring

### diff models for ec2
- on demand instances:
  - min of 60s
  - pay per seconds (linux/windows), pay per hours(other)
- reserved instances:
  - up to 75% discount compared to on demand on hourly rate
  - 1 or 3 - year commitment period
- spot
  - 90% discount
  - bid for unused capacity
  - loosing them if someone willing to pay more
- dedicated hosts
  - on demand
  - reservation for 1 or 3 years
 
### Computer - Lambda & ECS
- Lambda:
  - pay per call
  - pay per duration
- ECS:
  - you pay for aws resources stored and created in your app
- Fargate
  - pay for vCPU and memory

### Pricing for storage S3
- based on classes
- based on number and size of the objects
- number and type of requests
- data transfer out of the s3 region
- s3 transfer acceleration
- lifecycle transitions
- EFS is similar
- 
### Pricing EBS:
- volumne type
- provisioned volume, pay even if you dont use it
- IOPS
  - general purpose: included
  - provisioned IOPS
  - magnetic: number of requests
- snapshots:
  - added cost per GB per month
- data transfer out of the EBS
- 
  
