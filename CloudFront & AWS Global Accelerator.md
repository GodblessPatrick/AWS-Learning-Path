# CloudFront & AWS Global Accelerator

## AWS CloudFront

- Content Delivery Network (CDN)

- Improves **read** performance,content is cached at the edge

- 216 Point of Presence globally (edge locations)

- DDoS protection,integration with Shield,AWS Web Application Firewall

- Can expose external HTTPS and can talk to internal HTTPS backends

- ![image-20200406224909428](.\screenshot\image-20200406224909428.png)

  Bucket in Australia,User in U.S. and will  go access an edge location close to it and network is going to be transmitted over the private AWS network 

  Example: S3 Transfer Acceleration

### Origins

- S3 bucket
  - For distributing files and caching them at the edge
  - Enhanced security with CloudFront **Origin Access Identity (OAI)**
  - CloudFront can be used as an ingress (to upload file to S3)
- S3 website
  - Must first enable the bucket as a static S3 website
- Custom Origin (HTTP) - Must be publicly accessible
  - ALB
  - EC2 instance
  - Any HTTP backend you want
- ![image-20200406225618501](.\screenshot\image-20200406225618501.png)
- ![image-20200406225755011](.\screenshot\image-20200406225755011.png)

## CloudFront Geo Restriction

You can restrict who can access your distribution

- Whitelist: Allow your users to access your content only if they're in one of the countries on a list of approved countries
- Blacklist: Prevent your users from accessing your content only if they're in one of the countries on a list of approved countries
- Use Case: Copyright Laws to control access to content

### CloudFront Vs S3 Cross Region Replication

- CloudFront
  - Global Edge network
  - Files are cached for a TTL (time to live) maybe a day
  - **Great for static content that must be available everywhere**
- S3 Cross Region Replication
  - Must be setup for each region you want replication to happen
  - Filed are updated in near real-time
  - Read only
  - **Great for dynamic content that needs to be available at low-latency in few regions**

## CloudFront Signed URL/Cookies

You want to distribute paid shared content to premium users over the world

You can use CloudFront Signed URL / Cookie. We attach a policy with:

- Includes URL expiration
- Includes IP ranges to access the data from
- Trusted signers (which AWS accounts can create signed URLs)

How long should the URL be valid for?

- Shared content (movie,music): make it short (a few minutes)
- Private content (private to the user): you can make it last for years

Singed URL = access to the individual files (one signed URL per file)

Singed Cookies = access to multiple files (one signed cookie for many files)

![image-20200407215209064](.\screenshot\image-20200407215209064.png)

### CloudFront Signed URL Vs S3 Pre-Signed URL

- CloudFront Signed URL:
  - Allow access to a path, no matter the origin
  - Account wide key-pair, only the root can manage it
  - Can filter by IP, path, data, expiration
  - Can leverage caching features
  - ![image-20200407215540381](.\screenshot\image-20200407215540381.png)
- S3 Pre-Signed URL:
  - Issue a request as the person who pre-singed the URL
  - Uses the IAM key of the signing IAM principal
  - Limited lifetime
  - ![image-20200407215552021](.\screenshot\image-20200407215552021.png)

## AWS Global Accelerator

You have deployed an application and have global user who want to access it directly. They go over the public internet,which can add a lot of latency due to many hops

![image-20200407215821615](.\screenshot\image-20200407215821615.png)

We wish to go as fast as possible through AWS network to minimize latency

### Unicast IP Vs Anycast IP

### Unicast IP: 

one server holds one IP address

![image-20200407220327450](.\screenshot\image-20200407220327450.png)

### Anycast IP 

All servers hold the same IP address and the client is routed to the nearest one

![image-20200407220424405](.\screenshot\image-20200407220424405.png)

### AWS Global Accelerator

- Leverage the AWS internal network to route to your application
- 2 Anycast IP are created for your application
- The Anycast IP send traffic directly to Edge Locations
- The Edge location send the traffic to your application
- ![image-20200407220713643](.\screenshot\image-20200407220713643.png)
- Works with Elastic IP, EC2 instances,ALB,NLB,public or private
- Consistent Performance
  - Intelligent routing to lowest latency and fast regional failover
  - No issue with client cache (because the IP doesn't change)
  - Internal AWS network
- Health Checks
  - Global Accelerator performs a health check of your applications
  - Helps make your application global (failover less than 1 minute for unhealthy)
  - Great for disaster recovery
- Security
  - Only 2 external IP need to be whitelisted
  - DDoS protection thanks to AWS Shield

### AWS Global Accelerator Vs CloudFront

Same:

- They both use the AWS global network and its edge locations around the world
- Both services integrate with AWS Shield for DDoS protection

Different:

**CloudFront**

- Improves performance for both cacheable content (such as images and videos)
- Dynamic content (such as API acceleration and dynamic site delivery)
- Content is served at the edge

**AWS Global Accelerator**

- Improves performance for a wide range of applications over TCP or UDP
- Proxying packets at the edge to applications running one or more AWS region
- Good fit for no-HTTP use cases,such as gaming(UDP),IoT(MQTT) or Voice over IP
- Good for HTTP use cases that require static IP addresses
- Good for HTTP use cases that required deterministic,fast regional failover



