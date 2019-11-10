### CodeCommit

You can trigger notifications in CodeCommit using AWS SNS (Simple Notification Service), AWS Lambda or AWS CloudWatch Event Rules.

Use cases for SNS / AWS Lambda notifications:

- Deletion of branches
- Trigger for pushes that happens in master branch
- Notify external build system
- Trigger AWS Lambda function to perform codebase analysis

Use cases for AWS CloudWatch Event Rules:

- Trigger for pull request updates (created / updated / deleted / commented)

### CodeBuild

Building and testing our code

### CodeDeploy

Deploying code to EC2 fleets

### CodePipeline

Automating our pipeline from code to Elastic Beanstalk
