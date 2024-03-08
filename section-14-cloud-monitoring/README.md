# Section 14: Cloud Monitoring

# 157: CloudWatch Metrics & CloudWatch Alarms Overview
- cloudwatch provides metrics for every services in AWS
- metrics have timestamps
- can create a cloudwatch dashboard of metrics,
- only available in us-east-1

### Important Metrics
- Ec2: cpu utilization, status checks, network
  - default: every 5 mins
  - detailed: 1 min but costs more
- ebs: disk r/w
- s3: bucketsizebytes, number of objects, all requests
- billing: total estimated charge only in us-east-1 but for entire account
- service limits: how much u have been using
- custom

### Alarms
- trigger notifications for any metric
- actions:
  - auto scaling: increase or decrese ec2 instance
  - ec2 actions: stop, terminate, reboot, recover an ec2 instance
  - sns notifications
 
- various options are there like sampling, %, max, min etc
- can choose a period on which to evaluate a alarm
- Alarm status: OK, insufficient_data, alarm

---

# 158: CW Hands On
- Go to CW metrics
- go to all metrics
- go to all alarms > create a alarm > cpu utilization
  - statistic > average
  - set greater than 80%
  - create a new topci
  - send a new notification
  - add the temp email
  - click next
  - create alarm
- go to ec2 instance > monitoring
- click on plus on alarm status
  - create an alarm
  - action : recover
  - status check failed: system
  - create alarm
- for billing alarm, go to us-east-1

---

# 159: CloudWatch logs:
- log files
- can collect from :
  - ecs
  - beanstalk
  - cloudtrail
  - aws lambda
  - agents on ec2 machines and on premise servers
  - route53
- enable real time monitoring of logs
- retention from 30 days to infite duration

### For EC2
- no default
- run a cloudwatch agent who push the log files to CW logs

---

# 160: CloudWatch Logs Hands On
- go to CW logs

---

# 161: Eventbridge (Formarly CW Events)
- react to events between aws events
- schedule: cronjobs (scheduled scripts)
- event pattern: event rules to react to a service doing something. ex: IAM root user sign -> sns topic with notification
- default eventbus: from aws services
- but can also get events from partners from AWS using partner event bus.
- Plug in custom event bus and use custom event bus
- schema registry: model event schema
- you can archive events sent to the bus and replay them

---

# 162: Eventbridge Hands On
- Go to the console, create a rule
- create in aws eventbridge scheduler
- choose repeat, frequency of 1 hour
- choose target as lambda
- select a lambda function
- choose defaults
- create schedule
- can create a loginevent rules, ec2 termination event

--- 

# 163: CloudTrail
- provides governance, compliance, and audit for your aws account
- enabled by default
- get a history of events/api calls made within your aws account by
  - console
  - sdk
  - cli
  - aws services
- can put logs from cloudtrail into cloudwatch logs or s3
- a trail can be applied to all regions or a single region
- investigate cloudtrail

--- 

# 164: Cloudtrail hands on
- go to cloutrail on the console

--- 

# 165: X-Ray
- debugging in production, the good way
  - test locally
  - add log statements
  - re deploy
- log format differ and analysis is hard
- monolith is easy but distributed is hard

### Benefits
- visual analysis of apps
- understand dependencies in a microservices architecture
- pinpoint service issues
- review request behavior
- find error and exceptions
- are we meeting time SLA?
- throttling
- identify users that are impacted

---

# 166: Amazon CodeGuru
- ML powered service
- auto code reviews
- app performance recommendation
- codeguru reviewer:
  - automated code reviews for static code analysis (dev)
- codeguru profiler: visibility/recommendations about application performance during runtime (prod)
  - understand run time behavior
  - id if app is consuming extensive cpu for long time
  - id and remove inefficiencies
  - reduce cpu utilization
  - decrease compute cost
  - provide heap summary
  - anomaly detection
 
---

# 167: AWS Health Dash: Service History

- alerts and remediation guidance when aws is experiencing events that might impact you
- general status of aws services, personalized view of performance and availability of the aws services underlying your aws resources
- displays relevant and timely info to help you manage events in progress and proactive notification to plan

---

# 168: AWS Health Dash Hands On

- Click on Bell and click on the Event log
- Service history for all aws services for all region for all the time
- Your account health is for your resources
- 
