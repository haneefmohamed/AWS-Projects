# Hosting wordpress on AWS

1.Create an Instance

After registration you have many options available and then you probably have this question in your mind that Which type of instance should I choose?

If you have new blog then you can choose EC2 micro instance which can handle around 200+ real-time traffic.

It has also attractive price structure but if you are migrating your existing blog and having traffic more than thousand per day then you must choose Small instance which can handle that traffic very easily.

To create a new instance, access the AWS Management Console and click the EC2 tab:
Choose an AMI in the classic instance wizard:
I chose the Basic 64-bit Ubuntu Server Amazon Linux AMI.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d8f6a7ff-17f4-48bc-a520-ca5dfa2e057b)

Instance details:
Select the Instance Type you want to use. I chose Small (m5a.small).

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/0256476e-c4c1-4056-926d-693a663b8ace)

Create a new key pair.
Enter a name for your key pair (i.e. crunchify) and download your key pair (i.e. crunchify.pem).
Select the quick start security group.
Launch your instance.

2.SSH into your Instance
Once your instance setup is complete and it shows instance is running, you can ssh into it.

First of all, you need to identify the IP Address (public DNS) of your instance:
Select the instance in the AWS Management Console.
Look for the Public DNS in the instance description (bottom part of the screen).
Use that address (and a path to your .pem file) to ssh into your instance:

//ssh ec2-user@ec2-50-17-15-27.compute-1.amazonaws.com -i ~/crunchify.pem//

If you are on windows system then you should use Putty for connect as SSH. You can connect with putty by following this article.

If you get an error message about your .pem file permissions being too open, chmod your .pem file as follows:

[ec2-user ~]$ chmod 600 ~/crunchify.pem
In this tutorial you need to perform many shell commands and most of command require root access. So, to avoid this we will prefix these all command with sudo by switching user once for all by this command.

[ec2-user ~]$ sudo su

3. Install the Apache Web Server to run PHP
To install the Apache Web Server, type in terminal:

[ec2-user ~]$ sudo yum -y install python-simplejson     # Install PHP latest version
[ec2-user ~]$ sudo yum update                           # System wide upgrade
[ec2-user ~]$ sudo yum install -y default-jre           # Install Java (just to be safe)
[ec2-user ~]$ sudo yum install httpd                    # Install HTTPD server
Start the Apache Web Server:

[ec2-user ~]$ service httpd start
After setup, to test your Web Server, open a browser and access your web site:

http://ec2-50-17-15-27.compute-1.amazonaws.com
(Use your actual public DNS name). You should see a standard Amazon place holder default page.

4. Install PHP to run WordPress
To install PHP, type in terminal:

[ec2-user ~]$ yum install php php-mysql
After installing php successfully Restart the Apache Web Server:

[ec2-user ~]$ service httpd restart
Create a page to test your PHP installation:

[ec2-user ~]$ cd /var/www/html
[ec2-user ~]$ vi test.php
Type i to start the insert mode
Type <?php phpinfo() ?>
Type :wq to write the file and quit vi
Open a browser and access test.php to test your PHP installation:

http://ec2-50-17-15-27.compute-1.amazonaws.com/test.php
(Use your public DNS name)

5. Install MySQL for adding database
To install MySQL, type:

[ec2-user ~]$ yum install mysql-server
Start MySQL:

[ec2-user ~]$ service mysqld start
Create your “blog” database:

[ec2-user ~]$ mysqladmin -u root create blog
Secure your database:

[ec2-user ~]$ mysql_secure_installation

Answer the wizard questions as follows:
Enter current password for root: Press return for none
Change Root Password: Y
New Password: Enter your new password
Remove anonymous user: Y
Disallow root login remotely: Y
Remove test database and access to it: Y
Reload privilege tables now: Y

6. Install WordPress
To install WordPress, type:

[ec2-user ~]$ cd /var/www/html
[ec2-user ~]$ wget http://wordpress.org/latest.tar.gz
To uncompress tar.gz file type:

[ec2-user ~]$ tar -xzvf latest.tar.gzcd
This will uncompress WordPress in its own WordPress directory.

I like having WordPress in a separate directory, but would rather rename it to “blog” if you want to install it to subdomain like “http://your-site.com/blog”:

[ec2-user ~]$ mv wordpress blog
otherwise move all files to parent folder by typing:

[ec2-user ~]$ mv *.* ..
Create the WordPress wp-config.php file:

[ec2-user ~]$ cd blog
[ec2-user ~]$ mv wp-config-sample.php wp-config.php
[ec2-user ~]$ vi wp-config.php
Type i to start insert mode.
Modify the database connection parameters as follows:

define(‘DB_NAME’, ‘blog’);
define(‘DB_USER’, ‘root’);
define(‘DB_PASSWORD’, ‘YOUR_PASSWORD’);
define(‘DB_HOST’, ‘localhost’);
Press esc one time then
Type :wq to write the file and quit vi
Open a Browser and access your blog:

http://ec2-50-17-15-27.compute-1.amazonaws.com/blog (Use your public DNS name).
This should open the WordPress installation configuration process.

TIP: To allow WordPress to use permalinks
WordPress permalinks need to use Apache .htaccess files to work properly, but this is not enabled by default on Amazon Linux. Use this procedure to allow all overrides in the Apache document root.

Open the httpd.conf file with your favorite text editor (such as nano or vim). If you do not have a favorite text editor, nano is much easier for beginners to use.

[ec2-user wordpress]$ sudo vim /etc/httpd/conf/httpd.conf
Find the section that starts with <Directory “/var/www/html“>.

<Directory "/var/www/html">
#
#Possible values for the Options directive are "None", "All",
#or any combination of:
#Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
#
#Note that "MultiViews" must be named *explicitly* --- "Options All"
#doesn't give it to you.
#
#The Options directive is both complicated and important.  Please see
#http://httpd.apache.org/docs/2.4/mod/core.html#options
#for more information.
#
Options Indexes FollowSymLinks
#
#AllowOverride controls what directives may be placed in .htaccess files.
#It can be "All", "None", or any combination of the keywords:
#Options FileInfo AuthConfig Limit
#
AllowOverride None
#
#Controls who can get stuff from this server.
#
Require all granted
</Directory>
Change the AllowOverride None line in the above section to read AllowOverride All.

Note:
There are multiple AllowOverride lines in this file; be sure you change the line in the <Directory "/var/www/html"> section.

AllowOverride All
Save the file and exit your text editor.

7. Map IP Address and Domain Name
To use your blog in production, you will have to:

Associate an IP address to your instance
Map your domain name to that IP address

That’s it.

You have successfully created LAMP environment and installed WordPress on Amazon EC2. 
