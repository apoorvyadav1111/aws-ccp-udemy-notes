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

