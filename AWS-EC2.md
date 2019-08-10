### EC2 (Elastic Compute Cloud)

#### Fundamentals

EC2 is a web service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change.

- termination protection is turned off by default, you must turn it on

- on an EBS-backed instance, the default action is for the root EBS (Elastic Block Store) volume to be deleted when the instance is terminated, however, the additional volumes would be persisted.

- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data. EBS-backed instance can be stopped. You will not lose the data on this instance if it is stopped.

#### Security group

- all inbound traffic is blocked by default

- all outbound traffic is allowed

- changes to Security Groups take effect immediately

- you can have any number of EC2 instances within a secruity group

- you can have multiple security groups attached to EC2 instances

- if you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again

- you cannot block specific IP addresses using Security Group, instead use Network Access Control Lists

- you can specify allow rules, but not deny rules

#### Pricing types

On Demand - allows you to pay a fixed rate by the hour (or by the second) with no commitment

Reserved - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 year or 3 year terms.

Spot - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. If the spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

Dedicated Hosts - physical EC2 server dedicated for your use.

