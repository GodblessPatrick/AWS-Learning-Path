# IAM Advanced

##  Security Token Service (STS)

![image-20200415212316255](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415212316255.png)

 ### Using STS to Assume a Role

![image-20200415212507850](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415212507850.png)

### Cross account access with STS

![image-20200415212647669](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415212647669.png)

## Identity Federation & Cognito

![image-20200415212834717](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415212834717.png)

### SAML 2.0 Federation

![image-20200415213032912](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213032912.png)

### SAML 2.0 Federation - Active Directory FS

![image-20200415213202408](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213202408.png)

![image-20200415213248347](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213248347.png)

### Custom Identity Broker Application

![image-20200415213355135](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213355135.png)

### Web Identity Federation - AssumeRoleWithWebIdentity

![image-20200415213516401](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213516401.png)

### AWS Cognito

![image-20200415213656508](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213656508.png)

## Directory Services

### Microsoft Active Directory (AD)

![image-20200415213833679](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415213833679.png)

### AWS Directory Services

![image-20200415214308057](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415214308057.png)

## AWS Organizations

![image-20200415214617322](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415214617322.png)

![image-20200415214755380](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415214755380.png)

### Organizational Units (OU) - examples

![image-20200415214922154](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415214922154.png)

### Service Control Policies (SCP)

![image-20200415215245751](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415215245751.png)

![image-20200415215521738](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415215521738.png)

### Moving Accounts

![image-20200415215654489](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415215654489.png)

## IAM Advanced

### IAM Conditions

![image-20200429235742405](screenshot/image-20200429235742405.png)

![image-20200415221052470](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415221052470.png)

### IAM for S3

![image-20200415221225512](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415221225512.png)

### IAM Roles Vs Resource based policies

![image-20200415221317758](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415221317758.png)

![image-20200415221415951](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415221415951.png)

## IAM - Policy Evaluation Logic

![image-20200415221617574](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415221617574.png)

IAM Permission Boundary => only allow actions on S3,CloudWatch and EC2

IAM Permissions Through IAM Policy => create user => out of Permission Boundary => No Permissions

![image-20200415222008546](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222008546.png)

![image-20200415222154398](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222154398.png)

Example:

![image-20200415222258819](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222258819.png)

![image-20200415222306469](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222306469.png)

No,since there is explicit deny on SQS:*

![image-20200415222348775](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222348775.png)

No, since there is explicit deny on SQS:*

**Whenever we have a explicit deny,the answer should be deny**

![image-20200415222440866](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222440866.png)

No,since there is no explicit deny and allow and everything in AWS remains deny at beginning,so it deny

## Resource Access Manager (RAM)

![image-20200415222655532](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222655532.png)

### VPC Example

![image-20200415222918550](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415222918550.png)

Account 1 cannot view,modify or delete EC2 of account2,vice versa

But all applications in this private subnet can access each other

## Single Sign-On (SSO)

![image-20200415223254809](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415223254809.png)

### Setup with AD

![image-20200415223439309](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415223439309.png)

### SSO Vs AssumeRoleWithSAML

![image-20200415223558834](C:\Users\boyan\Desktop\AWS\AWS_Certified Solutions Architect Associate\screenshot\image-20200415223558834.png)



