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
  - select .pem if mac, linux or windows 10+
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

# 39: SSH Overview

- SSH can be used using mac, linux, Windows 10+
- Putty can be used to connect via any windows
- EC2 instance connect can be used for any operating system, but only works for Amazon Linux

**will skip next lectures for windows and windows 10**

---

# 40: How to SSH using Linux or Mac

- Create a folder named ```aws``` or similar
- move the .pem file downloaded before into this folder
- copy public ip address of the ec2 instance running
- ensure that inbound traffic for port 22 is allowed for ssh
- open a terminal in the folder created
  - enter command ```ssh -i <filename>.pem ec2-user@<public-ip>```
  - We fill face an error saying bad permissions
  - Change the permissions using: ```chmod 0400 <filename>.pem```
  - try again, you should be logged in
  - type ```exit``` to exit

Remember, restarting your instance may change ur public IP, hence, you have to note the IP everytime you do ssh into ur instance

---

# 44: EC2 Instance Connect

alternative to ssh for connecting to ec2.

- Go to EC2 > click on the instance > Connect on the upper nav
- Click EC2 instance connect
- Click on connect

It opens a new tab. Its just as we are SSHing the instance from the terminal.

- It still requires us to configure the security group to accept SSH inbound traffic on port 22.

---

# 45: EC2 Instance Demo
Use IAM user
- Connect to the instance using anything
- it has aws cli installed
- But we cannot use it until we configure it.
- But configuring it requires us to use access key and secret key, which should not be entered in the instance. It will allow anyone using the ec2 instance run commands using your keys
- Instead do the following:
  - Go to IAM and create a role as per the needs, we created a demo role with one IAMReadOnlyAccess policy
  - Go to the instance, click on actions > security > modify iam role > choose the role > update / save
- now we can run commands that are allowed as per the role attached

---

# 46: EC2 Instance Purchasing Options
- On-Demand: short workload, predictable pricing, pay by second
- Reserved: 1 & 3 Years
    - long workloads
    - convertible reserved instances: long workloads with flexible instances
- Savings Plans: 1 & 3 Years
    - commitment to an amount of usage, workload
- Spot Instances: short workloads, cheap, but less reliable, can lose them
- Dedicated Hosts: book an entire physical server, control instance placement
- Dedicated Instances: no other customers will share your hardware
- Capacity Reservations: reserve capacity in a specific AZ for any duration

### EC2 on demand
- linux/windows: billing per second
- all others: billing per hour
- highest cost
- no long term commitment

  
### Reserved Instances
- up to 72% discount as compared to ON-demand
- reserve specific instance attributes
- period: 1 year or 3 years
- payment: no upfront, partial, or all upfront
- scope: zone or region
- steady-state usage apps
- can buy or sell in AWS Marketplace
  - Convertible reserved: can change the attributes like type, family, OS, scope and tenancy
  - up to 66% discount

### EC2 Saving Plans
- based on long term usage (up to 72%)
- Commit to certain type of usage ($10/hr for 1 or 3 year)
- Usage beyond the plan is billed on demand
- locked to instance family & Region
- flexible in size, OS, tenancy

### Spot Instances
- up to 90%
- can lose them any time
- workloads resilient to failures like batch, data analysis, image processing, distributed workload, workload with flexible schedule
- not suited for critical jobs/databases
**exam will test on this about what can be ran on these**

### Dedicated Hosts
- physical server with capacity full dedicated to ur use
- can cater to compliance requirements and existing software licences (per socket, per core, per VM software licenses)
- purchase:
  - on demand
  - reserve 1 or 3 years
- most expensive
- useful for software with BYOL model
- or strong compliance or regulation needs

### Dedicated Instances
- h/w is dedicated to you
- may share h/w with other instances in same account
- no control over instance placement

### EC2 capacity reservations
- reserve on-demand instances capacity in a specific az for any duration
- you will always have ec2 instance capacity when u need
- **no time commitment, no billing discount**
- can combine with regional reserved instances and savings plans to benefit from billing discounts
- **charged with on-demand rate whether or not instances are running**

--- 

# 47: Shared Responsibility Model for EC2

AWS manages: Infra, isolation on physical hosts, replacing faulty hardware, compliance validation

You manage:
- SG Rules
- OS patches and updates
- software and utilities
- IAM roles attached to EC2
- data security on the instance

--- 

  



