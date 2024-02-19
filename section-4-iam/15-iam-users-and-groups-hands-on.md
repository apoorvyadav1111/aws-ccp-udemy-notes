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
  
