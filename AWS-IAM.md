### Identity and Access Management (IAM)

- IAM is universal. It does not apply to regions.

- Always set up multifactor authentication on your root account using `Google Authenticator` app.

- The `root account` is simply the account created when first setup your AWS account. It has complete admin access. We should always set up administrative users under root account to manage AWS services.

- New users have no permissions when first created (least privilege principle). You should always use groups (policies attached to groups) to assign permissions to users.

- New users are assigned `Access Key ID` and `Secret Access Keys` when first created, which can be used programatically access AWS (via APIs or command line). You only get to view the generated `Access Key ID` and `Secret Access Keys` once. If you lose them, you have to regenerate them. There are two different ways to access AWS, console access (using `username` and `password`) and programmatic access (using `Access Key ID` and `Secret Access Keys`).

- A policy (in JSON format) defines the AWS permissions that you can assign to a user, group or role. It consists of an effect (allow or deny), service, action and resource. You can test your policy using `IAM Policy Simulator`.

- A user policy is an inline policy embedded in a user. A group policy is an inline policy embedded in a group.

- A role is for internal usage within AWS resources. It gives entities permissions so that they act like users. For example, you can give an EC2 instance full access to S3.

#### IAM Federation

- Big enterprises usually integrate their own repository of users with IAM. This way, one can login into AWS using their company credentials. Identity Federation uses SAML (Security Assertion Markup Language) standard.
