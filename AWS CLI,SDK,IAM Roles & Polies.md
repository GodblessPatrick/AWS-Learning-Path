# AWS CLI,SDK,IAM Roles & Polies

Never put credentials inside of EC2 instance,using IAM Roles instead 

## EC2 Metadata

It allows AWS EC2 instances to "learn about themselves" without using an IAM Role for that purpose

The URL http://169.254.169.254/latest/meta-data/

You can retrieve the IAM Role name from the metadata,but you **cannot** retrieve the IAM policy

Metadata = Info about the EC2 instance

Userdata = launch script of the EC2 instance

## SDK

### Exponential Backoff

Any API that fails because of too many calls needs to be retried with Exponential Backoff

These apply to rate limited API

Retry mechanism included in SDK API calls

![image-20200402224052840](.\screenshot\image-20200402224052840.png)

First API call fails,wait for 1 ms,second fails, 2 ms wait,third fails,4 ms



