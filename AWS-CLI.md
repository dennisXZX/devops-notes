### AWS CLI (Command Line Interface)

#### Fundamentals

The AWS Command Line Interface (CLI) is a unified tool to manage your AWS services and automate them through scripts. 

Use `aws configure` command to set up security credentials (using `Access Key ID` and `Secret Access Key`). Your credentials are stored in `~/.aws` folder. However, you should not store your Access Key ID and Secret Access Key on individual EC2 instances for security reason. You should assign roles to an EC2 instance in order to use AWS CLI commands in it.

AWS CLI command structure, `aws <service> <command> <arguments>`.

Examples:

`aws ec2 describe-instances` shows all the EC2 instances

`aws s3 ls` lists all the S3 buckets

`aws s3 mb s3://bucketName` creates an S3 bucket
