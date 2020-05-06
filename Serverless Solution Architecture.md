## Mobile application: MyToDoList

![image-20200413230045163](.\screenshot\image-20200413230045163.png)

![image-20200413230156686](.\screenshot\image-20200413230156686.png)

### Giving users access to S3

![image-20200413230352729](.\screenshot\image-20200413230352729.png)

### High read throughput,static data

![image-20200413230526461](.\screenshot\image-20200413230526461.png)

**Caching in API Gateway**

![image-20200413230556742](.\screenshot\image-20200413230556742.png)

## Serverless hosted website:MyBlog.com

![image-20200413230835947](.\screenshot\image-20200413230835947.png)

### Serving static content,globally

![image-20200413230933789](.\screenshot\image-20200413230933789.png)

### Serving static content,globally,securely

![image-20200413231016999](.\screenshot\image-20200413231016999.png)

### Adding a public serverless REST API

![image-20200413231105857](.\screenshot\image-20200413231105857.png)

### Leveraging DynamoDB Global Tables

![image-20200413231135273](.\screenshot\image-20200413231135273.png)

### User Welcome email flow

![image-20200413231248885](.\screenshot\image-20200413231248885.png)

### Thumbnail Generation flow

![image-20200413231357688](.\screenshot\image-20200413231357688.png)

## MicroServices

![image-20200413231602428](.\screenshot\image-20200413231602428.png)

### MicroServices Environment

![image-20200413231735713](.\screenshot\image-20200413231735713.png)

- you are free to design each micro-service the way you want
- Synchronous patterns: API Gateway,Load Balancers
- Asynchronous patterns: SQS,Kinesis,SNS, Lambda triggers (S3)
- Challenges with micro-services:
  - repeated overhead for creating each new microservices
  - issues with optimizing server density/utilization
  - complexity of running multiple versions of multiple microservices simultaneously
  - proliferation of client-side code requirements to integrate with many separate services
- Some of the challenges are solved by Serverless patterns:
  - API Gateway,Lambda scale automatically and you pay per usage
  - You can easily clone API,reproduce environments
  - Generated client SDK through Swagger integration for the API Gateway

## Distributing paid content

![image-20200414201444648](.\screenshot\image-20200414201444648.png)

### Start simple,premium user service

![image-20200414201530297](.\screenshot\image-20200414201530297.png)

### Add authentication

![image-20200414201613515](.\screenshot\image-20200414201613515.png)

### Add videos storage services

![image-20200414201638365](.\screenshot\image-20200414201638365.png)

### Distribute globally and secure

![image-20200414201702481](.\screenshot\image-20200414201702481.png)

### Distribute content only to premium users

![image-20200414201924013](.\screenshot\image-20200414201924013.png)

![image-20200414202028382](.\screenshot\image-20200414202028382.png)

## Software updates offloading

![image-20200414202123036](.\screenshot\image-20200414202123036.png)

### Our application current state

![image-20200414202232839](.\screenshot\image-20200414202232839.png)

### Easy way to fix things

![image-20200414202330763](.\screenshot\image-20200414202330763.png)

![image-20200414202413537](.\screenshot\image-20200414202413537.png)

## Big data ingestion pipeline

![image-20200414202453818](.\screenshot\image-20200414202453818.png)

### Big data ingestion pipeline

![image-20200414202737651](.\screenshot\image-20200414202737651.png)

![image-20200414202830717](.\screenshot\image-20200414202830717.png)

