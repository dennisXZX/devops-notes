### Lambda

- Lambda scales out automatically. 

- Lambda functions are independent (1 event = 1 function).

- AWS X-ray allows you to debug what is happening.

- Lambda can do things globally, for example, you can use it to back up S3 buckets to other S3 buckets.

- You can enable versioning for Lambda so you can have multiple versions of Lambda functions. You cannot edit a Lambda function once it's published as a version. You can only edit the `$LATEST` version.

- You can create an alias for a specific Lambda function version. You can split traffic using aliases to different versions.

You can use Lambda in the following ways:
  - As an event-driven compute service where AWS Lambda runs your code in response to events. These events could be changes to data in an S3 bucket or a DynamoDB table.
  - As a compute service to run your code in response to HTTP requests using AWS API Gateway or API calls made using AWS SDKs.
