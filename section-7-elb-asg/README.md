# Section 7: ELB and ASG

# 63: High Availabilty, Scalability, Elasticity
- Scalable: handle greater loads
  - Vertical
  - Horizontal (Elasticity)
- linked but different from High availablity

- Vertical:
  - increase the size of the instance
  - ex: t2.nano to t2.large
  - common for non distributed systems like databases
  - have a limit imposed by hardware

- Horizontal
  - add number of instances
  - distributed systems
  - web apps

### in terms of ec2
- scalable
  - vertically from t2.nano to u-12tb1.metal
  - horizontal: ASG and LB
- High Av: using multi AZ

### Scalability vs Elasticity vs Agility
- scalable: large load by scale
- Elasticity: auto scale as per load, to optimize cost and as per demand
- Agility: new resources are readily available

--- 

# ELB Overview

- spread across multiple instances
- expose single point of access one DNS to your app
- handle failures
- do health checks
- provide ssl certs
- high avail across AZ

### Why use an ELB?
- Managed by AWS in terms of:
  - it will be working
  - upgrades, maintainence, high av
  - only few config knobs

- our setup costs less, but far more effort
- 4 types:
  - ALB (application): http/https, layer 7
  - NLB (network): ultra high perf, tcp , layer 4
  - GLB (gateway): layer 3
  - CLB (classis) retired layer 4 & 7

### Difference

ALB          |         NLB        | GLB      
--- | --- | --- 
http/https/gRPC | tcp/udp proto | GENEVE proto on IP packets
http routing features | high perf, mil req per sec | route traffic to firewalls that you manage on ec2 instances |
static DNS(URL) | static IP via elastic IP | intrusion detection

---

# 65: ALB Hands on

- Launch 2 instances, paste same user data
- check the instance by going to the public IP
- go to load balances > create load balancer > alb
- give name > select all az
- create a new security group allowing only http inbound and all outbound
- create a new target group with instances and keep all defaults, add ur instances > click on **include pending from below**
- create the ALB and check the dns

---

# 66: ASG Overview

- load can vary over time
- can create new servers in cloud
- goal of ASG:
  - scale out (add ec2)
  - scale in (remove ec2)
  - ensure we have a min and max number of instances running
  - automatically register new instances to LB
  - replace unhealthy instances
### ASG in AWS
- can define
  - min size: 1
  - desired size
  - max size:
- work hand in hand with LB
- LB will send traffic to new ones being registered

---

# 67: ASG Hands On
- terminate the old 2 instances if not yet
- go to ASG and click create autoscaling groups
- Create a Launch Template (tells ASG on how to create the instances) > keeps options same as while creating ec2 instance so far
- select the launch template we just created
- select the zones
- chose existing LB and select the target group
- chose desired: 2, min: 1, max 4
- keep everything else same
- Create ASG

- check instances, target groups for new instances being created
- check the dns from the ALB
- try terminating one instance, our ASG will automatically create a new one
