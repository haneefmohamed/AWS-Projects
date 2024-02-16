# Hosting a website on AWS lightsail

Step 1:
Create a Lightsail Instance
Once you sign up with Amazon Lightsail, you can create your first Lightsail Instance.

Click on ‘Create Instance’ to run your first VPS server.


![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/409b0632-5742-43da-9373-9052cd51110e)

You will be prompted to select an Operating System platform. Linux works well for web servers unless you specifically want to use Microsoft technologies such as asp.net.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/4709c168-4968-44f0-b75d-baf89cc96627)

On the ‘select a blueprint’, you can choose an operating system only or an OS bundled with packages such as WordPress. An OS only blueprint is more flexible because it allows you to customize package installation.

Then, choose Ubuntu 16.04 as the operating system because it is easy to use and you can find many articles about it on the web.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d495eecb-65f1-4dab-acf6-3dcae690222e)

Towards the bottom of the screen, choose a plan for your instance, the $5 will work well when starting out.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/6c4134cc-c930-47eb-b416-ccabbb78f153)
Finally, name your instance and click ‘Create’ at the bottom of the screen


![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/2a991223-5014-4dc0-b04a-53e572e20dc5)

Your instance will be created automatically. Don’t worry if you see a pending status. The creation process will take a few minutes.

Step 2:
Installing a web server on Amazon Lightsail Instance
Once your instance is created and you are sure it is running, click it to get more details about it. You will see a public IP address and a username that you can use to connect to your instance via SSH.

Up to this point, you only have an operating system on your instance. We need to install the Apache web server to server website content.

So, on the instance details page, click on ‘Connect using SSH’

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/bf06167a-9866-4221-b1d7-addf8d901256)

Then, enter the following on the command line interface:

$ sudo apt-get update
$ sudo apt-get install apache2
Press Y and hit Enter when prompted to confirm the installation

Apache web server will be successfully installed on your instance.

If you enter your instance’s public IP address on your server, you should now see the default Apache Web page:
$ http://ip_adrress

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/48c50f3d-462a-4c07-98d3-91e2e902d2e3)

Step 3:
Point your domain to AWS Lightsail
Although it is okay to visit your website via an IP address, your visitors will need to use a domain name instead.  Luckily, you can create DNS records on Amazon Lightsail that point backs to your instance public IP address

Then, you need to enter the DNS records on your domain name depending on where you purchased it.  The DNS servers may look like this:

ns-806.awsdns-36.net

ns-494.awsdns-61.com

That's all !!





