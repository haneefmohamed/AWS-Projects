# Launching a static website through ec2
 we’ll be launching our EC2 instance which is, well, a virtual server and we’ll use the console for this then we will launch a web server directly on the EC2 instance using a piece of code as user data script and we will pass to the EC2 instance. Finally, we’ll learn how to start, stop, and terminate our instance.

Steps:

Step 1. Go to the AWS Management Console (https://aws.amazon.com/console/). On services, tab search for EC2 and click on instances in the sidebar for creating an EC2 Instance.

Step 2. First, enter a name tag for the instance. This will act as key-value pair and if you wanted to add additional tags to tag your instance differently, then you could click on “Add additional tags”.

Step 3. Next, you need to choose a base image for your EC2 instance i.e. operating system of your instance. You can see a full catalog of OS that you can search but in this article, we’re going to use Amazon Linux, which is provided by AWS.

![EC2](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/51e1f3ce-b6a0-49b3-abc5-2c16133148ab)

Step 4. Next, we need to choose an instance type. Instance types are going to differ based on the number of CPUs they have, the amount of memory they have, and how much they cost. In this article, we are going to have a T2 micro selected. This one is free tier eligible, so it will be free to launch them. If you wanted to compare the instance types click on “Compare Instance types” it shows you all the types of instances as well as how much memory they have and so on.
![Instancetypes](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/66ffc843-b6cf-4c66-923c-ffd13caffcd5)

Step 5. Next, create a key pair to log into your instance. So this is necessary if we use the SSH utility to access our instance. We could proceed without a key pair, but for now, let’s go ahead and create a new key pair.

Give a name to Key Pair.
Then you need to choose a key pair type (RSA encrypted or ED25519 encrypted), here we’ll be using the RSA encrypted.
And then we have to select key pair formats. If you have Mac or Linux or Windows 10 then you can use the .pem format.
If you have Windows less than version 10, for example, Windows 7 or Windows 8, then you can use a .ppk format.
When you create a key pair it will be downloaded automatically to your pc.

![keypair](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e9853a93-f572-4545-9865-8a361506a251)

 
Step 6. Next, we have to go into network settings. Leave the settings to default Our instances are going to get a public IP and then there is going to be a security group attached to our instance (which is going to control the traffic from and to our instance ) and therefore we can add rules. The first security group created will be called launch-wizard-1 which is created by the console directly and we can define multiple rules here. So the first rule we want to have is to allow SSH traffic from anywhere and to allow HTTP traffic from the internet.

Step 7. Next, we need to configure the storage for this instance let’s have an eight-gigabyte gp2 root volume because, in the free tier, we can get up to 30 gigabytes of EBS General Purpose SSD storage. If you go into advanced details you could configure them a little more advanced in terms of storage, volume, encryption, and keys. One important thing to note here is the “delete on termination’ should be “Yes”. By default, it is enabled to yes, which means that once we terminate our EC2 instance, then this volume is also going to be deleted.


![Networkandstoragesettings](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/f34e7629-d352-47ca-b24c-cb9e19028314)


User Data Script:
User data is when we pass a script with some commands to our EC2 instance. It will execute the script on the first launch of our EC2 instance and only on the first launch. And therefore, on the first launch, we shall be able to pass the commands here. In this article, we are going to pass below code

#!/bin/bash
# Use this for your user data (script from top to bottom)
# install httpd (Linux 2 version)
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Hello World from $(hostname -f)</h1>" > /var/www/html/index.html
The above code is a shell script. This script is going to update packages, then install the HTPD web server on the machine, and then write a file using httpd, an HTML file that will be a web server.
![Userdatascript](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/198b5c79-2e8a-4869-8f52-e964ab488c8d)

 

Step 8. Finally, we can review everything we have created and launch this instance. Let’s go to view all instances and refresh the page it’s gonna take about 10, 15 seconds for the instance to come up and this is the whole power of the Cloud we are able to create an instance or 100 of them very quickly in less than 10 seconds without us owning any single server.

Step 9. Once the instance name is created we can observe a few things 

There’s an instance ID which is just a unique identifier for our instance.
There is a public IPv4 address, this is what we’re going to use to access our EC2 instance,
There is a private IPv4 address which is how to access that instance internally on the AWS network, which is private.
The current state of the instance. The instance state is running,
We also get some information about hostname, private DNS, Instance type, AMI details, and Key pair.

![EC2InstanceConfigurations2](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/43055263-3432-4622-ad6f-748b5c26334d)

 

If we go to security. we get some information on the security group which was created called launch-wizard-1. Port 22 is accessible from everywhere and port 80 is accessible from everywhere.

Step 10. Launching webpage created via User Data Script.

Let’s check the web server running on our instance. And for this, you go to a public IPv4 address, you copy this or you click on the open address and probably it doesn’t work. If you click on it, copy, and then paste it, you press enter, it’s going to work. So it depends on the web browsers you have and so on, okay, but the reason sometimes it doesn’t work is that in the URL, you need to make sure that you’re using the HTTP protocol. If you use HTTPS, this is not going to work and it’s going to give you an infinite loading screen.

And in programming, when you do something for the first time, you usually say hello world. So our web server is saying hello world from an IP address here, which is not the public IP. It actually corresponds to the private IPv4 address. We used the public IP address to access it, but we have the private IP address showing up on the website.

![webpage](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/678ebec5-1d4a-42f2-a002-c5150c01701d)


Step 11. We can see our EC2 instance is running but if we don’t need it, we can go to the instance state and then click on stop instance. And in the Cloud, you can start and stop instances just as you wish. The longer you leave it running, the more you’re going to pay. But if you decide to stop an instance, then AWS will not bill you for it. While the instance is in a stopping state and if we try to refresh our webpage it’s not going to work because you don’t have the server running anymore.

If you stop an instance and then start it later on and if we go to the browser and try again we can’t able to see our webpage. Even though the server is running we can’t able to see the message.  It’s because If you stop an instance and then you start it, later on, AWS changes its public IPv4 address. So, therefore, you need to copy the new IPv4 and make sure to use HTTP to have access back to our EC2 instance. If you finally want to get rid of this instance we can do an instance state and then terminate the instance.

![Instance](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/125ea46f-fb43-4daf-b5b1-544eec3ee96a)




