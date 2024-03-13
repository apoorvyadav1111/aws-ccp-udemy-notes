# Section 18: Account Management, Billing and Support

# 213: Organizations Overview
- Global
- allows to manage multiple AWS account
- the main account is the master account
- cost benefit:
  - consolidated billing
  - pricing benefits from aggregated usage
  - pooling of reserved ec2  instances for optimal savings
- api is available to automate aws account creation
- restrict account privileges using SCP

### Multiaccount Strategies
- create accounts per department, per cost center, per dev, per test, based on regulatory restrictions
- multi account vs one account multivpc
- using tagging for billing
- enable cloud trail on all accounts, send logs to central s3 account

### Organization Units (OU)
- organize them
  - business unit
  - env lifecycle
  - project based

- organization
  - root ou
     - dev ou
     - prod ou
         - hr ou
         - finance ou
      
### SCP Service Control Policies
- whitelist or blacklist IAM actions
- applied at the ou or account level
- does not apply to master account
- is applied to all the users and roles of the account including root
- does not apply to service linked roles
- scp must have an explicit allow
- use cases:
  - restrict access to certain services, for example, cant use EMR
  - enforce PCI compliance

---

# 214: Organizations hands on

---

# 215: 
