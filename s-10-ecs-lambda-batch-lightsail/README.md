# Section 10: ECS, Lambda, Batch, Lightsail

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# 111: What is Docker?
- apps are packaged in a container that can run on any OS
- can scale up and down quickly
- Docker as an OS:
  - can run as java and node on EC2
- stored in docker repositories
- private: Amazon ECR
- Docker Vs VMs
  - sort of virtualization but not
  - resources shared with the host, can have many containers on many host
  - in VM, the VM runs on host and not share resources, Apps run over them

---

# 112: ECS, Fargate & ECR Overview
- Elastic Container Service
  - launch docker on AWS
  - must provide and maintain infra yourself, the ec2 instance
  - aws takes care of the starting and stopping containers
  - has integrations with ALB to know where to start docker
- Fargate
  - do not provision the infra
  - simpler
  - serverless
  - aws runs the containers based on the need as per CPU/RAM
- ECR
  - Elastic Container Registry
  - storing docker images
  - private
  - can be run by ECS or Fargate
 
---

# 113: Serverless Introduction
- dev dont manage the servers
- just deploy code or functions
- initially, serverless  ==  FAAS
- pioneered by the AWS lambbda , now dbs, messaging, storage etc
- it means you dont manage the servers, they are there
- so far: s3, dynamoDB, Fargate, lambda functions

---

# 114: Lambda Overview
- EC2:
  - virtual servers in the cloud
  - limited RAM & CPU
  - continuously running
  - scaling means intervention to add/remove servers
- Lambda
  - virtual fxns
  - limited by time up to 15 mins
  - no servers to manage
  - run on demand
  - autoscale
  - 

### Benefits
- pay per request and compute time
- free tier of 1M free requests and 400,000GB seconds of compute time
- integrated with whole of AWS Suites
- Event driven: fxns invoked by AWS
- fully integrated with many languages
- 10GB of Ram

### Lang support
- Node
- Python
- java
- c#
- golang
- ruby
- community supported like rust

- lambda container image
  - must implement the lambda runtime api
  - ecs/fargate is preffered for running arbitrary docker images
 
### Example:
- serverless image thumbnail creation server
- s3 buckets trigger a lambda fxn and push the thumbnail to s3 and metadata into dynamodb
- fully event driven

### Example:
- serverless cron job
- cloudwatch events => (trigger every hour) AWS Lambda Fxn


### Pricing
- pay per call, 1mil are free
- $.20 per 1M req
- pay per duration: 400GB s of compute time free, $1.00 per 600000GB seconds
---

# 115: Lambda Hands On

- go to lambda
- change the url path to /begin
- check out how it works
- click run
- click "next: respond to events"
- Click next and see the cost
- Click create a function
- Choose "use a blueprint"
- choose python
- name > demo-lambda
- create a new role
- Create function and checkout the code source
- Click on test
- create a new test event > give values  > create
- Go to configuration
- Go to Cloudwatch logs
- logs of the invocation of the function
- If any changes are made, click deploy
- The role created, have access to create cloudwatch logs

---

# 116: API Gateway Overview

- building serverless API
- we need external clients to access the lambda fxns
- it proxies requests to lambda requests
- fully managed service for developers to create, publish monitor, and secure APIs
- serverless and scalable
- security, auth, api throttling, api keys, monitoring

---

# 117: Batch Overview
- fully managed
- batch processing at any scale
- run 100000 of computing jobs on AWS
- a batch is a job with a start and end
- will dynamically launch of ec2 instances or spot instances
- aws batch provisions right amount of cpu/mem
- you submit the job and aws batch does the rest
- batch jobs are defined as docker images and run on ECS
- helpful for cost optimizations and focussing less on the infra

Lambda | Batch
---  | --- 
time limit | no time limit
limited runtime | any runtime as long as its packaged as docker image
limited temp disk space | rely on EBS / Instance store for disk space
serverless | relies on EC2 (can be managed by AWS)

---

# 118: Lightsail Overview
- virtual servers, storage, dbs, networking
- low and predictable pricing
- simpler alternative to ec2, rds, elb, ebs, route 53
- need little cloud experience
- use case:
  - simple web app
  - dev/test app
- high av but no auto scaling and limited AWS integrations

---

# 119: Lightsail Hands on 
- select OS
- select template
- select launch script
- change the ssh pair
- less cost plans
- simple to do
- 
---

# 120: Other compute summary


---

