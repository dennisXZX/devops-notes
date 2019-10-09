### EC2 (Elastic Compute Cloud)

#### Fundamentals

EC2 is a web service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change. An EC2 instance is just a virtual machine.

- EC2 instance uses EBS (Elastic Block Store) volume to store operating system and data. EBS volume is separate from its associated EC2 instance, so it can be transferred between different EC2 instances, or continue to exist after the EC2 instance is terminated.

- Termination protection is turned off by default, you must turn it on

- On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated, however, additional volumes would be persisted.

- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data. EBS-backed instance can be stopped. You will not lose the data on this instance if it is stopped.

- EBS volumes are replicated by default within an Availability Zone (AZ)

- You can create an image (AMI) from an running EC2 instance.

#### Copy files from local machine to an EC2 instance

Use `scp` to do the trick as follows:

`scp -r -i <pem_file> <local_code> ec2-user@<ec2_ip>:/home/ec2-user/project-name`

#### Bootstrap Script

You can add bootstrap script to an EC2 instance.

```bash
#!/bin/bash

# update all packages
yum update -y

# install Apache
yum install httpd -y

# start the Apache service
service httpd start

# make sure the httpd service runs after an EC2 instance reboot
chkconfig httpd on

# create a simple web page
cd /var/www/html
echo "<html><h1>hello world</h1></html>" > index.html

# create an S3 bucket
aws s3 mb s3://bucketName

# back up the created webpage to S3 bucket
aws s3 cp index.html s3://bucketName
```

#### User data & Meta-data

You can retrieve EC2 instance meta-data and user data by using `curl`

```bash
# retrieve EC2 meta data
curl http://169.254.169.254/latest/meta-data

# retrieve EC2 user data
curl http://169.254.169.254/latest/user-data
```

#### Security group

- all inbound traffic is blocked by default

- all outbound traffic is allowed

- changes to Security Groups take effect immediately

- you can have any number of EC2 instances within a secruity group

- you can have multiple security groups attached to an EC2 instance

- if you create an inbound rule allowing traffic in, that traffic is automatically allowed back out again

- you cannot block specific IP addresses using Security Group, instead use Network Access Control Lists

- you can specify allow rules, but not deny rules

#### Migrating EBS

- To move an EC2 volume from one AZ to another, take a snapshot of it, create an AMI from the snapshot and then use the AMI to launch the EC2 instance in a new AZ.

- To move an EC2 volume from one region to another, take a snapshot of it, create an AMI from the snapshot and then copy the AMI from one region to another. Then use the copied AMI to launch a new EC2 instance in a new region.

#### Placement groups

- Clustered placement group - a group of instances within a single Availability Zone. Placing instances as close as possible to enjoy low network latency and high network throughput.

- Spread placement group - a group of instances that are each placed on distinct underlying hardware. Mainly for individual critical EC2 instances.

- Partitioned placement group - a couple of instances are grouped together to form a partition, and each partition has its own network and power source.

#### Pricing types

On Demand - allows you to pay a fixed rate by the hour (or by the second) with no commitment

Reserved - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 year or 3 year terms.

Spot - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. If the spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran.

Dedicated Hosts - physical EC2 server dedicated for your use.
