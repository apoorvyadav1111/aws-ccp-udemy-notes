# Section 20: Other Services

---

# 239: Workspaces Overview
- Desktop as a service, managed
- eliminate management of on premise VDI
- fast and scalable to 1000 of users
- pay as you go with monthly or hourly rates
- secured data
- multiregions:
  - to minimize latency deploy close to your office

---

# 240: AppStream 2.0 Overview
- Desktop App stream service
- stream an app without acquiring a computer
- app is accessible via the browser, eg. blender
- Workspace:
  - fully managed vdi
  - users connect to the vdi
- appstream:
  - no need to connect to vdi
  - work with any device
  - allow you to configure as per app

---

# 241: IoT Core Overview
- connect iot device to aws cloud
- secure, serverless and scalable to billions of devices
- apps can connect to the device when they are not connected
- integrate with diff services like lambda, s3, sagemaker
- build iot app that collect, gather and act on data


---

# 242: AppSync
- store data, build backend for mobile and web app in real time
- make use of graphql
- client code can be generated automatically
- integrations with lambda and dynamoDB
- real time subs
- offline data sync
- fine grained security
- aws amplify can leverage aws app sync in the background
  

---

# 243: Amplify
- set of tools and services to develop and deploy scalable full stack web and mobile apps
- auth, storage, api, ci/cd, pubsub, analytics ai/ml, etc

---

# 244: AWS application Composer
- visually design and build serverless apps on aws
- deploy aws infra code without being an expert
- config how your resources interact with each other
- generates IAC using CF
- able to import existing CF/SAM templates to visualize them

---

# 245: Device Farm Overview
- fully managed service that tests your web, mobile apps against desktop browsers, real mobile devices and tablets
- run tests concurrently on mobile devices
- ability to configure device settings

---

# 246: AWS backup Overview
- fully managed backup service to centrally manage for all services
- on demand and scheduled backups
- supports PITR
- retention periods, lifecyle management, backup policies
- cross region backups
- cross account backups (backed by aws organizations)
- aws backup > create backup plan (freq, retention, policy) -> assign services -> backup to s3

---

# 247: Disaster Recovery Strategies
- backup and restore:
  - cheapest
  - s3 and corporate data center
- pilot light
  - ec2 in cloud with main server on corporate
  - mid cost
- warm standby
  - ec2, full version of the app, but at minimum size
- multi-site/hot-site:
  - full version of the app at full size
  - costliest

### Typical DR Setup
- have failover in another region

---

# 248: AWS Elastic Disaster Recovery Service (DRS)
- previously, CloudEndure Disaster Recovery
- quick, easy to recover physical, virtual and cloud based servers into aws
- continous block level replication for your servers
- an aws replication agent does continous replication from corporate data center to aws cloud and then you can create a failover minimum app when in disaster
- do a failback post disaster

---

# 249: AWS Datasync
- move large data from onpremise to aws
- can sync to s3, efs and fsx for windows
- replication tasks can be scheduled for hourly, daily, weekly
- incremental load

---

# 250: Application Discovery Service and App migration Service
- plan migration projects by gathering information about on premise data center
- server utilization and dependency mapping are essential
- agentless discovery:
  - vm inventory, configuration and performance history such as CPU, memory and disk usage
- agent based discovery:
  - system configuration, system perf, running processes, details of the network
- resulting data can be viewed in the migration hub

- MGN
  - rehost solution which simplify migrating applications to AWS
  - converts the physical, virtual or cloud baser servers to run natively on AWS

---

# 251: AWS migration evaluator
- helps building a data driven case for migration to aws
- install agentless collector to conduct a broad based discovery
- takes a snapshot of on premise footprint, server dependencies..
- analyze current state, define target state and then develop migration plan

---

# 252: AWS Migration Hub
- Central location to collect servers and applications inventory data for the assessement planning and tracking of migrations to AWS
- helps accelerate the migration, automate lift-and-shift
- aws migration hub orchestrator- provides pre built templates to save time and effort migrating enterprise apps
- supports migrations status updates from application mgration service

---

# 253: AWS Fault injection simulator (FIS)
- fully managed service for running fault injection experiments on aws workloads
- based on chaos engineering- stressing an application by creating disruptive events
- uncover hidden bugs and perf bottlenecks
- supports the following aws services: EC2, ecs, eks, rds
- prebuilt templates that generate the desired disruptions

---

# 254: Step Fxn
- build serverless visual workflow to orchestrate your lambda fxn
- features: sequence, parallel, conditions, timeouts, error handling
- can integrate with ec2,ecs, on premise servers, etc
- use cases: order fullfillment, data processing, web apps, any workflow

---

# 255: Ground Station
- fully managed
- control satellite comm, process data, and scale
- global network of satellite ground stattions
- allows you to download the satellite data to the ground stations within seconds

---

# 256: AWS Pinpoint
- scalable 2 way marketing comm service
- email, push notifications, push, voice, sms, and inapp msg
- ability to segment and personalize msg
- possible to get replies
- scales to billions of msg per day
- ex: run campaigns, bulk
- you can create msg templates, schedules, target segments and campaigns

---
