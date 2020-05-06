# EBS & EFS

## What's an EBS Volume?

An EC2 machine loses its root volume (main drive) when it is manually terminated,<u>EBS(Elastic Block Store</u>) is a network drive you can attach to your instances while they run

EBS uses network to communicate the instance,which means there might be a bit of latency

EBS is locked to an AZ

EBS has a provisioned capacity

## Type

### GP2

- Recommended for most workloads
- System boot volumes
- Virtual desktops
- Low-latency interactive apps
- Development and test environments
- 1 GB - 16 TB
- small gb2 volumes can burst IOPS to 3000
- Max IOPS is 16000, 3 IOPS per GB, such that 5334 GB will be at max IOPS 

### IO1

- Critical business applications that require sustained IOPS performance,or more than 16000 IOPS per volume
- Larger database workloads
- 4 GB - 16 TB
- IOPS is provisioned (PIOPS)  min 100, max 64000(Nitro) 32000(other instance)
- the max ratio of provisioned IOPS to requested volume size is 50:1 (GB)

### STI

- Steaming workloads requiring consistent,fast throughput at a low price
- Big data,data warehouses,log processing
- Cannot be a boot volume
- 500 GB - 16 TB
- Max IOPS 500
- Max throughput 500 MB/S (can burst)

### SCI

- Throughput-oriented storage for large volumes of data that is infrequently accessed
- The lowest storage cost is important
- Cannot be a boot volume
- 500 GB - 16 TB
- Max IOPS 250
- Max throughput 250 MB/S (can burst)

## Snapshots

- Incremental - only backup changed blocks
- EBS backups use IO and you should not run them while your application is handling a lot of traffic
- Snapshots will be stored in S3(you won't see them directly)
- Not necessary to detach volume to do snapshot but recommended
- Max 100000 snapshots
- Can copy snapshots across AZ or Region
- Can make Image (AMI) from Snapshot
- EBS volumes restored by snapshots need to be pre-warmed (using fio or dd command to read the entire volume)
- Snapshots can be automated using Amazon Data Lifecycle Manager

## EBS Migration

EBS volumes are only locked to a specific AZ,to migrate it to a different AZ(or region)

- Snapshot the volume
- (optional)Copy the volume to a different region
- Create a volume from the snapshot in the AZ of your choice

## Encryption

When you create an encrypted EBS volume ,you get the followings

- Data at rest is encrypted inside the volume
- All the data in flight between the instance and the volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot
- Copying an unencrypted snapshot allows encryption
- Snapshot of encrypted volumes are encrypted

Encrypt an unencrypted EBS volume:

1. Create an EBS snapshot of the volume
2. Encrypt the EBS snapshot (using copy)
3. Create new EBS volume from the snapshot (the volume will also be encrypted)
4. Now you can attach the encrypted volume to the original instance

## EBS VS Instance Store

Some instance do not come with Root EBS volumes,instead they come with "Instance Store(ephemeral storage)"

Instance store is physically attached to the machine (EBS is network drive)

**PROS**(Instance Store)

- Better I/O performance
- Good for buffer/cache/scratch data/temporary content
- Data survives reboots

**CONS**:

- On stop or termination,the instance store is lost
- You cannot resize the instance store
- Backups must be operated by the user

Ask yourself "Am I ok losing my date" : Yes => instance store No => EBS

## EBS RAID

you would mount volumes in parallel in RAID settings and RAID is possible as long as your OS supports it

RAID options: 

- RAID 0
  - increase performance
  - combine 2 or more volumes and getting the total disk space and I/O
  - but one disk fails,all date is failed
  - Example: two 500 GB Amazon EBS iol volumes with 4000 IOPS will create 1000 GB RAID 0 array with an available bandwidth of 8000 IOPS and 1000MB/s of throughput
- RAID 1
  - increase fault tolerance
  - mirroring a volume to another
  - if one disk fails,our logical volume is still working. We have to send the data to two EBS volume at the same time (2x network)
  - Example: two 500 GB Amazon EBS iol volumes with 4000 IOPS will create 500 GB RAID 1 array with an available bandwidth of4000 IOPS and 500MB/s of throughput
- RAID 5 (not recommended for EBS)
- RAID 6 (not recommended for EBS)

## EFS

Elastic File System

- Managed NFS (network file system) that can be mounted on many EC2
- EFS works with EC2 instances in multi-AZ
- Highly available,scalable,expensive (3xgp2),pay per use
- Uses NFSv4.1 protocol
- Uses security group to control access to EFS
- Compatible with Linux based AMI (not Windows)
- Performance mode:
  - general purpose (default)
  - max I/O - used when thousands of EC2 are using the EFS
- EFS file sync to sync from on-premise file system to EFS
- Backup EFS-to-EFS (incremental - can choose frequency)
- Encryption at rest using KMS

Use cases: **content management**,**web serving** , **data sharing**, **Wordpress**

## EBS & EFS for Solutions Architect

- EBS volumes can be attached to only one instance at a time
- EBS volumes are locked to the AZ level
- Migrating an EBS volume across AZ means first backing it up (snapshot),the recreating it in the other AZ
- EBS backups use I/O and you shouldn't run then while your application is handling a lot of traffic
- Root EBS Volumes of instances get terminated by default if the EC2 instance get terminated
- Disk IO is high => increase EBS volume size (for gp2)
- EFS mounting 100s of instances
- EFS share website files
- EBS gp2,optimize on cost
- Custom AMI for faster deploy on ASG
- EFS vs EBS vs Instance Store
  - EFS: for many instances,cross AZ
  - EBS: local storage but portable
  - Instance Store: actually volume,cannot attach or detach it,higher performance