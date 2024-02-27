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

    
                    
