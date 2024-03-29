# Section 11: Deployments & Managing Infra

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# 121: CloudFormation Overview
- declarative way of outlining your aws infra for most resources
- cloudformation creates the infra in the config and order you specified
- infra as a code
- cost is easy to track as all of the items in a stack are tagged
- you can estimate the costs from the template
- you can provision and delete and reprovision infra automatically

### Benefits:
- productivity
  - create infra on the fly
  - diagram of the template
  - declarative programming
 
- existing templates on the web
- exisiting documentations
- supports most of the resources
- add custom resources

### Stack designer

---

# 122: CloudFormation Hands ON
- go to cloudformation
- create a stack
- go to us-east-1
- choose template is ready
- upload a template
- View in designer
- click next
  - Name it democloudformation
  - tag it > demoCF
  - Click next and create stack

- to update it> template > modify> upload
- it will show changes in change set preview
- it will remove the old infra > clean up after itself
- We can delete the infra  by just deleting the stack

---

# 123: CDK Overview
- use programming languages to create a template
- CDK compiles the code to yaml/json
- great for lambda fxns
- great for docker container in ECS/EKS

---

# 124: Beanstalk Overview
- typically, client requests to ELB which forward to multiple ec2 in a ASG target group. which are then connected to DBs and cached
- Dev problems:
  - manage infra
  - deploy code
  - configure database, LBs
  - scaling concerns
 
- most web apps have some arch
- beanstalk is a centric view for deploying an app
- its a paas
- we still have control
- using it free, but pay for underlying services
- managed service
  - instance configuration/ Os is handled by beanstalk
  - deployment strategy is configurable but perfomed by BeanS
  - capacity provisioning
  - LB and ASG
  - health monitoring and responsiveness
- only responsiblity dev have is code
- three arch models
  - single instance deployments: good for dev
  - LB+ASG: for preprod and prod
  - ASG: for non web apps in production
- supports:
  - go, java, php python etc..
- health monitoring:
  - health agents on ec2 which pushes metrics to cloudwatch
  - checks for health and published health events
    
---

# 125: Beanstalk Hands On
- Go to the service
- create application
- choose: web or worker > web
- give a name
- give a env name
- choose a platform > choose a default
- choose app code > sample
- presets > single instance
- Click Next:
  - Configure service access (IAM role allowing beanstalk to do what it needs to do)
  - create a new role
  - create a new ec2 instance profile
    - IAM console
    - create roles
    - select aws service
    - ec2
    - next:
    - add policy: search for beanstalk> add web, worker and multi container tier
    - next
    - add name
  - now you will have a role to add
  - click skip to review (chooses default)
  - submit
 
- go to events, coming from cloudformation (a stack is created by beanstalk)
- can upload a new version easily
- we can create multiple environment
- centered around code and enviroment
  
---

# 126: CodeDeploy Overview
- deploy our app automatically
- v1 => v2
- works with ec2 instances
- works with on premises servers
- hybrid service
- serves/instances must be provisioned and configured ahead of time with the codedeploy agent

---

# 127: CodeCommit Overview
- like github
- store within aws
- source control service that hosts git based repos
- makes it easy to collaborate with others on code
- the code changes are automatically versioned
- benefits:
  - fully managed
  - scalable and highly av
  - private, secured, integrated with aws
 
---

# 128: CodeBuild Overview
- build in the cloud
- compiles the source code, run test, and produces packages that are ready to be deployed
- benefits:
  - fully managed, serverless
  - continously scalable and high av
  - secure
  - pay as you go - pay for the build time

---

# 129: CodePipeline Overview
- code => build => test => provision => deploy
- basis for CICD
- benefits:
  - fully managed
  - compatible with many product
  - fast dilivery and rapid updates
 
---

# 130: CodeArtifact Overview
- software packages that depend on each other to be built (code dependencies)
- storing and retrieving these dependencies is called artifact management
- usually you setup you own artifact management system
- codeartifact is a secure, scalable and cost effective artifact management for software development
- works with common dependency management tools such as maven, gradle, npm, yarn
- devs and codebuild can fetch directly

---

# 131: CodeStar Overview
- unified UI to easily manage software dev activites in one place
- creates all the code* service for you.
- can edit the code using cloud9 directly on aws.

---

# 132: AWS Cloud9
- Cloud IDE
- within web
- pair programming

---

# 133: CodeStar & Cloud9

- Go to Code commit
- Checkout all the tools
- Use Codestar
- create a project
- create a service role
- choose a template > Flask
- Give a name
- Create a key pair
- Setup up cloud9
- create a cloud9 environment
- Can integrate JIRA

---

# 134: Systems manager (SSM)
- manage ec2 instances and on-premise systems at scale
- another hybrid aws service
- suite of 10+ products
- features are:
  - patching automation for enhanced compliance
  - run commands across an entire fleet of service
  - store parameter config with SSM parameter store
- works for linux, windows, macos, raspberry Pi OS

### How does it work?
- install ssm agent on the systems we want to control
- installed by default on Amazon Linux AMI and some Ubuntu AMI
- if an instance can't be controlled by SSM, probably an issue with the agent

---

# 135: SSM Session Manager
- allows you to start a secure shell on your ec2 and on premise server
- no ssh access, bastion hosts or ssh keys needed
- no port 22 needed (secure)
- supports Linux, macOS, windows
- send session data to s3 or cloudwatch logs

- Hands on
  - create a new ec2 instance , disallow all traffic
  - in advanced settings, go to IAM instance profile > create a new profile
    - create a role
    - aws service
    - ec2
    - choose AmazonSSMManagedInstanceCore
    - create
  - select the newly created role
  - launch the instance
  - go to SSM
  - go to fleet manager > all instances registered with ssm are listed
  - go to session manager > start a session on the ec2 instance
  - 3 ways to access ec2 instance
    - ssh keys + ssh from terminal
    - ec2 instance connect (still need open port 22)
    - ssm (need an iam role)
   
--- 

# 136: SSM Parameter Store

- secure storage for config and secrets (api keys, passwords)
- serverless, scalable, durable, easy SDK
- control access permissions via IAM
- version tracking and encryption
- integrated with KMS

- Hands On
  - go to parameter store
  - create a parameter
  - give name and choose standard
  - choose string
  - enter the value
 
---



