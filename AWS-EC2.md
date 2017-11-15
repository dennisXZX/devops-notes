## EC2 (Elastic Compute Cloud)

##### Deploy a Laravel app to EC2

- Create a new EC2 instance and choose an Amazon Machine Image
- Generate a key pair (public and private keys) which allows you to connect to your instance securely

You should store your ssh keys in `/Users/$USERNAME/.ssh/` and set the directory permissions to `700` (drwx------).

- Launch your instance
- Change the permissions of your private key `key.pem` to 600 and move it to a safe place.

```
chmod 600 key.pem
mv key.pem /Users/$USERNAME/.ssh/
```

- Connect to your instance

```
ssh -i key.pem ec2-user@Your_IPv4_Public_IP
```

- Install necessary softwares for web server

```
sudo yum install -y httpd24 php71-* mysql-server mysql
```

- Add a security rule to allow inbound HTTP (port 80) connections to your instance

- Start your Apache server by using `sudo service httpd start`

Now you should see a homepage if you visit your public IP

- Start your MySQL service by running `sudo service mysqld start`

- Secure our MySQL by running `sudo mysql_secure_installation`

- Install Git by running `sudo yum install git`

- Clone your Laravel repo into `/var/www/html`

- Add `ec2-user` to apache group

```
sudo usermod -a -G apache ec2-user
```

- Change the ownership of your Laravel project to apache user and group

```
sudo chown -fR apache:apache project_folder
```

- Change the document root setting in Apache httpconf file by running `sudo vi /etc/httpd/conf/httpd.conf`

```
// change DocumentRoot to the public folder of your Laravel project
DocumentRoot "/var/www/html/laravel-lms-api/public"

// enable cross-origin resource sharing on apache
<Directory "/var/www/">
 AllowOverride None
 # Allow open access:
 Require all granted
 Header set Access-Control-Allow-Origin "*"
</Directory>

// change AllowOverride to All
#
# AllowOverride controls what directives may be placed in .htaccess files.
# It can be "All", "None", or any combination of the keywords:
# Options FileInfo AuthConfig Limit
#
AllowOverride All

// restart your Apache server
sudo service httpd restart
```

- Install Composer

```
// run these following commands to download and install Composer
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"

// set Composer to be accessed globally
sudo mv composer.phar /usr/local/bin/composer
```

- Install project dependencies by running `composer install`

- Create a `.env` config file for the Laravel project

```
sudo cp .env.example .env
```

- Update the MySQL database, username and password in `.env` file

- Log in MySQL to create a database

```
// log in MySQL
mysql -u username -p

// create a database
CREATE DATABASE databaseName;
```

- Migrate the database by running `php artisan migrate`

Now your Laravel app should be up and running! Hooray!

 
