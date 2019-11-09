### AWS CLI (Command Line Interface)

#### Fundamentals

The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services and automate them through scripts. 

Use `aws configure` command to set up security credentials (using `Access Key ID` and `Secret Access Key`). Your credentials are stored in `~/.aws` folder. However, you should not store your Access Key ID and Secret Access Key on individual EC2 instances for security reason. You should create role for an EC2, giving it the least privilege, and attach the role to the EC2 instance in order to use AWS CLI commands in it.

AWS CLI command structure, `aws <service> <command> <arguments>`.

Examples:

`aws ec2 describe-instances` shows all the EC2 instances

`aws s3 ls` lists all the S3 buckets

`aws s3 mb s3://bucketName` creates an S3 bucket

#### Dry runs

Some AWS CLI commands contain a `--dry-run` option to simulate API calls.

`aws ec2 run-instances --dry-run --image-id AMI_ID --instance-type t2.micro`

#### STS (Security Token Service) decode errors

STS can be used to decode additional information about the authorization status of a request from an encoded message returned in response to an AWS request.

`decode-authorization-message --encoded-message ERROR_MESSAGE`

#### AWS SDK (Software Developerment Kit)

AWS SDK is used to perform actions on AWS directly from your application code, such as communicating with DynamoDB in your code. AWS CLI actually uses the Python SDK.

#### Manage multiple CLI accounts

You can use different profiles to manage multiple CLI accounts.

- Create a new profile `aws configure --profile PROFILE_NAME`
- Check your new profile credential at `~/.aws/credentials`
- Use the new profile `aws s3 ls --profile PROFILE_NAME`
