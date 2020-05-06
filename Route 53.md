# Route 53

## Overview 

Route53 is a Managed DNS

In AWS,the most common records are:

- A: URL to IPv4
- AAAA: URL to IPv6
- CNAME: URL to URL
- Alias: URL to AWS resource

Can use: public domain names you own,private domain names that can be resolved by your instances in your VPCs

Route53 has advantages features such as:

- Load balancing (through DNS,also called client load balancing)
- Health checks
- Routing policy: simple,failover,geolocation,latency,weighted,multi value

No free service

## How work

![image-20200331214610126](.\screenshot\image-20200331214610126.png)

## TTL

Time to Live

![image-20200331220337431](.\screenshot\image-20200331220337431.png)

low value of TTL => more queries to Route53

high value of TTL => really hard to change the values and changes

## CNAME Vs Alias

AWS resources expose an AWS URL: lbl-1234.us-east-2.elb.amazon.com

CNAME:

- Points a URL to any other URL
- <u>**ONLY for non root domain (aka something.mydomain.com, not mydomain.com)**</u>

Alias:

- Points a URL to an AWS Resources (app.mydomian.com => blabla.amazonaws.com)
- <u>**Works for root domain and non root domain (aka mydomain.com)**</u>
- Free of charge
- Native health check

## Simple Routing Policy

Maps a domain to one URL

Use when you need to redirect to a single resource

You **cannot** attach health checks to simple routing policy

If multiple values are returned, a random one is chosen by the **client**(from browser chooses)

## Weighted Routing Policy

Control the %  of the requests that go to specific endpoint

Helpful to test 1% of traffic on new app version for example

Helpful to split traffic between two regions

Can be associated with Health Checks

The sum of % does not need to be 100%

![image-20200331222544315](.\screenshot\image-20200331222544315.png)

## Latency Routing Policy

Redirect to the server that has the least latency close to us

Super helpful when latency of users is a priority

<u>**Latency is evaluated in terms of users to designated AWS Region**</u>

![image-20200331223523592](.\screenshot\image-20200331223523592.png)

## Health Checks

If some endpoints are not healthy, Route53 will not redirect to these endpoints

Have X health checks failed => unhealthy (default 3)

Have X health checks passed => health (default 3)

Default Health Check Interval: 30s (can set to 10s - higher cost)

About 15 health checker will check the endpoint health => one request every 2 sec on avg.

Can have HTTP,TCP and HTTPS health checks (no SSL verification)

Possibility of integrating the health check with CloudWatch

<u>Health checks can be linked to Route53 DNS queries</u> 

## Failover Routing Policy

![image-20200331225010270](.\screenshot\image-20200331225010270.png)

## Geo Location Routing Policy

Different from Latency based,this policy is based on user location

Should create a <u>"default"</u> policy (in case there's no match on location)

![image-20200401202155366](.\screenshot\image-20200401202155366.png)

## Multi Value Routing Policy

Use when routing traffic to multiple resources

Want to associate a Route53 health checks with records

Up to 8 healthy records are returned for each Multi Value query

Multi Value is **Not** a **substitute** for having an ELB

![image-20200401202823332](.\screenshot\image-20200401202823332.png)

## 3rd Party Domains & Route53

A domain name registrar is an organization that manages the reservation of Internet domain names

Domain Registrar **!=** DNS

If you buy your domain on 3rd party website,you can still use Route53,how?

- create a public Hosted Zone in route53
- update NS records on 3rd party website to use Route53 named servers