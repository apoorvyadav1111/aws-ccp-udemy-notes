# Section 8: Amazon S3

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---
# 71: S3 Overview
- main building blocks of AWS
- infinite scaling

### Use Cases:
- backup/ storage
- disaster recovery
- archive
- hybrid cloud storage
- app hosting
- media host
- data lakes & big data
- s/w updates
- static websites
- ex: Nasdaq stores 7 years

### Buckets:
- stores objects (files) in buckets (directories)
- must have globally unique name across all regions all accounts
- buckets are defined at the region level
- Name
  - no upper case, no undescore
  - 3-63 chars long
  - not an Ip
  - must start with lowercase letter /number
  - not start with xn--
  - not end with -s3alias

### Objects:
- have a key
- key is the full path
- key is prefix + object name
- aws s3 not have directory concepts
- just keys with long name and /
- Object values are content
  - max size is 5TB
  - if more than 5GB then use multipart upload
- metadata: list of text key/ value pair - system or user metadata)
- tags useful for security/lifecycle
- version ID: if enabled

---

# 72: S3 hands on

- go to s3 > Create Bucket
- give a unique name
- choose a region
- disable ACL
- set all other default

in the view,we can see all the buckets in all regions but buckets are confined to one region only

- upload a file
- public url should not work for now
- create a folder named images
- upload another image in new folder

---

# 73: S3 Security: Bucket Policy

- User Based:
  - IAM policies: which api calls should be allowed for a specific user from IAM
 
- Resource Based:
  - Bucket Policies: bucket wide rules from s3 console, allows cross account
  - Object Access Control List (ACL): finer grain (can be disabled)
  - Bucket Access Control List (ACL): less common (can be disabled)
- IAM Principal can access an s3 object if:
  - IAM permissions allow it **OR** the resource policy allows it
  - **and there is no explicit deny**
- Encryption

### S3 Bucket Policy
- json based policies
  ```
  {
    "Version":"2012-10-17",
    "Statement":[
      {
        "Sid":"PublicRead",
        "Effect":"Allow",
        "Principal":"*",
        "Action":[
          "s3.GetObject"
        ],
        "Resource":[
          "arn:aws:s3:::example/*"
      ]
    }
  }
  ```
  - Use s3 bucket policy to force objects to be encrypted at upload
  - grant access to another account
 
- IAM policy to user to allow access to the s3 bucket
- for ec2 instance: use IAM roles and do not use IAM user.
- Cross account access: use bucket policy, can allow this access for that iam user

### Bucket Settings for Block Public Access
- Even if public bucket, you keep settings on, it will not be public
- can set this as account level

---

# 74: S3 Security: Bucket Policy Hands on
- Go to the Bucket > Permissions > Edit "Block public access (bucket settings)" > Uncheck All
- Go to the Bucket Policy > Edit > Policy Generator
- Select type of policy as "S3 bucket policy"
- Principal: "*"
- Actions: GetObject
- Resource: get the arn from the bucket policy page and append "/*" at the end
- Generate, copy and paste the policy and save changes
- Check if the object is now public

---

# 75: S3 Website Overview
- static website
- url will depend on the region

---

# 76: S3 Website Hosting Hands On

- Go to bucket > properties > scroll down to the website hosting
- Click Edit and enable it > 
- Upload index.html
- Go back to properties and in the website hosting click on the public URL

--- 

# 77: S3  Versioning Overview
- version files
-  have to enable at the bucket level
- same key overwrite will change the version: 1,2,3
- protect from delete
- easy roll back
- any file before enabling version will have version null
- any versions after disabling versioning will be kept

---

# 78: S3 Versioning Hands On

- Go to bucket properties > Versioning > enable
- Lets update the website HTML and reupload
- Check the website
- Check the versions
- Click show versions, if not then only marker is deleted and not permanently deleted
- We can rollback by deleting the newer versions
- Delete Coffee.jpg w/o show versions
- Now we see an image issue
- Click show versioning > find the delete marker > delete it
- Now we restored the image

---

# 79: S3 Replication Overview

