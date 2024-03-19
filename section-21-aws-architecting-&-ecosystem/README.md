# Section 21: AWS Architecting & Ecosystem

# 257: AWS Whitepapers Well-Architected Frameworks
- AWS Cloud Best Practices:
  - Scalable
  - Disposable Resourses
  - automation
  - loose coupling:
    - monolith
    - break it down into smaller loose components
    - a change should not cascade to others
  - services, not servers
    - dont just use ec2
- 6 Pillars
  - they are synergy
 
---

# 258: Pillar 1: Operational Excellence
- includes the ability to run and monitor systems to deliver business value and to continually improve process and procedures
- design principles:
  - perform ops as a code
  - annotate documentations
  - make frequent, small, reversible changes
  - refine operations procedures freq
  - anticipate failure
  - learn from all operational failures
 
- Prepare
  - use config and CF
- operate
  - use automate,
  - track and trace
  - use CF, config and cloudtrail
  - use cloudwatch
  - use xray
- evolve
  - CF
  - use cicd tools like codebuild, code commit, codedeploy, codepipeline
  -

---

# 259: Pillar 2: Security
- implement a strong identity foundation
- enable tracebility
- apply security at all layers
- automate security best practices
- keep people away from data
- prepare for security events
- IAM: IAM, STS, MFA, AWS organization
- Detective : AWS Config, CLoudtrail, Cloudwatch
- infra protection: CF, VPC, Sheild, WAF, Inspector
- data protection: kms, s3, elb, ebs, rds
- incident response: Iam, cf, cloudwatch events,


---

# 260: Pillar 3: Reliability
- recover from infra or service disruptions
- design principles:
  - test recovery procedures
  - automatically recover from failures
  - scale horizontally to increase system, availability
  - stop guessing capacity
  - manage change in automation
- services:
  - foundations: IAM, VPC, Service Limits/Quotas, Trusted Advisor
  - Change Management: Autoscaling, Cloudwatch, Cloudtrail, config
  - Failure management: backups, CF, s3, glacier, route 53

---

# 261: Pillar 4: Performance Efficiency
- able to use the resources efficiently
- design principles:
  - democratize advanced technologies
  - go global in minutes
  - use serverless arch
  - experiment more often
  - mechanical sympathy (be aware of all the aws services) v v hard
- Service:
  - selection: autoscaling, lambda, ebs, s3, rds
  - review: CF
  - monitoring: cloudwatch, lambda
  - tradeoffs: rds, elasticache, snowball
 
---

# 262: Pillar 5: Cost Optimization
- run systems to deliver business value at lowest price point
- design principles:
  - adopt a consumption mode
  - measure overall efficiency -  use cloudwatch
  - stop money on data center operations, use cloud
  - analyze and attribute expenditure
  - use managed and application level services
- services:
  - Expenditure awareness: budget, cost and usage report, cost explorer, reserved instance reportng
  - cost effective resources: spot instance, reserved instance, s3 glacier
  - match supply and demand: autoscale and lambda
  - optimizing over time: trusted advisor, cost and usage report, aws news blog
 
---

# 263: Pillar 6: Sustainability
- minimize env impacts
- design principles:
  - understand your project
  - estabilish sustainability goals
  - maximize utilization
  - anticipate and adopt new features
  - use managed services
  - reduce the downsteam impact of your cloud workloads
 
- services:
  - autoscaling, serverless offering
  - cost explorer, graviton 2, ec2 T instances, spot instances
  - efs ia, s3 glacier, ebs, cold hdd
  - s3 lifecycle configurations
  - data lifecyle manager
  - read local, write global
 
---

# 264: AWS well architected tool
- free tool to review your architectures against the 6 pillars
- go to the tool
  - Give name, description, regions, ...
  - apply lenses
  - answer the questions
  - evaluate
 
----

# 265: 

