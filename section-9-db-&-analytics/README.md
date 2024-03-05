# Section 9: Database & Analytics

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

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

# 99: Redshift Overview

- based on postgres, but used for OLAP
- load data per hour rather than every second
- 10X better performance than other, scale PBs of data
- Columnal storage
- Parallel Query Execution
- Has a SQL interface
- BI tools integrated with it like AWS Quicksight and Tableau

### Redshift serverless
- auto provision and scales data warehouse
- run analytics without managing infra
- pay for what you use
- use case: reporting, dashboarding, real time analytics

---

# 100: EMR Overview
- Elastic Map Reduce
- Hadoop Cluster/ Big Data
- made of hundreds of EC2 instances
- Apache Spark, HBase, Presto
- EMR, takes care of the provisioning and configuring
- Use case: data processing, ML, web indexing, big data

---

# 101: Athena Overview
- serverless query service to perform analytics against s3 objects
- uses standard sql
- supports csv, json, orc, avro, parquet (build on presto)
- price: $5.00 per TB of data scanned
- use compressed or columnar data for cost saving
- uses: BI, analyze and query VPC flow, Logs, cloudtrail trails etc

--- 

# 102: QuickSight Overview
- serverless, ml powered BI service to create dashboards
- fast, auto scale, embeddable, per session pricing
- uses:
  - Biz analytics
  - building viz
  - perform ad hoc analysis
  - get BI using data
 
- integrated with RDS, aurora, athena, redshift, s3

--- 

# 103: DocumentDB
- AWS implementation of MongoDB (noSQL)
- similar deployment concepts as Aurora
- Fully Managed, highly av with replication across 3 AZ
- auto-scales with step of 3GB
- mil of requests per seconds

---

# 104: Neptune Overview:
- fully managed graph database.
- high AV with 3 AZ up to 15 replicas
- build and run apps with highly connected datasets
- can store up to billions of relations and query the graph with ms latency
- great for storing knowledge graphs, recommendation engines, social network

---

# 105: Timestream Overview

- time series database
- fully managed, fast, scalable, serverless
- store/ analyze trillions of events per day
- built-in series analytics fxns

---

# 106: QLDB overview
- Quantum Ledger Database
- ledger is a book recording financial transactions
- fully managed, serverless, high av, replication across AZ
- used to review history of all the changes made to your application data over time
- immutable entries, cryptographically verifiable

---

# 107: Managed Blockchain Overview
- the difference is QLDB is centralized.
- Blockchain makes it possible to build apps where multiple parties can execute transactions without the need of trusted, central auth
- managed service to:
  - join public blockchain networks
  - create your own scalable private networks
- compatible with Ethereum and hyperledger fabric

---

# 108: Glue Overview
- managed ETL service
- useful to prepare and transform data for analytics
- fully serverless service
- can do it from S3 and RDS as source
- Glue data catalogs: catalog of databases
  - can be used by Athena, redshift, emr
---

# 109: DMS 
- data migration service
- extract the source db and insert into target DB
- quick, secure
- source db is av during the migration
- based on the tech of src db and target db: homogeneous and heterogeneous migrations (automatically converts the data)


---


