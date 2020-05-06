# Classic Solutions Architecture Discussions

## WhatsTheTime

![image-20200429204601698](screenshot/image-20200429204601698.png)

### Starting simple

![image-20200429204700829](screenshot/image-20200429204700829.png)

### Scaling vertically

![image-20200429204853127](screenshot/image-20200429204853127.png)

### Scaling horizontally

![image-20200429204944607](screenshot/image-20200429204944607.png)



![image-20200429205125484](screenshot/image-20200429205125484.png)

![image-20200429205232808](screenshot/image-20200429205232808.png)

### Scaling horizontally,with a load balancer

![image-20200429205409001](screenshot/image-20200429205409001.png)

### Scaling horizontally,with an auto-scaling group

![image-20200429205525811](screenshot/image-20200429205525811.png)

### Making our app multi-AZ

![image-20200429205559625](screenshot/image-20200429205559625.png)

### Minimum 2 AZ => Let's reserve capacity

![image-20200429205704597](screenshot/image-20200429205704597.png)

### Summary

![image-20200429205850172](screenshot/image-20200429205850172.png)

## MyClothes

![image-20200429205935852](screenshot/image-20200429205935852.png)

### Stateful Web App

![image-20200429210047683](screenshot/image-20200429210047683.png)

### Introduce Stickiness(Session Affinity) 

![image-20200429210152739](screenshot/image-20200429210152739.png)

###  Introduce User Cookies

![image-20200429210332791](screenshot/image-20200429210332791.png)

### Introduce Server Session

![image-20200429210446261](screenshot/image-20200429210446261.png)

### Storing User Data in a database

![image-20200429210535211](screenshot/image-20200429210535211.png)

### Scaling Reads

![image-20200429210609193](screenshot/image-20200429210609193.png)

### Scaling Reads(Alternative) - Write Through

**need some changes in application code**

![image-20200429210645116](screenshot/image-20200429210645116.png)

## Multi AZ - Survive disasters

![image-20200429210740268](screenshot/image-20200429210740268.png)

### SG

![image-20200429210815130](screenshot/image-20200429210815130.png)

### Summary

![image-20200429210914992](screenshot/image-20200429210914992.png)

## MyWordPress

![image-20200429210942605](screenshot/image-20200429210942605.png)

### RDS layer

![image-20200429211001376](screenshot/image-20200429211001376.png)

### Scaling with Aurora: Multi-AZ & Read Replicas

![image-20200429211039529](screenshot/image-20200429211039529.png)

### Storing Images with EBS

![image-20200429211135087](screenshot/image-20200429211135087.png)

when scaling,problem with multi-AZ of EBS

![image-20200429211151015](screenshot/image-20200429211151015.png)

### Storing Images with EFS

![image-20200429211312453](screenshot/image-20200429211312453.png)

### Summary

![image-20200429211401421](screenshot/image-20200429211401421.png)

## Five pillars:

- Cost

- Performance
- Reliability
- Security
- Operational excellence

## Instantiating Application quickly

- EC2 instances
  - Use a **Golden AMI**: install your applications,OS dependencies etc. beforehand and launch your EC2 instance from the Golden AMI
  - Bootstrap using User Data: for dynamic configuration,user data scripts
  - Hybrid: mix Golden AMI and User Data (Elastic Beanstalk)
- RDS Databases
  - Restore from a snapshot: the database will have schemas and data ready
- EBS volumes:
  - Restore from a snapshot: the disk will already be formatted and have data

## BeanStalk 

### Typical architecture Web App 3-tier

![image-20200429211753654](screenshot/image-20200429211753654.png)

### ElasticBeanStalk Overview

ElasticBeanstalk is a developer centric view of deploying an application on AWS

- Managed service
  - Instance configuration / OS is handled by Beanstalk
  - Deployment strategy is configurable but performed by Beanstalk
  - Just the application code is the responsibility of the developer
- Three architecture models:
  - Single Instance deployment: good for dev
  - LB + ASG: good for production or pre-production web applications
  - ASG only: good for non-web apps in production (workers,etc.)
- Three components:
  - Application
  - Application version: each deployment gets assigned a version
  - Environment name: free naming (DEV,TEST,PROD)
- You deploy application versions to environments and can promote application versions to the next environment
- Rollback feature to previous application version
- Full control over lifecycle of environments
- ![image-20200401224158436](.\screenshot\image-20200401224158436.png)

