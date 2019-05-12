### AWS - Identity and Access Management (IAM)

- IAM is universal. It does not apply to regions at this time

- Always set up multifactor authentication on your root account using `Google Authenticator`

- The 'root account' is simply the account created when first setup your AWS account. It has complete Admin access.

- New users have no permissions when first created

- New users are assigned `Access Key ID` and `Secret Access Keys` when first created, which can be used programatically access AWS (via APIs and command line). There are two different ways to access AWS, console access (via user and password) and programmatic access (via access key id). 

- A policy defines the AWS permissions that you can assign to a user, group, or role. 

- A role is to give entities permissions so that they act like users.
