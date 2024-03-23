# Section 15: VPC & Networking

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# 170: VPC Overview

---

# 171: Ip Address in AWS:
- IPv4: 4.3 Billion address
  - public ipv4 can be used on the internet
  - ec2 instance gets a new public ip address every time you start it
  - private ipv4 can be used on private networks  (lan) such as aws n/w
  - fixed for ec2
- elastic IP
  - fixed public ipv4
- IPv6: 3.4 * 10^38 address
  - every ip address is public (no private range)
  - free

---

# 172: VPC, Subnet, Internet gateway & NAT Gateway
- VPC:
  - private n/w to deploy your resources
  - within vpc, subnets allow partitioning
  - a public subnet is a subnet that is accessible from internet
  - private subnet is vice versa
  - to define access to the internet and between subnets, we use route tables
  - example: keeping databases in private subnet
  - VPC will have CIDR range: address in your vpc
- Internet Gateway
  - helps our vpc to connect with the internet
  - public subnets have a route to the internet gateway to connect to internet
  - private subnet need to access internet for os updates etc
    - create a nat gateway in public subnet which then allows private subnet internet access via itself
   
- Go to VPC
- when we create an account, a default vpc is created
- we get a cidr range
- use cidr xyz to check the range
- go to subnets
- might see 3 subnets for each AZ
- each subnet gets u different ipv4 cidr

- go to internet gateway
- one vpc on IG
- go to any subnet and click route table

---

# 173: Security Groups & NACL
- NACL:
  - firewall controlls traffic from and to subnet
  - can have allow and deny rules
  - attached at the subnet level
  - rules only include ip address
- SG:
  - firewall controls traffic from and to ENI/EC2 instance
  - can have only allow rules
  - rules include only IP address and other SGs

SG | NACL
--- | ---
operates at instance level | at subnet level
allow rules only | allow or deny
stateful return traffic allowed | stateless return traffic must be allowed explicitly
we evaluate all the rules before deciding whether to allow traffic | we process rules in number order when deciding to allow traffic
applicable to an instance when specified | applicable to all instances in the subnet

- go to default VPC and checkout NACL
- one NACL with all 3 subnets
- we can check inbound and outbound rules

---

# 174: VPC Flow Logs
- capture info about IP traffic into your interface
  - vpc flow logs
  - subnet flow logs
  - elastic networking interface flow logs
- Help to monitor and troubleshoot connectivity issues
  - subnet to internet
  - subnet to subnet
  - internet to subnet
 
- captures network information from aws managed interfaces too: ELB, elasticache, RDS, Aurora

### VPC Peering
- connect two vpc privately via aws network
- behave like they are on the same network
- must not have overlapping cidr
- they are not transitive: A <===> B <===> C, doesnt mean A<===>C

  
---

# 175: VPC Endpoints : Interface and Gateway (s3 and dynamodb)
- allows u to connect to aws services using private n/w instead of www
- enhances security and lower latency
- **vpc endpoint gateway**: **s3 and dynamodb**
- vpc endpoint interface: the rest
- go to vpc
  - click  endpoints
  - create a endpoint
  - find s3 and select it

---

# 176: PrivateLink
- from vpc endpoint service family
- most secure and scalable way to expose a service to 1000s of vpc
- does not need vpc peering, internet gateway, NAT, route tables
- 3rd party vpc running an app service, will establish private link to get access to their network LB. each customer need a new private link

---

# 177: Direct Connect and Site-to-Site VPn
- STS:
  - on premise VPN to aws
  - automatically encrypted
  - **goes over the public internet**
- Direct Connect(DX)
 - physical connection between on premise and aws
 - private, secure, fast
 - expensive than STS
 - atleast a month to establish

- STS:
  - on premise> must use a customer gateway
  - AWS must use a virtual private gateway
    
---

# 178: Client VPN
- connect via your computer using openvpn to your private n/w in aws and on premise
- allows connecting to your ec2 over a private IP as if you were in the private vpc
- goes over the public internet
  
---

# 179: Transit Gateway
- for having transitive peering between 1000s of vpc and on premise, hub-and-spoke connection
- one single gateway
- works with vpn connection

---
