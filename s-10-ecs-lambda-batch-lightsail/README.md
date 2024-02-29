# Section 10: ECS, Lambda, Batch, Lightsail

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
