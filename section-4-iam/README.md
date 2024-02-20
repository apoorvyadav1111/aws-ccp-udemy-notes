# Section 4: IAM

[🏠 Go to Home](https://apoorvyadav1111.github.io/aws-ccp-udemy-notes/)

---

# IAM Users and Groups

IAM = Identity and Access Management, Global service

Root account created by default, should be used or shared but only be used to create users.

Users are  people from the organization and can be grouped together. Groups can only contain users.

### IAM: Permissions
- Users or Groups can be assigned json documents called **policies**.
```
{
  "Version":"2012-10-17",
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

  ---

# IAM: Users and Groups

### Hand ons experiment
- Go to console > IAM > Users
- Notice the region is disabled as IAM is global service
- We create user because we are using root account right now, which is bad practice
- Create User
  - Create user
  - Add your name
  - check allow access the management console, since it will be used by us.
  - User type: I want to create an IAM User
  - Auto passwords and require user to change password on next sign in is to be used when creating other user
  - Create Group
    - Enter Name
    - Add permissions, here we added adminpermissions
  - Go to next and review.

Once created we can see users and groups. User can be seen having permission but given to them _via_ group. 

### Creating Alias
- In order to sign in using IAM user, we need to use either out account id or an alias
- creating alias is better since its human readable
- to create it:
  - in root account console, go to IAM
  - on the right side, under the account id, create alias
  - use this new url to login via iam user created before
  - old url is still valid

--- 

# IAM: Policies

**IAM Policies Inheritance**
- In policies at group level, each user in group will get the same permission
- Inline policy belong to a user
- If a user is a part of two groups, they will inherit from both groups. If they had inline policy, they will inherit that too.


**IAM policy structure**
- "Version": Language version, always include "2012-10-17"
- "Id": identifier of the policy (optional)
- "Statement":One of more individual statements (required)
**Statement**
  - "Sid":id of the statement, _optional_
  - "Effect": Allow, Deny
  - "Principal": account/user/role this policy applies to
  - "Action": list of api calls, denied or allowed
  - "Resource":"list of resources to which actions applied to"
  - "Condition":When this policy in in effect, _optional_
 
    ---

# IAM Policies Hands On

- Updating Permissions of a user
  - Using Root, go to the IAM>Groups>admin
  - Remove the user from the group
  - user will not be able to check users in the IAM Console now
  - Using Root, go to the IAM>Users>user_name
  - Click on add permissions> add permissions > Attach policies Directly > IAMreadonlyaccess

Now the user will be able to see the list of users and groups and their details but would not be able to modify them.
**Creating Policy**
**Use Root**
- Go to IAM>policies
- Check out the predefined policies, json and summary
- Create Policy > Use Visual/JSON> Add Name
- Check out the policy

  ---

# IAM - MFA

**Password Policy**
- can setup a pwd policy: length, specific char type
- allow or not to change their pwd
- pwd expiry dates
- prevent reuse

**Multi Factor Authentication - MFA**
- want to protect root and IAM users
- MFA = pwd + security device
- unauthorized individual with a pwd will not be able to do until they have the device
- Device Options
  - Virtual: Google Authenticator (phone only), Authy (multi-device)
  - Universal: U2F security Key example: YubiKey
  - Hardware Key Fob MFA Device,ex Gemalto, SurePassID

  ---


# IAM MFA Hands On

**Password Policy**
Using Root:
- Go to IAM > Account Settings > Password Policy
- Edit > Custom

**MFA**
Using Root
- Click on the account name on the nav
- Click on the **security credentials**
- Assign MFA
  - Name
  - Select Device > Select authenticator app > select app from list
  - Scan QR Code
  - You need to put the MFA code from the app twice in the console for verification
  - Click Add MFA

Can assign up to 8 devices at one time. 


---
