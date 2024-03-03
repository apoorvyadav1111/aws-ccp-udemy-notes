# Section 6: EC2 Instance Store

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)


# 49: EBS Overview
- Elastic Block Store
- EBS Volume is a network drive you attach when ur instance run
- allows us to persist data
- only be mounted to **one instance at one time**
- bound to **one az**
- think of them network usb drive
- 30Gb of free EBS of type General Purpose SSD or Magnetic per month

### More
- Its a network drive
- bit latency
- can be detached and attached to another instance
- is locked to an AZ, hence cant be attached to instance in another AZ
- Have a provisioned capacity in GBS, IOPS
- get billed for all the provisioned capacity
- Can attach more than one EBS to one EC2 instance
- can leave them unattached

### Delete on Termination attribute
- when we create ebs volume while creating a ec2 instance, it means when we delete the instance, we delete the volume
- can be controlled by aws console/cli for modifying
- use case: save root volume upon termination

**EBS Multi attach feature in io1 and io2 allow themselves to be attached to more than one instance but they are out of the scope of this exam**

---

# 50: EBS Hands On
- Volumes > Create Volume
- Choose gp2/gp3
- Select 2 Gibs
- Select AZ same as your ec2 AZ
- Create Volume
- Select the Volume when created, click actions > attach volume
- Select the instance > click attach volume

Check the EC2 storage and now you will have two volumes
- You can create another volume with different AZ to see if you can attach to your ec2 instance. (we cant)

**When u delete the instance the volume you attach to, after instance creation, is by default saved on termination**

---

# 52: EBS Snapshot Overview

- make a backup of ebs volume at a point in time
- can do without detaching, but **recommended**
- can copy snapshot accross az or region
- **Can use snapshots to move ebs volume across the az or region by restoring it.**

### Features
- EBS Snapshot archive:
  - Move a snapshot to a **archive tier**,: 75% cheaper
  - Takes 24 to 72 hours to restore
- Recycle Bin for EBS Snapshot
  - Setup rules to retain deleted snapshot
  - specify retention from 1 day to 1 year

---

# 53: EBS Snapshots Hands On
- Click on Volume > Actions > Create Snapshots
- Go to the Snapshots > find the volume
- Check if its done 100%
- Click on the snapshot > copy snapshot > change the region

- We can recreate the volume from it
- Select the snapshot > Click actions > Create Volume from snapshots
- Can change AZ this time

### Create a retention rule
- Click on recycle bin
- Create a retention rule
- Select EBS Snapshots
- Select 1 Days
- select Unlock
- Create the rule

  Volumes in bin are billed the same rate as normal

---

# 54: AMI Overview

- AMI: Amazon Machine Image
- customization of an ec2 instance
- can be built for a specific region, can copy across the region
- launch ec2 instances from:
  - Public AMI: AWS Provided
  - Your own ami: make and maintain them ourselves
  - Launch from AWS Marketplace, someone else made
 
### Process
- Start an instance and customize it
- Stop the instance to preserve data integrity
- Build an AMI-  will also create EBS Snapshots
- Launch instances from other AMIs
  
---

# 55: AMI Hands On
- Create a EC2 instance just like before except use existing SG and omit the echo line in user data
- Click the Instance > Actions > Image and Templates > Create Image
- Give Name, keep everything same
- Create Image

- Go the AMIs and verify the image

### Launch Instance
- Select My AMIs this time
Now we have faster boot, setup on the first time.

---

# 56: EC2 Image Builder Overview

- Automate the creation of VMs or container images
- automate the creation, maintain, validate and test ec2 AMI

- It creates a Builder EC2 instance, Build components and create the AMI
- Then test it automatically by creating an instance
- checks if it runs, secure
- AMI is distributed to regions, (while AMI is not)
- Can run on a schedule, weekly or when packages are updated
- Free, only pay for underlying resources, if you create an instance during the process,you pay for it, you pay for AMI created and its storage

---

# 57: EC2 Instance Store

- EBS are nw drives, good but limited performance
- high performance hardware disks: EC2 instance store
- Better I/O
- great thruput
- If you stop the instance store, they are lost, they are ephemeral
- Good for buffer/cache/scratch data/ temporary content
- risks if hardware fails
- we need to do backups
- very high iops > ec2 instance store

---

# 58: EFS Overview

- network file systems
- Elastic File System
- can be mounted to 100s of EC2
- Shared NFS
- Can only work with Linux EC2 in multi AZ
- Highly available, scalable, expensive (3X gp2), pay per use, no capacity planning

### EBS vs EFS

 EBS | EFS 
 ---|---
 Need to make a snapshot to move to AZ, not a sync but a replica | Shared by everything mounted to it
 
 ### EFS Infrequent Access EFS-IA
 - Storage class that is cost optimized for files not accessed every day
 - up to 92% cost compared to EFS Standard
 - If enabled, then efs will move file automatically based on their last access time
 - depends on the lifecycle policy
 - ex: 60 days
 - transparent to the apps

--- 

# 59: Shared Responsiblity Model for EC2 Storage

AWS | EC2 Storage
---|---
Infra | Setttng up backup / snapshot procedure
Replication for EBS & EFS | data encryption
replace faulty hardware | responsible for any data on the drives
Employess should not have access | understand the risks of ec2 instance store

---

# 60: Amazon FSx Overview
- Launch 3rd party high-performance file systems on AWS
- Full Managed Services]
- FSx for Lustre, FSx for Windows File Server, FSx for NetApp on ONTAP

### Amazon FSx for Windows File Server
- full managed, highly reliable, scalable **windows** native shared FS
- Built on Windows File Server
- Supports SMB protocol & Windows NTFS
- integrated with MS-AD
- can be accessed from AWS or on premis infra

### Amazon FSx for Lustre
- full managed, highly performance, scalable for high performance
- Lustre : Linux + Clustre
- Machine Learning, Analytics, Video Processing, Financial modeling
- Scales up to 100s GB/s millions of IOPS, sub ms latencies

---

