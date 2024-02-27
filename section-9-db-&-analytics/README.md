# Section 7: Database & Analytics

# 91: Database Introduction
- storing data on disk(efs,ebs,ec2 is,s3) can have its limits
- in db:
  - you can structure the data
  - build indexes
  - define relations
- optimised for a purpose

### Relational DB
- links b/w tables

### NoSQL DB
- non relational
- built for specific data models and have flexible schemas
- benefits:
  - flexible
  - scalable
  - high-performance: optimized for a specific data model
  - highly functional optimized for data
- ex: key value, document, graph, in memory, search databses

### Shared responsibility model 
- aws offers to manage different dbs
- benefits:
  - quick proivisioning, high AV, scaling
  - auto backup and restore, operations, upgrades
  - OS patching is handled by AWS
  - monitoring, alerting

- we can run most dbs on ec2 but we will have to all the work ourselves

---

# 92: RDS & Aurora Overview

### RDS
- relational
- sql like syntax
- managed db service
- supports
  - postgres
  - MySQL
  - MariaDB
  - Oracle
  - MS SQL Server
  - IBM DB2
  - Aurora (AWS proprietary)

### Advantages of RDS vs deploying a DB on EC2
- managed service
  - auto provision, os patching
  - continous backup and restore to specific timestamp
  - monitoring db
  - read replicas
  - multi AZ for disaster recovery
  - maintaince windows for upgrades
  - scaling : vertical and horizontal
  - storage backed by **EBS**
- **cannot ssh in to db**

### RDS Solution Arch
```
                      ________>[EC2]________
                    /                     \
---- > | ELB | --------------->[EC2]--------- > [RDS] 
                    \_________>[EC2]---------/
                            (possibly ASG)
```

### Amazon Auroro
- not open source
- postgres and mysql
- cloud optimized and claims 5X performance improvement over mysql on rds and 3X over postgres over RDS
- grows auto in steps of 10GB up to 128TB
- costs more than 20% more than RDS
- not in free tier

### Amazon Auroro Serverless
- auto data instantiation and scaling based on usage
- PostgreSQL and MySQL are both supported
- no capacity planning needed
- least management overhead
- pay per second, can be more effective
- good for infrequent, intermittent, unpredictable workload
```
                              [Client]
                                  |
                            [ proxy fleet ]
                          (managed by aurora)
                                  |
      --------------------------------------------------------------
      |          |          |        |          |        |         |
  [Aurora]   [Aurora]  [Aurora]  [Aurora]  [Aurora]  [Aurora]  [Aurora]
<==========================Shared Storage Volume=======================>
```

---

# 93: RDS Hands On

- go to RDS > Create A DB >
- Standard and Free, choose standard
- chose MySQL
- chose free tier
- give name and password
- create new vpc
- select Yes for public access
- Create database

- go to actions
- take snapshots
- give a name
- cant proceed if db is in **backing up stage**
- we can then restore the snapshot
- you can create a copy of the db using snapshot
- you can share the db

--- 

# 94: RDS Deployments Options
- read replicas:
  - create more reading replicas,
  - can create up to 15 read replicas
  - data is written only to one main db
- MultiAZ:
  - incase of AZ outage
  - replication cross AZ
  - will be a failover DB
  - if main crashes, RDS triggers failover
  - can have only 1 AZ as failover AZ
- multiregion
  - read replicas
  - writes need to happen in cross region too
  - disaster recovery
  - local performance low latency
  - replication cost to transfer data
 
---

# 95: Elasticache Overview
- managed redis/memcached
- high performance/ low latency
- help load of db for read intensive workloads

---

# 96: DynamoDB Overview
- Fully managed highly AV, with replication across 3 AZ
- NoSQL db
- distributed serverless database
- mil of requests per seconds, trillions of rows, 100s TB of storage
- fast and consistent in performance
- single digit millisecond latency
- integrated with IAM for security, auth and administrations
- standard & IA Class
- key value data is stored
  - primary key: partition key + sort key (optional)
  - attributes
 
### DynamoDB Accelerator DAX
- fully managed in memory cache for DyanoDB
- just for DynamoDB
- 10x performance improvement (microseconds latency)
- secure, high scale & AV

---

# 97: DynamoDB Hands On
- Create table
- give partition key
- choose defaults
- create

All data is in one db and no way to join it

---

# 98: DynamoDB Global Tables
- accessible with low latency in multiple regions
- up to 10 regions
- users can write into any region and is actively synced in anther region

---

