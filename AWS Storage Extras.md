# AWS Storage Extras

## Snowball

- physical data transport solution that helps moving TBs or PBs of data in or out of AWS
- Alternative to moving data over the network (and pay network fees)
- Secure,tamper resistant,uses KMS 256 bit encryption
- Tracking using SNS and text messages,E-ink shipping label
- Pay per data transfer job
- Use cases: large data cloud migrations,DC decommission,disaster recovery
- If it takes more than a week to transfer over the network,use Snowball devices

### Snowball Process

1. Request snowball devices from the AWS console for delivery
2. Install the snowball client on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you're done (goes to the right AWS facility)
5. Data will be loaded into an S3 bucket
6. Tracking is done using SNS,text messages and the AWS console

![image-20200407223853155](.\screenshot\image-20200407223853155.png)

### Snowball Edge

- Snowball Edges add computational capability to the device
- 100 TB capacity with either
  - Storage optimized - 24 vCPU
  - Compute optimized - 52 vCPU & optional GPU
- Support a custom EC2 AMI so you can perform processing on the go
- Supports custom Lambda functions
- Very useful to pre-process the data while moving
- Use cases: data migration, image collation, IoT, capture, ML

![image-20200407224221305](.\screenshot\image-20200407224221305.png)

### Snowball into Glacier

- Snowball cannot import to Glacier directly
- You have to use S3 first and a S3 Lifecyle policy
- ![image-20200407224403982](.\screenshot\image-20200407224403982.png)

## Storage Gateway

![image-20200407224914233](.\screenshot\image-20200407224914233.png)

Storage Gateway brings the bridge with these solutions

Example:

Bridge between on-premise data and cloud data in S3

Use cases: disaster recovery, backup & restore, tiered storage

3 types of Storage Gateway:

- FIle Gateway
- Volume Gateway
- Tape Gateway

![image-20200407225155942](.\screenshot\image-20200407225155942.png)

- File Gateway:
  - Configured S3 buckets are accessible using **NFS** and **SMB** protocol
  - Supports S3 standard,S3 IA,S3 One Zone IA
  - Bucket access using IAM roles for each File Gateway
  - Most recently used data is cached in the file Gateway
  - Can be mounted on many servers
  - ![image-20200407225531013](.\screenshot\image-20200407225531013.png)
- Volume Gateway
  - Block storage using **iSCSI** protocol backed by S3
  - Backed by EBS snapshots which can help restore on-premise volumes
  - Cached volumes: low latency access to most recent data
  - Stored volumes: entire dataset is on-premise,scheduled backups to S3
  - ![image-20200407225828983](.\screenshot\image-20200407225828983.png)
- Tape Gateway
  - Some companies have backup processes using physical tapes
  - With Tape Gateway,companies use the same processes but in the cloud
  - **Virtual Tape Library (VTL)** backed by S3 and Glacier
  - Back up data using existing tape-based processes (and iSCSI interface)
  - Works with leading backup software vendors
  - ![image-20200407230133220](.\screenshot\image-20200407230133220.png)

**Summary**:

High level: On premise data to the cloud => Storage Gateway

File access / NFS => File Gateway (backed by S3)

Volumes / Block Storage / iSCSI => volume gateway (backed by S3  with EBS snapshots)

VTL Tape solution / Backup with iSCSI = > Tape Gateway (backed by S3 and Glacier)

## Amazon FSx for Windows (File Server)

- EFS is a shared POSIX system for Linux system
- **FSx** for Windows is a fully managed Windows file system share drive
- Supports SMB protocol & Windows NTFS
- Microsoft Active Directory integration,ACLs,user quotas
- Built on SSD,scale up to 10s of GB/s,millions of IOPs,100s PB of data
- Can be accessed from your on-premise infrastructure
- Can be configured to Multi-AZ (high availability)
- Data is backed-yp daily to S3

## Amazon FSx for Lustre

- Lustre is a type of parallel distributed file system,for large-scale computing
- Lustre = "Linux" + "Cluster"
- Use cases: ML, **High Performance Computing (HPC) **,video processing,Financial Modelling,Electronic Design Automation
- Scales up to 100s GB/s,millions of IOPs,sub-ms latencies
- Seamless integration with S3
  - Can "read S3" as a file system (through FSx)
  - Can write the output of the computations back to S3 (through FSx)
- Can be used from on-premise servers

## Storage Comparison

- S3:**Object Storage**
- Glacier: **Object Archival**
- EFS: Network File System for **Linux** instances, POSIX filesystem
- EBS volumes: **Network storage** for one EC2 instance at a time
- Instance Storage: **Physical Storage** for your EC2 instance (high IOPs)
- FSx for Windows: Network File System for **Windows** servers
- FSx for Lustre: **High Performance Computation** Linux file system
- Storage Gateway: **File Gateway**, **Volume Gateway** (cache & stored),**Tape Gateway**
- Snowball / Snowmobile: to move large amount of data to the cloud,**physically**
- Database: for specific workloads,usually with **indexing and querying**