# Launching a static website through ec2

0) Login to the EC2 Amazon Console
https://console.aws.amazon.com/console/home

1) In the EC2's Security group section add an inbound rule to open ports 80 and 443
Type: HTTP, Protocol: TCP, Port: 80, Source: 0.0.0.0/0
Type: HTTPS, Protocol: TCP, Port: 443, Source: 0.0.0.0/0

2) Copy the Public DNS for your EC2 instance
ec2-##-##-##-##.us-west-2.compute.amazonaws.com

3) On the Github Repo page, open ⚙Settings and paste the Public DNS into the Custom domain field
Custom domain = ec2-##-##-##-##.us-west-2.compute.amazonaws.com

4) SSH into your EC2 instance and install nginx
$ sudo yum install nginx

5) Start the nginx web server
$ sudo /etc/init.d/nginx start

6) View the test site by browsing to your Repo's website
user.github.io/repository

7) Copy your web files to the nginx html folder on the EC2 instance
$ sudo cp -a _site/*html ../../../../usr/share/nginx/html/


NOTE: To restart server after reboot
$ sudo /etc/init.d/nginx restart
