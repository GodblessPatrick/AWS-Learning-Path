# Decoupling applications: SQS,SNS,Kinesis,Active MQ

## Introduction

When we start deploying multiple applications,they will inevitably need to communicate with one other

There are two patterns of application communication:

- Synchronous communications

  (application to application)

  ![image-20200408205433497](.\screenshot\image-20200408205433497.png)

- Asynchronous / Event based

  (application to queue to application)

  ![image-20200408205504217](.\screenshot\image-20200408205504217.png)

## SQS

### What's a queue?

![image-20200408205745444](.\screenshot\image-20200408205745444.png)

### Standard Queue

- Oldest offering 
- Fully managed
- Scales from 1 message per second to 10000s per second
- Default retention of messages:4 days,maximum of 14 days
- No limit to how many messages can be in the queue
- Low latency (< 10 ms on publish and receive)
- scaling in terms of number of consumers
- Horizontal scaling in terms of number of consumers
- Can have duplicate messages (at least once delivery,occasionally)
- Can have out of order messages (best effort ordering)
- Limitation of 256 KB per message sent (not good for video,best for JSON)

### Delay Queue

- Delay a message (consumers don't see it immediately) up to 15 minutes
- Default is 0 seconds (message is available right away)
- Can set a default at queue level
- Can override the default using the **DelaySeconds** parameter
- ![image-20200408210706680](.\screenshot\image-20200408210706680.png)

### Producing Messages

- Define Body
- Add message attributes (metadata - optional)
- Provide Delay Delivery (optional)
- Get back
  - Message identifier
  - MD5 hash of the body
- ![image-20200408210853799](.\screenshot\image-20200408210853799.png)

### Consuming Messages

- Poll SQS for messages (receive up to 10 messages at a time)
- Process the message within the **visibility timeout**
- Delete the message using the message ID & receipt handle
- ![image-20200408211134931](.\screenshot\image-20200408211134931.png)

### Visibility Timeout 

When a consumer polls a message from a queue,the message is "invisible" to other consumers for a defined period => **visibility timeout**

- Set between 0 second to 12 hours (default 30 seconds)
- If too high (15 minutes) and consumer fails to process the message,you must wait a long time before processing the message again
- If too low (30 seconds) and consumer needs time to process the message (2 minutes),another consumer will receive the message and the message will be processed more than once
- **ChangeMessageVisibility** API to change the visibility while processing a message
- **DeleteMessage** API to tell SQS the message was successfully processed

### Dead Letter Queue

If a consumer  fails to process a message within the Visibility Timeout,the message goes back to the queue

We can set a threshold of how manty times a message can go back to the queue => **redrive policy**

After the threshold is exceeded,the message goes into a **dead letter queue** (DLQ)

We have to create a DLQ first and then designate it DLQ

Make sure to process the message in the DLQ before they expire 

![image-20200408212216292](.\screenshot\image-20200408212216292.png)

### Long Polling 

When a consumer requests message from the queue,it can optionally "wait" for messages to arrive if there are none in the queue => **long polling**

**Long polling decreases the number of API calls made to SQS while increasing the efficiency and latency of your application**

The wait time can be between 1 sec to 20 sec (20 sec is preferable)

Long polling is preferable to short polling

Long polling can be enabled at the queue level or at the API level using **WaitTimeSeconds**

![image-20200408212645562](.\screenshot\image-20200408212645562.png)

![image-20200408212814805](.\screenshot\image-20200408212814805.png)

### FIFO Queue

![image-20200408213907582](.\screenshot\image-20200408213907582.png)

## SQS with ASG

![image-20200408214703234](.\screenshot\image-20200408214703234.png)

![image-20200408214747920](.\screenshot\image-20200408214747920.png)

## SNS

What if you want to send one message to many receivers?

![image-20200408214917205](.\screenshot\image-20200408214917205.png)

- The "event producer" only sends message to one SNS topic
- As many "event receivers" (subscriptions) as we want to listen to the SNS topic notifications
- Each subscriber to the topic will get all the messages (note: new feature to filter messages)
- Up to 10,000,000 subscriptions per topic
- 100,000 topic limit
- Subscribers can be:
  - SQS
  - HTTP/HTTPS (with delivery retries - how many times)
  - Lambda
  - Emails
  - SMS messages
  - Mobile Notifications

### SNS integrates with a lot of Amazon Products

- Some service can send data directly to SNS for notifications
- CloudWatch (for alarms)
- Auto Scaling Group notifications
- Amazon S3 (on bucket events)
- CloudFormation (upon state changes => failed to build,etc)

### How to publish

- Topic Publish (within your AWS Server - using SDK)
  - Create a topic
  - Create a subscription (or many)
  - Publish to the topic
- Direct Publish (for mobile apps SDK)
  - Create a platform application
  - Create a platform endpoint
  - Publish to the platform endpoint
  - Works with Google GCM,Apple APNS,Amazon ADM

### SNS + SQS

**Fan out**

Push once in SNS,receive in many SQS

Fully decoupled

No data loss

Ability to add receiver of data later

SQS allows for delayed processing

SQS allows for retries of work

May have many workers on one queue and one worker on the other queue

![image-20200408220005591](.\screenshot\image-20200408220005591.png)

## Kinesis

 ### Overview

Kinesis is managed alternative to Apache Kafka

Great for application logs,metrics,IoT,clickstreams

Great for "real-time" big data

Great for streaming processing frameworks

Data is automatically replicated to 3 AZ

***Kinesis Streams**: low latency streaming ingest at scale

**Kinesis Analytics**: perform real-time analytics on streams using SQL

**Kinesis Firehose**: load streams into S3,Redshift,ElasticSearch

![image-20200408221108505](.\screenshot\image-20200408221108505.png)

### Kinesis Streams

- Streams are divided in ordered Shards / Partitions

  ![image-20200408221505511](.\screenshot\image-20200408221505511.png)

- Data retention is 1 day by default,can go up to 7 days

- Ability to reprocess / replay data

- Multiple applications can consume the same stream

- Real-time processing with scale of throughput

- Once data is inserted in Kinesis,it can't be deleted (immutability)

### Kinesis Streams Shards

- One stream is made of many different shards
- 1 MB/s or 1000 messages/s at write per shard
- 2 MB/s at read per shard
- Billing is per shard provisioned,can have as many shards as you want
- Batching available or per message calls
- The number of shards can evolve over time (reshard / merge)
- **Records are ordered per shard**
- ![image-20200408222020688](.\screenshot\image-20200408222020688.png)

### Put records

- PutRecord API + Partition key that gets hashed
- The same key goes to the same partition (helps with ordering for a specific key)
- Messages sent get a "sequence number"
- Choose a partition key that is highly distributed (helps prevent "hot partition")
  - user_id if many users
  - **NOT** country_id if 90% of the users are in one country
- Use Batching with PutRecords to reduce costs and increase throughput
- **ProvisionedThroughputExceeded** if we go over the limits
- Can use CLI,AWS SDK, or producer libraries from various frameworks
- ![image-20200408222803390](.\screenshot\image-20200408222803390.png)

### Exceptions

- ProvisionedThroughputExceeded Exceptions
  - Happens when sending more data (exceeding MB/s or TPS for any shard)
  - Make sure you don't have a hot shard (such as your partition key is bad and too much data goes to that partition)
- Solution
  - Retries with backoff
  - Increase shards(scaling)
  - Ensure your partition key is a good one

### Consumers

![image-20200408223129069](.\screenshot\image-20200408223129069.png)

### Security

- Control access / authorization using IAM policies
- Encryption in flight using HTTPS endpoints
- Encryption at rest using KMS
- Possibility to encrypt / decrypt data client side (harder)
- VPC Endpoints available for Kinesis to access within VPC

## Kinesis Firehose & Kinesis Data Analytics  

### Kinesis Firehose

- Fully managed service,no administration,automatic scaling,serverless
- Load data into **RedShift / Amazon S3 / ElasticSearch / Splunk**
- **Near Real Time**
  - 60 seconds latency minimum for non full batches
  - or minimum 32 MB of data at a time
- Supports many data formats,conversions,transformations,compression
- Pay for the amount of data going through Firehose

![image-20200408224855510](.\screenshot\image-20200408224855510.png)

### Kinesis Data Stream Vs Firehose

- Streams
  - Going to write custom code (producer/ consumer)
  - Real time (~200 ms)
  - Must manage scaling (shard splitting / merging)
  - Data storage for 1 to 7 days,replay capability,multi consumers
- Firehose
  - Fully managed,send to S3,Splunk,RedShift,ElasticSearch
  - Serverless data transformations with Lambda
  - **Near** real time (lowest buffer time is 1 minute)
  - Automated Scaling
  - No data storage

### Kinesis Analytics

![image-20200408225313497](.\screenshot\image-20200408225313497.png)

![image-20200408225343647](.\screenshot\image-20200408225343647.png)

## Data Ordering for Kinesis Vs SQS FIFO

### Ordering data into Kinesis

![image-20200408225800160](.\screenshot\image-20200408225800160.png)

**Data will be ordered in Shard level**

### Ordering data into SQS

![image-20200408225947117](.\screenshot\image-20200408225947117.png)

### Kinesis Vs SQS ordering

![image-20200408230104080](.\screenshot\image-20200408230104080.png)

## SQS Vs SNS Vs Kinesis

![image-20200408230357730](.\screenshot\image-20200408230357730.png)

## Amazon MQ

When migrating to the cloud,using Amazon MQ

Amazon MQ does not scale as much as SQS/SNS

Amazon MQ runs on a dedicated machine,can run in HA with failover

Amazon MQ has both queue feature (~SQS) and topic feature(~SNS)

**if you see we are migrating an app from on-premise with cloud, and the app is using the MQTT or the AMQP protocol or whatever,what should we use? Well, the answer is Amazon MQ.**



