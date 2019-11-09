### Elastic BeanStalk

Three architecture models:

- Single Instance deployment: good for dev
- ELB + ASG: great for production or pre-production web apps
- ASG only: great for non-web apps in production (workers)

__Deployment process__

- Create an app

- Create environments (dev, testing, prod)
  - You can modify environment config during this stage
  - An S3 bucket is created to store environment data

- Upload version

- Release to environments

__Deployment policy__

- All at once (deploy all in one go): fastest, but instances aren't available to serve traffic for a bit (downtime). 
  - Fastest deployment
  - App has downtime
  - Great for quick iterations in development environment
  - No additional cost

- Rolling: update a few instances at a time (bucket), and then move onto the next bucket once and first bucket is healthy.
  - App is running below capacity
  - You can set the bucket size
  - App is running both versions simultaneously
  - No additional cost
  - Long deployment if bucket size is small

- Rolling with additional batches: like rolling, but spins up new instances to move the batch (so that the old application is still available).
  - App is running at capacity
  - You can set the bucket size
  - App is running both versions simultaneously
  - Small additional cost
  - Additional batch is removed at the end of the deployment
  - Longer deployment
  - Good for production deployment
  
- Immutable: spins up new instances in a new ASG, deploys version to these instances, and then swaps all the instances when everything is healthy.
  - Zero downtime
  - New code is deployed to new instances on a temporary ASG
  - High cost, double capacity
  - Longest deployment
  - Quick rollback in case of failures (just terminate new ASG)
  - Good for production deployment
  
- Blue / Green
  - Zero downtime
  - Create a new 'stage' environment and deploy v2 there
  - The new environment (green) can be validated independently
  - Can roll back to current environment (blue) if there are issues during deployment
  - Route 53 can be setup using weighted policies to redirect a little bit of traffic to the stage environment
  - Using Beanstalk 'swap URLs' when done with the environment test
