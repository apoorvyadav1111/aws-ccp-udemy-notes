# Section 4: EC2 Elastic Computed Cloud
---

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

# 33: AWS Budget Setup
Using Root,
- Click on the account name in the top navigation bar
- Budget and Planning > Budgets > Create a budget
- Select Default options, give ur email and click ok

You will get notified of a cost incurrance of 0.01$.
- Usually u get notified, if you spend 70% of the budget, you are expected to spend 100% of the budget, and when you actually spend all of the budget

---

# 34: EC2 Basics

- Most popular
- IAAS
- Rent VM: EC2
- Store data  on virtual drives EBS
- Distributing Load accross machines using EBS
- Scaling automatically using an auto scaling group ASG

### EC2 Sizing and config
- OS: Windows, Linux, Mac
- CPU, RAM, Storage (attach via network (EBS, EFS) or Hardware attach (EC2 instance store))
- Network Card, speed of the card, public IP address
- Firewall Rules: Security Group
- Bootstrap script, config at first launch, EC2 user data

### EC2 User Data
- run when machine starts, runs only once.
- to automate boot tasks such as
  - install updates
  - install software
  - download files from the internet
- runs with the root user

### EC2 Instance Types

Instance | Cpu | mem (GiB) | storage | n/w performance | ebs bw (mbps) | 
--- | --- | --- | --- |--- |--- |
t2.micro | 1 | 1 | EBS only | low to moderate | |
t2.xlarge | 4 | 16 | EBS only | moderate | |
c5d.4xlarge | 16 | 32 | 1 x 400 NVMe SSD | up to 10gbps | 4750 |
r5.16large | 64 | 512 | EBS Only | 20Gbps | 13600 |
m5.8xlarge | 32 | 128 | EBS Only | 10Gbps | 6800 |

- t2.micro is part of the free tier for 750 hours

---

# 35: EC2 instance with user data for have a website hands on

Key takeaways:
- can choose from 1000 of images
- architecture
- instance types (t2.micro is free + t3 is t2 is not available)
- key pair for login
  - create a key
  - select rsa
  - select .ppm if mac, linux or windows 10+
- check the allow Http traffic from internet in network
- click on advanced and scroll down to the user data
- paste the start up code here
- Click Launch Instance
- Open public ip with http to check out our webpage

public ip address is ephemeral hence it changes upon restarting the instance.

---

# 36: EC2 Instance types

- https://aws.amazon.com/ec2/instance-types/
- Naming conventions:
   m 5 . 2xlarge
  - m: instance class
  - 5: generation
  - 2xlarge: size within instance class
- General Purpose
   - web servers, code repos
   - balance between compute, memory, network
   - name: t or m
- Compute Optimized
  - high performance cpus
  - batch processing
  - media
  - web servers
  - hpc
  - gaming servers
  - name: C
- Memory Optimized
  - large data sets in memory i.e. ram
  - in-memory databases
  - distributed web cache stores
  - high performance dbs
  - apps performing real time processing of unstructure data
  - name: R, x, z
- Storage Optimized
  - large data in local storage
  - OLTP systems
  - Redis type 
  - warehousing
  - DFS
  - name: I,d, h1
 
Instance | Cpu | mem (GiB) | storage | n/w performance | ebs bw (mbps) | 
--- | --- | --- | --- |--- |--- |
t2.micro | 1 | 1 | EBS only | low to moderate | |
t2.xlarge | 4 | 16 | EBS only | moderate | |
c5d.4xlarge | 16 | 32 | 1 x 400 NVMe SSD | up to 10gbps | 4750 |
r5.16large | 64 | 512 | EBS Only | 20Gbps | 13600 |
m5.8xlarge | 32 | 128 | EBS Only | 10Gbps | 6800 |

---

# 37: Security Groups & Classic Ports Overview

- fundamentals of the network security of the aws
- how traffic is allowed in or out of our ec2 instance
- contain only **allow** rules
- can reference by IP or by security group

### Deeper Dive
- act as a firewall
- they regulate
  - access to ports
  - ip range auth
  - control of inbound n/w (from other to the instance)
  - control of outbound n/w (from instance to other)

### Good to know
- can be attached to multiple instances
- locked down to a region or vpc
- does live outside the instance
- one SG for SSH access is a good practice
- if your apps is timed-out, its a SG issue
- if you get connection refused, then its an app error
- all inbound traffic is blocked by default
- all outbound is authorized

### Referencing from another SG
When we allow another SG, any instance with that SG are allowed for inbound access. you dont have to worry much about IP address

### Classic ports to know
- 22: ssh, login to linux instance
- 21: ftp
- 22: sftp,upload files using ssh, secure
- 80: HTTP, access unsecured websites
- 443: https: access secured websites
- 3389: RDP, login to windows instance

---

# 38: Security Groups hands-on
- EC2 > Security Groups
- Time out means mostly SG issue

---




