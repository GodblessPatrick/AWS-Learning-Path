# More Solution Architectures

## Event Processing 

### Lambda, SNS and SQS

![image-20200420222858765](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420222858765.png)

DLQ in SQS side																				DLQ in Lambda side

### Fan out pattern: deliver to multiple SQS

![image-20200420223150762](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420223150762.png)

### S3 Event

![image-20200420223650901](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420223650901.png)

## Caching Strategies in AWS

![image-20200420223748480](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420223748480.png)

CloudFront: TTL to balance cache

API Gateway: regional service => cache will be regional

No caching in S3

## Blocking an IP Address in AWS

### Blocking an IP address

![image-20200420224101739](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420224101739.png)

NACL: VPC level

### Blocking an IP address - with an ALB

![image-20200420224159093](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420224159093.png)

Connection from Client will be terminated and ALB creates a new connection to EC2 instance

EC2 SG must be configured to connect to ALB SG 

### Blocking an IP address - with a NLB

![image-20200420224446064](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420224446064.png)

NACL will work for particular clients' IPs

### Blocking an IP address - ALB + WAF

![image-20200420224717604](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420224717604.png)

WAF: install to ALB

### Blocking an IP address - ALB,CloudFront WAF

![image-20200420224808559](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420224808559.png)

CloudFront: geo-restriction feature to restrict all the country from out clients to be denied on CloudFront

ALB will need to receive public IP of CloudFront so NACL is not helpful at all (clients' IPs will go to CloudFront first)

## High Performance Computing (HPC)

![image-20200420225052177](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420225052177.png)

### Data Management & Transfer

![image-20200420225131323](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420225131323.png)

### Compute and Networking

![image-20200420225216680](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420225216680.png)

![image-20200420225847582](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420225847582.png)

### Storage

![image-20200420230014420](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420230014420.png)

### Automation and Orchestration

![image-20200420230101091](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420230101091.png)

## EC2 Instance High Availability

![image-20200420230406455](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420230406455.png)

Lambda: detach Elastic IP from failed EC2 instance and attach to standby EC2 instance

### ASG Approach

![image-20200420230608582](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420230608582.png)

![image-20200420230629800](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200420230629800.png)

### ASG + EBS

![image-20200420230818841](screenshot/image-20200420230818841.png)

![image-20200420230922958](screenshot/image-20200420230922958.png)

![image-20200420231002003](screenshot/image-20200420231002003.png)

## Bastion Host High Availability

![image-20200420231155994](screenshot/image-20200420231155994.png)

![image-20200420231239510](screenshot/image-20200420231239510.png)

**We use NLB for TCP traffic**

**No ALB since it is for HTTP**

![image-20200420231425732](screenshot/image-20200420231425732.png)

