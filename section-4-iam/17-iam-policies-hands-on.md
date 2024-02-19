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
