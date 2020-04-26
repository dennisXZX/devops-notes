### EC2 (Elastic Compute Cloud)

#### Fundamentals

EC2 is a web service that provides resizable compute capacity in the cloud. EC2 reduces the time required to obtain and boot new server instances to minutes, allowing you to quickly scale capacity, both up and down, as your computing requirements change. An EC2 instance is just a virtual machine.

- Termination protection is turned off by default, you must turn it on

- Instance store volumes cannot be stopped. If the underlying host fails, you will lose your data. EBS-backed instance can be stopped. You will not lose the data on this instance if it is stopped.

- EBS volumes are replicated by default within an Availability Zone (AZ)

- You can create an image (AMI) from a running EC2 instance.

- By default, an EC2 machine comes with a private IP for internal AWS network and a public IP for public access. When you SSH into the EC2 machine, you can't use a private IP because you are not in the same network of your EC2 instance. If THe EC2 instance is stopped and then re-started, the public IP can change unless you attach an elastic IP to it.

- Burstable instances can be amazing to handle unexpected traffic. If your instance consistently runs low on CPU credit balance, you need to move to a different kind of non-burstable instance.

#### Load balancer

Advantages of using a load balancer:

- Spread load across multiple downstream instances

- Expose a single point of access (DNS) to your application

- Seamlessly handle failures of downstream instances

- Do regular health checks to your instances

- Provide SSL termination for your websites. This will free your backend servers from the compute-intensive work of encrypting and decrypting all of your traffic

- Enforce stickiness with cookies

- High availability across zones

- Separate public traffic from private traffic. The load balancer does a connection termination and would start a new connection with the EC2 instance. So the EC2 instance would see a private IP from the load balancer.

__Application Load Balancer__

Application load balancer can handle multiple apps at the same time. For example, a user visiting `yourDomain/user` can be routed to a target group for User application (You will need to place EC2 instances into a target group), while another user visiting `yourDomain/search` would be routed to a target group for Search application. 

If the traffic is coming through a load balancer, EC2 instances will only see the traffic is coming from the private IP of the load balaner. However, you can see the user's public IP address from the `X-Forwarded-For` header.

#### Auto Scaling Group

The goal of an auto scaling group is to:

- Scale out to match an increased load
- Scale in to match a decresed load
- Ensure we have a minimum and a maximum number of machines running
- Automatically register new instances to a load balancer

It is possible to scale an ASG based on CloudWatch alarms. An alarm monitors a metric, based on the alarm we can create scale-out and scale-in policies. Scaling policies can be on CPU, network, custom metrics or based on a schedule.

IAM roles attached to an ASG will get assigned to ECS instances within the ASG.

#### EBS Volume

EBS is a network drive, not a physical drive. It uses the network to communicate with the instance, which means there might be a bit of latency.

EC2 instance uses EBS (Elastic Block Store) volume to store operating system and data. EBS volume is separate from its associated EC2 instance, so it can be detached and attached between different EC2 instances, or continue to exist after the EC2 instance is terminated.

On an EBS-backed instance, the default action is for the root EBS volume to be deleted when the instance is terminated, however, additional volumes would be persisted.

__Encryption__

When you create an encrypted EBS volume, you get the following:

- Data at rest is encrypted inside the volume
- All the data in transit moving between the EC2 instance and the volume is encrypted
- All snapshots are encrypted
- All volumes created from the snapshot are encrypted

#### SSH into an EC2 instance

- Get the public IP of your EC2 instance

- Make sure the security group attached to the EC2 instance allows SSH on port 22

- Update the permission for your private key by `chmod 0400 <pem_file>`

- `ssh -i <pem_file> ec2-user@YOUR_EC2_INSTANCE_PUBLIC_IP`

#### Copy files from local machine to an EC2 instance

Use `scp` (securely copy files) to do the trick as follows:

`scp -r -i <pem_file> <local_code> ec2-user@<ec2_ip>:/home/ec2-user/project-name`

#### Install Apache on an EC2 instance

- SSH into the EC2 instance
- `sudo su` to switch to root user
- run `yum update -y` to update the packages in the machine
- `yum install -y httpd.x86_64` to install Apache
- `systemctl start httpd.service` to start Apache service
- `systemctl enable httpd.service` to ensure Apache service enabled after machine reboot
- `echo "hello world from $(hostname -f)" > /var/www/html/index.html` to generate a web page
- `curl localhost:80` to test whether Apache service is running properly
- Set up security group which allows HTTP traffic for Apache, and attach it to the EC2 instance
- Open your browser and use the public IP of your EC2 instance to access the website

#### Bootstrap Script

You can add bootstrap script to an EC2 instance. EC2 User Data is automatically run with the `sudo` command.

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

You can retrieve EC2 instance meta-data (info about the EC2 instance) and user data (launch script of the EC2 instance) by using `curl`

```bash
# retrieve EC2 meta data
curl http://169.254.169.254/latest/meta-data

# retrieve EC2 user data
curl http://169.254.169.254/latest/user-data
```

#### Security group (Firewall for EC2 instance)

- all inbound traffic is blocked by default

- all outbound traffic is allowed

- changes to Security Groups take effect immediately

- you can have any number of EC2 instances within a security group

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

#### EC2 instance launch types

On Demand instances - allows you to pay a fixed rate by the hour (or by the second) with no commitment. Best for short workload, predictable pricing.

Reserved - provides you with a capacity reservation, and offer a significant discount on the hourly charge for an instance. Contract terms are 1 year or 3 year terms. Best for long workload (>= 1 year)

Convertible reserved instances - long workload with flexible instances. You can convert the EC2 instances between different types. (like from t2 to c5)

Scheduled reserved instances - launch within time window you reserve

Spot - enables you to bid whatever price you want for instance capacity, providing for even greater savings if your applications have flexible start and end times. If the spot instance is terminated by Amazon EC2, you will not be charged for a partial hour of usage. However, if you terminate the instance yourself, you will be charged for any hour in which the instance ran. Best for batch jobs, big data analysis or workload that are resilient to failures.

Dedicated instances - no other customers will share your hardware. No control over instance placement, which means the instance would move hardware after a stop / start.

Dedicated Hosts - control an entire physical server and can control instance placement. Best for software that have complicated licensing model (BYOL - Bring Your Own License), or for companies that have strong regulartory or compliance needs.

#### Custom AMI

Using a custom built AMI can provide the follow advantages:

- Pre-installed packages needed

- Installing your app ahead of time (for faster deploys when auto-scaling)

- Faster boot time (no need for long EC2 user data at boot time)

- Machine comes configured with monitoring / enterprise software

- Control of maintenance and updates of AMIs over time

AMI are built for a specific AWS region.
