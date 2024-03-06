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
