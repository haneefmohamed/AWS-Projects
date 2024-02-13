# Setting up an Application Load Balancer with AWS EC2

What is Load Balancing?
Load balancing is the distribution of workloads across multiple servers to ensure consistent and optimal resource utilization. It is an essential aspect of any large-scale and scalable computing system, as it helps you to improve the reliability and performance of your applications.

Elastic Load Balancing:
Elastic Load Balancing (ELB) is a service provided by Amazon Web Services (AWS) that automatically distributes incoming traffic across multiple EC2 instances. ELB provides three types of load balancers:

Application Load Balancer (ALB) — operates at layer 7 of the OSI model and is ideal for applications that require advanced routing and microservices.
Network Load Balancer (NLB) — operates at layer 4 of the OSI model and is ideal for applications that require high throughput and low latency.
Classic Load Balancer (CLB) — operates at layer 4 of the OSI model and is ideal for applications that require basic load balancing features.

Steps:
1:
launch 2 EC2 instances with an Ubuntu AMI and use User Data to install the Apache Web Server.

Log in to your AWS Console and go to the EC2 dashboard.

Click on the “Launch Instance” button and select “Ubuntu Server “.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/b13d27da-9b96-496c-9e43-a45808b6b0a6)
Choose the instance type, configure the instance details, add storage, and configure security groups as required.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/6f5c22a5-c332-4618-b73a-8b8cd5423b49)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/09ee5bbd-e4f1-4732-bb24-a4d18471a511)

In the “Configure Instance Details” page, scroll down to the “Advanced Details” section and expand the “User data” field.

In the “User data” field, enter the following commands to install and start the Apache web server:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/69756c6b-c258-4279-ae39-3dcb12f7d19f)

You can see two instances are created.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/0f7721b2-dc51-493f-bb6d-0f7f11edc2ef)

Modify the index.html file to include your name so that when your Apache server is hosted, it will display your name also do it for 2nd instance.

For apache-server1

Check apache2 status using below command:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/c3956fde-0b18-4dec-8280-72f20ec079fe)

Go inside /var/www/html path and edit index.html file

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/7539a553-997c-4fae-aff6-a25fc99d5d2b)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/bfedff62-edcc-49e4-82fd-ca2070a0b09d)

Copy the public IP address of your EC2 instances.

Open a web browser and paste the public IP address into the address bar.

You should see a webpage displaying information about your PHP installation.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/5620be68-ec62-4242-89ab-ac029d5b887b)

For apache-server2:

Check apache2 status.

Go inside /var/www/html path and edit index.html file

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/8d06df71-7f01-4fe8-a90f-01bb409b59f2)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/65ce832e-7bd0-47ef-955e-228fe23eb636)

Copy the public IP address of your EC2 instances.

Open a web browser and paste the public IP address into the address bar.

You should see a webpage displaying information about your PHP installation.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e8118d04-e155-4c13-acba-158017a3efdd)

2:
Create an Application Load Balancer (ALB) in EC2 using the AWS Management Console.

Log in to the AWS Management Console and go to the EC2 dashboard.

Click on “Load Balancers” in the left-hand navigation menu and then click the “Create Load Balancer” button.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/32b1d232-4ec6-4e89-89ec-ffa99145fec3)

Select “Application Load Balancer” as the load balancer type and click “Create”.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/0662064e-c1a6-4cf4-9272-b567525eb6df)

Configure the load balancer settings, such as name, listener, security group, and availability zones. For the listener, you can choose HTTP or HTTPS, depending on your application’s requirements.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/94a411a3-80f2-4a8b-8614-f56ea5100efe)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/770ec808-b149-480f-b824-8305e811cc43)

Configure “Security Groups”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e88e1c31-1975-4d81-bf03-85672b540cee)

Create a target group by specifying a name, protocol, port, and health check settings. Choose the same availability zones as the load balancer and select the instances that you launched in step 1 as targets for the target group.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/484aae0b-44f3-41d9-8bbd-b5a752c7ba87)

Add EC2 instances which you launch in step-1 to the ALB as target groups.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/746c79e1-4dea-4cd8-9c0f-3aee9bf1b35a)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/aa7f7674-9d67-47a8-b08d-66e7cf497e4b)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/7a50e61e-af35-473b-89f2-5ffa499efcf1)

Load balancer is created.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/29bd9547-d5f9-43e6-9460-2d0b6dd59018)

Target group is created.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/21b30e2e-0c1c-4dd6-a712-2a5a4ed71a49)

Verify that the ALB is working properly by checking the health status of the target instances and testing the load balancing capabilities.

Verify that the instances are registered with the load balancer by checking the target group’s health status. You should see a healthy status for all instances in the group.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/16655f43-1964-4888-8904-e2e29cd4efcb)

Test the load balancing capabilities by accessing the load balancer’s DNS name in a web browser . You should see traffic being evenly distributed across the instances.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/0109acab-ae49-48f8-bd3d-5c140e074d72)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/5732c2f1-5b32-4d83-891d-bddfd8b3b034)

THANKYOU!!!
