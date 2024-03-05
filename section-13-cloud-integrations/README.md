# Section 13: Cloud Integrations

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# 150: Cloud Integrations Overview
- multiple apps need to communicate with each other
- sync comm: one service talk to one another
- async comm: one service enqueues the message for the other service to read, decoupled

### Sync comm
- can be problematic due to spikes of traffic
- its better to use decoupled model
- using SQS: queue model
- using SNS: pub/sub
- using Kinesis: Real time streaming model

- these apps scale independently from our app

---

# 151: SQS: Simple Queue Service
- producers send messages into the queue 
- consumers pull messages from the queue (polling)
- oldest aws offering: over 10 years
- fully managed services, use to **to decouple apps**
- scales from 1 msg to 10000s per second
- default retention of 4 days to max 14 days
- no limit on the queue size
- msg deleted after being read
- low latency (<10 ms)
- decouple between apps tiers
- supports FIFO queues

---

# 152: SQS Hands-on
- go to sqs
- create a queue
- choose standard queue
- choose default for others
- click "send and receive messages"
- send a message
- check the receive message section
- click pull from messages > they will be pulled from the queue.

---

# 153: Kinesis Overview
- real-time big data streaming
- managed service to collect, process and analyze real time streaming data at any scale
- kinesis data streams: low latency streaming to ingest data at scale from hundreds of thousands of sources
- kinesis data firehose: load streams into s3, redshift, elasticsearch etc
- kinesis data analytics: perform real-time analytics on streams using SQL
- kinesis video streams: monitor real time video streams for analytics for AI/ML

---

# 154: SNS: simple notification service
- send one message to many receivers
- event publishers: sends messages
- event subscribers: listen to messages
- up to 12.5 mil subs per topic, 100000 topics limit
- send messages to sqs, lambda, kinesis, emails, SMS, http endpoints

---

# 155: SNS Hands On
- go to sns
- create a topic > default options
- create a subscriptions > Email > get a temp email from mailinator.com > confirm subs
- click publish message > send message
- check inbox

---

# 156: Amazon MQ Overview
- SQS and SNS are cloud native
- traditional apps using open protocols like MQTT, AMQP, STOMP, Openwire, WSS.
- you can use MQ service when you migrate to cloud
- it is a managed message broker for RabbitMQ & ActiveMQ
- Amazon MQ doesnt scale as much as other two
- runs on a server with multi az feature with failover
- both queue and topic features

---
