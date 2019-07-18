### EC2 (Elastic Compute Cloud)

#### Fundamentals

EC2 is a wb service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.

- termination protection is turned off by default, you must turn it on

- on an EBS-backed instance, the default action is for the root EBS (Elastic Block Store) volume to be deleted when the instance is terminated

- EBS Root volumes of your DEFAULT AMI cannot be encrypted. You can use a third party tool (bit locker) to encrypt the root volume, or this can be done when creating AMI in the AWS console or using the API

- additional volumes can be encrypted

#### Security group

- all inbound traffic is blocked by default

- all outbound traffic is allowed

- changes to Security Groups take effect immediately

- you can have any number of EC2 instances within a secruity group

- you can have multiple security groups attached to EC2 instances

- you cannot bloack specific IP addresses using Security Group, instead use Network Access Control Lists

- you can specify allow rules, but not deny rules

__Pricing types__

On Demand - allows you to pay a fixed rate by the hour (or by the second) with no commitment

Reserved - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 year or 3 year terms.

Spot - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. If the spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

Dedicated Hosts - physical EC2 server dedicated for your use.

