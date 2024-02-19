# IAM Users and Groups

IAM = Identity and Access Management, Global service

Root account created by default, should be used or shared but only be used to create users.

Users are  people from the organization and can be grouped together. Groups can only contain users.

### IAM: Permissions
- Users or Groups can be assigned json documents called **policies**.
```
{
  "Version":"2024-01-01",
  "Statement": [
      {
        "Effect":"Allow",
        "Action":"ec2:Describe",
        "Resource":"*
      }
  ]
}
```
- policies define the permissions of the users
- **lease privilege permission** in AWS. only allow what is needed.
