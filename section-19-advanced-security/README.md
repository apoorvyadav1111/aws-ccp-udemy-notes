# Section 19: Advanced Security

---

# 233: Security Token Service (STS) Overview
- enables to create temp priveleges creds
- short term creds: you configuration period
- use cases:
  - identity federation
  - iam roles for cross/same account access
  - iam roles for ec2
 
---

# 234: Cognito Overview
- Identity for your web and mobile apps
- create a user in cognito
- login with social app like google, facebook

---

# 235: Microsoft AD
- database of objects, user accounts, computers, printers, file shares, SG
- centralized security management, create account assign permissions

### AWS Directory Service
- AWS managed MS AD
  - create your own AD in AWS
  - establish trust connections with your on premise AD
 
- AD Connector
  - Directory gateway (proxy) to redirect to on premise AD
  - users are managed by on premise AD
- Single AD
  - AD compatible managed directory on AWS
  - cannot be joined with on premise AD

---

# 236: AWS IAM Identity Center
- one login sso for all your
  - aws accounts in aws organizations
  - business cloud apps
  - saml2.0
  - ec2 windows instances
- identity providers
  - built in identity store in IAM Identity Center
  - 3rd party AD, One Login, Okta
 
---

