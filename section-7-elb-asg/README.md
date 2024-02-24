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


