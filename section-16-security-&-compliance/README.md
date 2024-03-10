# Section 16: Security and Compliance

# 181: Shared Responsiblity Model: Reminders and Examples
- Shared Responsibility Model
  - AWS
    - security of the cloud
    - protect infra
    - managed services like s3, dynamodb, rds etc
  - Customer:
   - security in the cloud
   - for ex ec2, for guest OS security, patch, update, firewall, n/w config, iam
   - encryption of app data
  - shared controls
    - patch management, config management, awareness and training


### RDS
- AWS
  - manage the underlying ec2, disable ssh instance
  - auto db patching, os patching
  - audit underlying ec2 instance
- Your
  - check ports /IP/ SG inbound rules in DB's SG
  - in db user creattion and permissions
  - creating a db with/without public access
 
### S3
- AWS
  - guarantee you get unlimited storage
  - you get encryption
  - separation of data between different customers
  - aws employees cant access data
 
- yours:
  - bucket config
  - bucket policy/ public access
  - iam users/roles
  - enable encryption
 
---

# 182: DDos: WAF & Sheild
- multiple servers lauch bots which request our app and then our app will not be able to cater to them leading it to be unavailable to actual users
- Sheild Standard: for all website at no cost
- Sheild Advanced: 24/7 premium
- WAF: filter specific requests based on rules
- Cloudfront and ROute53
  - availabilty protection usign global edge network
  - combined with aws sheild, provides attack mitigation at the edge
 
- be ready to scale: auto scale

### Sample ref arch for ddos
```
                                                            |-----------VPC-------- |
[clients] ==== > [Sheild Route53]=====> [Sheild CF] ===== > | Sheild LB ====> ASG   |
                                            ||              |_______________________|
                                           [WAF]
```

### AWS sheild
- sheild standard :
  -free
  - comman attacks such as syn/udp floods, reflection attacks,and other layer 3/4 attacks
- sheild advanced:
  - optional
  - 3000$ per month per organization
  - sophisticated attack on EC2, ELB, CF, Global Accelerator, Route 53
  - access to response team
  - protect against higher fees during ddos attacks
 

### WAF - web application firewall
- protects your web at layer 7
- http
- deploy on ALB, API gateway, CF
- define webacl
  - rules can include IP, http headers, http body, URI strings
  - attacks such as sql injection and xss
  - size constraint, geo match
  - rate limit
  - 

---

# 183: AWS N/W Firewall
- protect your vpc overall from layer 3 to layer 7
- any direction, you can inspect
   - vpc to vpc traffic
   - outbount to internet
   - inbound
   - from DX and Site to Site
 
---

# 184: AWS Firewall Manager
- manage all security rules of all accounts of an aws organization
- security policy
  - vpc SG
  - WAF
  - Sheild advanced
  - n/w firewall
 
- rules are applied to new resources that are created

---

# 185: Penetration Testing
- aws customers are welcome to test your own infra for security assessments without prior approval for 8 services
  - ec2, nat gateways, elb
  - rds
  - cf
  - aurora
  - api gateways
  - lambda and lambda edge functions
  - lightsail resoures
  - beanstalk environments
- prohibited:
  - dns zone walking
  - DOS, DDoS, Simulated DoS, Simulated DDos,
  - port flooding
  - protocol flooding
  - request flooding
 
---

# 186: Encryption with KMS and CloudHSM
- KMS
  - we dont have access to the keys
  - aws manages the keys and we define who can access the keys
  - opt in
    - ebs
    - s3
    - redshift
    - rds
    - efs
  - auto
    - cloud trail logs
    - s3 glacier
    - storage gateway
- Cloud HSM
  - AWS provisions HSM
  - we manage the keys
  - device is tamper resistant

- Cloud HSM Client to manage the keys via ssl connection

