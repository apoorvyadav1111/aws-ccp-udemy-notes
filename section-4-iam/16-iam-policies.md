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
