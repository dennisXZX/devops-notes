## AWS Database

### RDS (Relational Database Service)

- There are two different types of backups for RDS, namely, `automated backups` and `database snapshots`.

- You can use `read replicas` to increase performance. A `read replica` can be promoted to primary database.

- `multiple availability zone` can be enabled for disaster recovery.

#### Wire up a WordPress app with MySQL database

Launch an EC2 instance with the following boostrap scripts:

```bash
#!/bin/bash

yum install httpd php php-mysql -y
cd /var/www/html
wget https://wordpress.org/latest.tar.gz    # download the Wordpress zip file
tar -xzvf latest.tar.gz                     # extract an archive
cp -r wordpress/* /var/www/html/
rm -rf wordpress
rm -rf latest.tar.gz
chmod -R 755 wp-content                     # change wp-content directory permissions 
chown -R apache:apache wp-content           # change wp-content directory to own by apache user and apache group
chkconfig httpd on                          # make sure Apache service is on after instance reboot
service httpd start                         # start Apache service
```

Now you can go to the EC2 instance IP address to config the WordPress app. You need to use the RDS instance endpoint as `Database Host` in the WordPress config. Then you need to use AWS CLI to edit the `wp-config.php` in `/var/www/html` directory.

You have got a WordPress app up and running at this point.

#### Aurora

- A MySQL-compatible relational database engine.

- You can convert a MySQL database to an Aurora one by first creating Aurora read replica from the MySQL database, then promote the read replica. After the promotion, the MySQL database will be successfully migrated to Aurora database.

#### DynamoDB (NoSQL)

#### Redshift (Data Warehouse)

#### ElasticCache

- ElasticCache is used to increase database and web app performance. There are two open-source in-memory caching engines, namely, Memcached and Redis.
