# Network - VPC

## CIDR, Private Vs Public IP

### Understanding CIDR - IPv4

![image-20200416204716327](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416204716327.png)

![image-20200416204817789](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416204817789.png)

#### Subnet Mask

![image-20200416205010948](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416205010948.png)

![image-20200416205121503](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416205121503.png)

### Private Vs Public IP (IPv4)

#### Allowed ranges

![image-20200416205412564](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416205412564.png)

## Default VPC

![image-20200416205916728](C:\Users\boyan\AppData\Roaming\Typora\typora-user-images\image-20200416205916728.png)

## VPC - Overview

![image-20200416210533428](screenshot/image-20200416210533428.png)

### Adding Subnets

![image-20200416210954069](screenshot/image-20200416210954069.png)

![image-20200416211509215](screenshot/image-20200416211509215.png)

## Internet Gateway & Route Tables

### Internet Gateway

![image-20200416212006071](screenshot/image-20200416212006071.png)

### Adding IGW

![image-20200416212026228](screenshot/image-20200416212026228.png)

### Editing Route Tables

![image-20200416212216089](screenshot/image-20200416212216089.png)

## NAT Instance

![image-20200416212920549](screenshot/image-20200416212920549.png)

![image-20200416213012599](screenshot/image-20200416213012599.png)

### Comments

![image-20200416214105265](screenshot/image-20200416214105265.png)

## NAT Gateways

![image-20200416214217186](screenshot/image-20200416214217186.png)

![image-20200416214447372](screenshot/image-20200416214447372.png)

### NAT Gateway with High Availability 

![image-20200416214603703](screenshot/image-20200416214603703.png)

### NAT Gateway Vs Instance

## DNS Resolution Options & Route 53 Private Zones

![image-20200416215347959](screenshot/image-20200416215347959.png)

## NACL & Security Group

### Incoming Request

![image-20200416220116083](screenshot/image-20200416220116083.png)

If the inbound rules pass,the outbound will also pass automatically(stateful). But NACL outbound rules will evaluate again

### Outgoing Request

 ![image-20200416220327960](screenshot/image-20200416220327960.png)

### Network ACLs

![image-20200416220716877](screenshot/image-20200416220716877.png)

### Network ACLs Vs Security Group

![image-20200416221342660](screenshot/image-20200416221342660.png)

**Ephemeral port**

## VPC Peering

![image-20200416221838682](screenshot/image-20200416221838682.png)

![image-20200416221938451](screenshot/image-20200416221938451.png)

![image-20200416221954662](screenshot/image-20200416221954662.png)

## VPC Endpoints

![image-20200420200315270](screenshot/image-20200420200315270.png)

![image-20200420200414750](screenshot/image-20200420200414750.png)

**try to specify the region when you use endpoint** e.g. when `ls` S3 bucket,use 

`aws s3 ls --region eu-west-1`

## VPC Flow Logs

![image-20200420201247145](screenshot/image-20200420201247145.png)

![image-20200420201316673](screenshot/image-20200420201316673.png)

### Flow Logs Syntax

![image-20200420201431463](screenshot/image-20200420201431463.png)

**Use Athena to do analysis on Flow logs**

## Bastion Hosts

![image-20200420204336542](screenshot/image-20200420204336542.png)

## Site to Site VPN, Virtual Private Gateway & Customer Gateway

![image-20200420204559734](screenshot/image-20200420204559734.png)

### Site to Site VPN

![image-20200420204729110](screenshot/image-20200420204729110.png)

## Direct Connect & Direct Connect Gateway

![image-20200420205208105](screenshot/image-20200420205208105.png)

![image-20200420205309564](screenshot/image-20200420205309564.png)

### Direct Connect Gateway

![image-20200420205423446](screenshot/image-20200420205423446.png)

**VPCs are not connected,not peered**

#### Connections Types

![image-20200420205622480](screenshot/image-20200420205622480.png)

#### Encryption

![image-20200420205742724](screenshot/image-20200420205742724.png)

## Egress only Internet Gateway

Egress = outgoing

![image-20200420210049851](screenshot/image-20200420210049851.png)

## AWS PrivateLink - VPC Endpoint Services

### Exposing services in your VPC to other VPC

![image-20200420210324557](screenshot/image-20200420210324557.png)

![image-20200420210353829](screenshot/image-20200420210353829.png)

### AWS Private Link (VPC Endpoint Services)

![image-20200420210505108](screenshot/image-20200420210505108.png)

## AWS ClassicLink

![image-20200420210811386](screenshot/image-20200420210811386.png)

## VPN CloudHub

![image-20200420210932177](screenshot/image-20200420210932177.png)

## Transit Gateway

Network topologies can become complicated



![image-20200420211140514](screenshot/image-20200420211140514.png)

![image-20200420211318682](screenshot/image-20200420211318682.png)

## VPC Section Summary

![image-20200420211548131](screenshot/image-20200420211548131.png)

### Summary(1/3)

![image-20200420211826553](screenshot/image-20200420211826553.png)

### Summary(2/3)

![image-20200420212029497](screenshot/image-20200420212029497.png)

### Summary(3/3)

![image-20200420212120740](screenshot/image-20200420212120740.png)

## Networking Costs in AWS

![image-20200420213237869](screenshot/image-20200420213237869.png)

