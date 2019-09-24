### AWS CLI

#### Fundamentals

`aws configure` sets up configure credentials in an EC2 (using `Access Key ID` and `Secret Access Key`). Your credentials are stored in `~/.aws` folder. However, you should not store your Access Key ID and Secret Access Key on individual EC2 instances for secruity reason. You should assign roles to an EC2 instance in order to use AWS CLI commands in it.

AWS CLI command structure, `aws <service> <command> <arguments>`.

Examples:

`aws s3 ls` lists all the S3 buckets

`aws s3 mb s3://bucketName` creates an S3 bucket