- types of KMS keys
  - customer managed keys:
     - create, managed, used
     - rotation policy (one year, keeps old key)
     - possiblity to bring your own key
  - aws managed key
     - created maneged and used on the customers behalf by aws
     - used by aws services (AWS/s3, aws/ebs/,
  - aws owned key
     - collectin of CMK, that an aws service owns and manages to use in multiple accounts
     - aws can use those to protect resources in your account but we cant see the keys
   
  - CloudHSM keys
    - key generated from our own device
    - ops performed by our own HSM cluster

---

# 187: KMS & CloudHSM Hands On

- go to KMS
- go to ec2 console > create a volume > encrypt the volume
- use default aws master key
- create volume
- go to cloud trail
  - go to the s3 bucket
  - check out the file properties, it will be encrypted
 
- go to customer managed key >
- symmetric
- Choose KMS
- give alias
- click next
- click next until finish and click finish
- go to key rotation, changes every year, keeps old key
- now when you create a new volume with encryption, you can choose the key we just created

  ---

# 188: ACM Overview
- easily provision, SSL, TLS certificate
- provide in flight encryption https
- our ALB will use http to connect to ASG, but we can use ACM to provision and maintain TLS certificate and allow HTTPS connection from client to ALB
- supports both public and private TLS Certificates
- free of charge for public tls certs
- auto TLS certs renewal
- integration with load TLS on ELB, CF, Api Gateway

---

# 189: Secrets manager overview
- never service, meant for storing secrets
- capable to force secrets rotation every x days
- auto generate secrets on rotation (lambda)
- integration with aws rds (MySQL, postgres, aurora)
- secrets are encrypted using KMS
- mostly meant for RDS integration
- paid service
- go the console >
  - click store a new secret
  - select RDS
  - choose database, rotation policy and create
 
---

# 190: Artifact Overview
- not really a service 
- on demand access to aws compliance documentation and aws agreement
- artifact reports: allows you to download aws security and compliance documents from 3rd party auditors like aws iso certifications, payment card industry, system and organization control
- artifact agreements: review, accept, track status of aws agreements  for an individual account or in your organization
- can be used to support internal audit or compliance needs
- GLOBAL service

---

# 191: GuardDuty Overview
- intelligent threat discovery to protect your aws account
- uses ML
- one click enable
- 30 days trial
- input data includes:
  - cloudtrail event logs: unusual api calls, unauth deployments
  - vpc flow logs: unusual internal traffic, unusual IP address
  - dns logs: compromised ec2 instances
  - optional features: EKS audit logs, rds & aurora, ebs, lambda
- can setup eventbridge rules to be notified in case of finding
- eventbridge rules can target aws lambda or SNS
- can protect against cryptocurrency attacks (has a dedicated "finding" for it)

---

# 192: Inspector Overview:
- auto security assessments
- for ec2 instances:
  - leverage aws system manager agent
  - analyse against unintended n/w accessibility
  - analyze the running OS against known vulnerability
- for container images push to amazon ecr
  - assessment of container images as they are pushed
- for lambda functions
   - identifies software vulnerabilites in fxn code and package dependencies
   - assessment of fxns as they are deployed
 
- report and integration with AWS security hub
- send findings to amazon event bridge

### what does it evaluate?
- only for running ec2 instances, container images and lambda fxns
- continous scanning of the infra, only when needed
- package vulnerabilities (ec2, ecr, lambda & database of CVE)
- n/w reachability
- risk score is associated with all the vulnerabilites for prioritization

---

# 193: Config Overview
- helps with audit and recording compliance of ur aws resources
- helps record config changes over time
- possible to store in s3 and get it analyzed with athena
- ex:
  - is there unrestricted ssh access to my security group
  - do my buckets have public access?
  - ALB config changed over time
 
- You can receive alerts (SNS) for any changes
- per region service
- can be aggregated for all regions and all accounts
- can see the changes made for making compliant or non compliant
  
---

# 194: Macie Overview
- fully managed data security and data privacy service using ML and pattern matching to discover and protect PII
- helps ID and alerting you for PII using eventbridge notifications

---

# Security hub Overview
- central security tool to manage security across several aws accounts and automate security checks
- integrated dashboards showing current security and compliance status to quickly take actions
- automatically aggregates alerts in predefined or personal findings formats from various aws services & aws partner tools
- 30 days trial

---

# 196: Amazon Detective Overview
- guard duty, macie, security hub are used to id potential issue
- sometimes u need deeper analysis
- amazon detective analyzes, investigates, quickly identifies the root cause of security issues or suspicious activities using ML and graphs
- automatically collects and processes events from VPC flow logs, cloud trail, guardduty and create a unified view

---

# AWS abuse
- report suspected aws resources used for abusive or illegal purposes
- like:
  - spam emails
  - port scanning
  - dos ddos
  - intrusion
  - hosting objectionable or copyrighted content
  - distributing malware
 
---

# Root User Privileges
- root user has complete access to all aws services and resources
- actions can be performed by root:
  - change account settings
  - view tax invoicees
  - restore Iam permissions
  - change or cancel aws support plan
  - register as a seller in the reserved instance marketplace
  - configure s3 bucket to enable mfa
  - sign up for gov cloud
 
---

# 199: IAM Access Ananlyze
- find out resources are shared externally
- define zone of trust = aws account or organization
- access outside of zone of trusts => findings
- go to access analyzer -
  - give name, zone of trust, create
- go to findings and act accordingly
- can create an archive rules for intended access

----

