# Section 8: Amazon S3

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