- two flavors: CRR & SRR
- cross-region replication and same region replication
- need to have versioning enabled in both src and dest buckets
- buckets can be in different accounts
- copying is async
- must give proper IAM permission to S3
- Use Case
  - CRR: compliance, lower latency, replication across accounts
  - SRR: log aggregation, live replication between prod and test
 
--- 

# 80: S3 Replications Hands ON
- Create 2 buckets with versioning enabled in different regions/az
- add item in src bucket
- go to management > replication > create replication rule
- add name, choose scope, add dest bucket,
- it will ask if old objects need to be replicated, your choice
- add new item
- allow some time and check in the dest bucket. Notice the versions are the same across the bucket.

--- 

# 81: S3 Storage Classes
- Standard
- Standard - IA
- One Zone - IA
- Glacier Instant Retreival
- Glacier Flexible Retreival
- Glacier Deep Axv
- Intelligent Tiering
can move among classes manually or using s3 lifecyle config

### s3 durability and availability
- Durable:
  - High durable: 11 9's across multi AZ
  - if u store 10 mil object, you can on average expect one object loss once every 10000 years
  - same for all storage classes
- Available
  - S3 standard have 99.99% availability, 53 mins per year unavailable

s3 standard |       s3 standard IA  | s3 one zone IA |
---|---| --- |
99.99% av | 99.9% av | 99.5%  |
freq access | less access than standard, cheaper | data lost when AZ destoyed
low latency & high thruput | | 11 9s durable in one zone | 
sustain 2 concurrent facility failures | | |
big data analytics, mobile and gaming apps, content dist | disaster recovery, backups | store secondary copies of on premise data or something u can recreate |

### Amazon s3 glacier storage classes 
- low cost for archiving and backup
- price for storage + data retrieval
- S3 Glaciel Instant Retrieval
  - millisecond retrieval, great for data accessed once a quarter
  - minimum storage duration of 90 days
- S3 Glacier Flexible Retrieval (Formarly S3 Glacier) Minimum storage duration for 90 days
  - expedited ( 1 to 5 mins)
  - standard ( 3 to 5 hours)
  - Bulk (5 to 12 hours) free
- S3 Glacier Deep Archive - for long term storag
  - standard : 12 hours
  - bulk: 48 hours
  - minimum storage days of 180 days
 
### S3 intelligent tiering
- small monthly monitoring and auto tier fee
- moves object automatically based on usage
- no charges in s3 intelligent tiering
- no retrieval charges

- Frequent Access Tier (automatic): default tier
- infrequent A T (auto): objects not accessed for 30 days
- Archive Instant A T (auto): objects not accessed for 90 days
- Archive A T (optional): configurable from 90 days to 700+ days
- Deep Archive A T (optional): configurable from 180 days to 700+ days

### S3 Price Comparision
- Cheapest and instant is One Zone IA


**IMP: Study from AWS for new classes**
---

# 82: Storage Classes Hands On
- Create a new bucket with defaults
- Upload a file in the bucket, in properties > select Standard-IA
- Can go to the object's property and edit the storage class, eg to One Zone IA
- Can create a lifecycle rule in bucket's properties > create a lifecycle rule

--- 

# 83: S3 Encryption
- Server Side encryption
  - when uploaded, an object is encrypted by server
- Client Side Encryption: from client

Both options are there, but server side is by default enabled

---

# 84: IAM Access Analyzer for S3
- ensures that only intended people have access to your s3 buckets
- evaluates s3 bucket policies, s3 acls, s3 access point policies
- powered by IAM access analyzer

---

# 85: Shared responsibility model for S3
- AWS
  - Infra, global security, durability, availability, sustain, concurrent loss of data in two facilities
  - configuration and vulnerability analysis
  - compliance validation
- Personal
  - S3 Versioning
  - S3 Bucket Policies
  - S3 Replication Setup
  - Logging and Monitoring
  - S3 storage Classes
  - data encryption at rest and in transit

--- 

# 86: AWS Snow Family
- highly secure, portable device to **collect and process data at the edge and migrate data in and out of the aws**
- Data Migration:  Snowcone, Snowball edge and snowmobile
- Edge Compute: Snowcone and Snowball edge

