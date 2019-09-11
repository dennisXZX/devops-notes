### CloudTrail

- CloudTrail basically tracks events. You can create a trail to log management events (management operations that are performed on resources in your AWS account) and data events (resource operations performed on or within a resource, such as, S3 or Lambda). These logs are stored in S3 so you should watch out for what you are logging to avoid unnecessary costs. 

- You can also deliver events recorded from CloudTrail to CloudWatch Logs group. CloudWatch Logs aggregates logs from CloudTrail and non-AWS sources and provides interface to view and search logs.

- You can use Athena to search CloudTrail logs. Athena allows you to perform SQL-based queries against objects in S3.
