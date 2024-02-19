# Section - 3 
[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)
---
### Traditional IT Overview

- Networks: cables, routers and serves connected to each other
- Router: n/w device that forwards the data between the computer networks. They know where to send the packet.
- Switch: Takes a packet and send it to the correct server/client on your network

#### Old way
- Old way to create a website was to create it in home/garage.
- Create data center when scale.
- Needs power
- cooling
- maintenance
- upgrade and scaling is limited
- Constant monitoring
- so on.

All this when externally managed is broadly called cloud.

---
# What is Cloud computing?

- on demand delivery of resources
- pay as you go
- provision the right size and type
- access them instantly as you want them
- UI based access

### New way for IT
- Use cloud instead of data center
- some example: gmail, dropbox, netflix (entirely on aws)

### Deployment models of the cloud
- Private: Single organization, private, ex: rackspace. secure
- Public: AWS, Azure, GCP. resources are owned by the providers and delivered to the uses over the internet.
- Hybrid: Mix of both. Keep some on premise and extend some on the cloud.

### 5 characteristics of the cloud:
- on demand
- broad network access
- multi tenancy and resource pooling: others can share the infra w/o comprimising the security
- elastic and scalable
- Measured service and pay as per use

### 6 Advantages:
- Trade Capital Expense (CAPEX) for operational expense (OPEX)
    - on demand, dont own hardware
    - reduced total cost of ownership and opex
- Benefit from the massive economies of scale
  - reduced prices
- Stop guessing capacity
  - scale automatically based on the usage
- Increase speed and agility
- Go Global in minutes

### Problems Solved
- Flexible
- Cost Effective
- Scalable
- Elastic
- High Available
- Agile

---

# Types of Cloud Computing
- IAAS
  - blocks for the cloud IT
  - networks, computers, data storage
  - flexible
- PAAS
  - no worries about the infra
  - focus on deployment and management
- SAAS
  - Completed product being managed by the provider
 


### Pricing of the Cloud
- Compute: pay for the compute time
- Storage: data stored in the cloud
- Data Transfer: into the cloud is free

  ---

# AWS Cloud Overview
- 2019, $35B revenue
- 47% market, in 2019
- over 1M active users


### Use cases
- scalable apps
- IT, backup, analytics
- Hosting
- Gaming servers

### Global Infra
- AWS Regions
  - all around the world.
  - ex: us-east-1, eu-west-3
  - cluster of the data center
  - most services are region-scoped
  - How to choose an aws region?
    - compliance
    - proximity to the users
    - availability of the services
    - pricing vary region to region
- AWS Availability Zones
  - Each region have minimum 3 az and maximum 6 az
  - each az have one or more discrete data centers with redundant power, networking and connectivity
  - isolated from disasters
  - connected with high bandwidth ultra low latency network

- AWS Data Centers
- AWS Edge Locations
  - 400+ points of presence in 90+ cities in 40+ countries

---

# Shared Responsibility Model & AWS Acceptable Policy

- Customer is responsible for the security **in** the cloud
  - data
  - encryption: client, server, network traffic
  - access: platform, apps, identity
  - firewalls: OS and Network
- AWS is responsible for the security **of** the cloud
  - software
  - resources
  - infra
  - regions, AZs, edge locations

  When you use aws, you agree to their usage policy, which states not to do bad stuff using them.

--- 

# Tour of the console and Services in AWS

Key points
- Route 53 is kind of exception when it comes to region as most services are region bound but not route 53, which is global
- Aws global infra and regional availablity here: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/?p=ngi&loc=4

  
