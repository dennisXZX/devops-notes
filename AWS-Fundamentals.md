## AWS Fundamentals

- A region is a physical location in the world which consists of two or more Availability Zones (AZ)
- An AZ is one or more discrete data center
- Edge Location (CloudFront) is endpoint for AWS which is used for caching content
- Install AWS CLI bundled to programmatically connect to AWS

### Identity Access Management (IAM)

- IAM is universal. It does not apply to regions at this time

- Always set up multifactor authentication on your root account using `Google Authenticator`

- The 'root account' is simply the account created when first setup your AWS account. It has complete Admin access.

- New users have no permissions when first created

- New users are assigned `Access Key ID` and `Secret Access Keys` when first created, which can be used programatically access AWS (via APIs and command line). There are two different ways to access AWS, console access (via user and password) and programmatic access (via access key id). 

- A policy defines the AWS permissions that you can assign to a user, group, or role. 

- A role is to give entities permissions so that they act like users.

### CloudWatch

- Concerned mainly with what's happening with AWS resources so you can respond to it.

### CloudTrail

- Concerned mainly with 'who did what on AWS', for example, someone logged in from the AWS console, or someone shut down an EC2.

- Concerned with people within your account

- CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account

### S3 (Simple Storage Service)

- S3 is object based, which allows you to upload files (up to 5TB per file)

- A bucket is just like a folder, which needs to be unique globally. Each bucket you create would have a URL.

- When you upload a file to S3, you will receive an HTTP 200 code if the upload was successful.

#### Cross Region Replication

- Versioning must be enabled on both the source and destination buckets

- Files in an existing bucket are not replicated automatically. You need to copy them using command line `aws s3 cp --recursive s3://testbucket-by-dennis-versioning s3://test-by-dennis-replication-sydney`. All subsequent updated files will be replicated automatically

- Delete markers are NOT replicated

#### Lifecycle Management

- Can be used in conjunction with versioning

- Can be applied to current versions and previous versions

- Transition to the Standard - Infrequent Access (IA) Storage Class 30 days after creation date, archive to Glacier Storage Class 30 days after IA.
