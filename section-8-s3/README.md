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