### Data Migrations with AWS Snow Family
- 100TB on 100Mbps -> 12 days
- Challenges:
  - limited connectivity
  - limited B/W
  - high n/w cost
  - shared b/w
  - connection stability
- snow family are offline devices to perform data migrations
- if it takes more than a week for uploading, use snow mobile

- AWS delivers, and we ship back to the AWS Facility
- They take and plug into their infra

### Snowball Edge: up to 24 TB use
- TBs or PBs of data in/out of AWS
- Pay per data transfer job
- provide block storage and s3 compatible object storage
- Snowball storage optimized: 80TB of HDD
- Snowball Compute optimized: 42TB of HDD or 28TB of NVMe capacity
- Use Case: large data cloud migration, DC decommission, disaster recovery

### Snowcone and Snowcone SSD up to 80TB use
- small portable computing rugged and secure
- light 2.1 kgs 4.5 lbs
- used for storage, edge computing and data transfer
- snowcone - 8TB of HDD
- snowcone ssd - 14TB of SSD
- use snowcone when snowball does not fit (space)
- need your own battery / cables
- can be sent back to AWS or connect it to internet and use **AWS Datasync** to send data
- 

### Snowmobile upto 1 EB
- transfer: 1EB = 1000PB = 1MilTBs
- Each snowmobile have 100PB Capacity use multiple in parallel
- High security, temp controlled, GPS, 24/7 video surveillance
- Better to use when have more than 10 PB of data
- 

### Snowmobile usage process
- request
- install snowball client/ aws opshub on server
- connect the snowball and copy using the client
- ship back the device
- data is loaded
- complete wipe

### Edge Computing
- process data while being created at the edge location
- edge location: remote, disconnected from internet or computing power, ex: ships, mines, trucks
- we setup snowball or snowcone
- uses:
  - preprocess data
  - ML at the edge
  - transcoding media stream
- then ship back to AWS

- Snowcone & snowcone SSD
  - 2 CPUs, 4GBs of memory, wired or wireless
  - USB-C power using a cord or optional battery
- Snowball Edge - Compute optimized
  - 104 vCPUs 426 GB of RAM
  - Optional GPU
  - 28TB NVMe or 42 TB HDD
  - Storage clustering is available

- All : can run ec2 instances & AWS lambda fx using AWS IoT greengrass
- long term deployment options: 1 or 3 years discounted pricing

### AWS OPSHUB
- historically, you needed aws cli
- now we can use **opshub** to manage the snow family device
- unlocking and configuring single or clustered device
- transfer files
- launch and manage instances
- monitor device metrics
- launch compatible aws services like ec2 instances, aws datasync, NFS

---

# 87: AWS SnowFamily Hands On
- Go to Snow Family Console
- click order
- give jobname
- choose job type
- choose snow device
- pricing option
- add ami
- select buckets
- choose the encryption key
- grant access and create a service role
- choose address, ship speed
- 

---

# 88: AWS Snowball Edge Pricing

- usage of the device + data transfer  out of the AWS
- data in to AWS is **free**
- on demand
  - one time service fee per job
    - 10 days of usage for snowball edge storage optimized 80TB
    - 15 days of usage for snowball edge storage optimized 210TB
  - shipping days are not included in 10 or 15 days
- committed up-front
  - pay in advance: monthly, 1 year or 3 years usage (edge computing)
  - up to 62% discount
 
---

# 89: Storage Gateway Overview

- AWS is pushing for hybrid cloud
- Can be due to
  - long cloud miggrations
  - security
  - compliance
  - IT strategy
- S3 is proprietary tech, so how to expose it?
- AWS Storage Gateway:

- Storage Cloud Native options
- Block: EBS, EC2 instance store
- File: EFS
- Object: S3, Glacier

- Storage Gateway b/w on premise data + cloud data in S3
- use case: disaster recovery, backup and tiered storage
- Types:
  - File gateway
  - Volume gateway
  - Tape Gateway
- from on premise to EBS, S3, Glacie

---
