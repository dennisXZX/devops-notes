### EFS (Elastic File System)

#### Hook up an EFS to multiple EC2 instances

Add these boot-up scripts to EC2 instances.

```bash
#!/bin/bash

yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
yum install amazon-efs-utils -y 
```

Once the EC2 instances are up and running, SSH into each instance and navigate to `/var/www`, then mount the EFS (fs-9816b269) to each EC2 instance by `mount -t efs -o tls fs-9816b269:/ /var/www/html`. Now all your EC2 instances are sharing the `/var/www/html` directory, which means any change you make in that directory would reflect across all EC2 instances.
