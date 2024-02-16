# Objective
The objective of setting this AWS auto-scaling lab is to ensure that your application can handle network traffic by automatically adjusting the number of EC2 instances that are running. AWS AutoScaling allows scale resources up or down through a pre-defined threshold, which helps you only pay for the resources you actually need.
Prerequisites for this lab
-An AWS account.
-You need to have basic knowledge of AWS services like EC2 instances, VPC, and Security groups.

Steps by step guide for setup AWS Auto Scaling

Login to your AWS Console and navigate to the EC2 service.
Click on the “Auto Scaling Groups” option from the left-hand menu.
Click on the “Create Auto Scaling Group” button to start the auto-scaling group creation process.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/2ee7bd60-9c68-4307-8859-df0e27b261f9)

Give an auto scaling group name and click on the “Create a launch template”.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d5ae0223-2f73-429f-b8b9-27de5f3b26cd)

Give a name and description for launch template.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/18cbae97-f2fc-4ddc-846f-cdc27a30e9e9)

Configure AMI for your application (Webserver).

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/cbc41df3-abb1-4f74-9613-64c01412238d)

Configure instance type asper your need.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/083670f6-8c07-4c67-8143-9b65dd42d234)

Configure Key pair, Security group and Network settings.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/fb5f66bf-c464-4300-b7f1-e780ad3bea98)

Configure EBS storage volumes and click on the “Create launch template”.

A launch template will be created.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/39e36835-f743-4e85-8fff-1eed5e646772)

Now, Go back to the screen “Create Auto scaling group”. Click on the refresh icon to get created launch configuration and select that launch template. After configuration click on the “Next”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/084177a2-8732-487b-9faf-52105c691931)

Choose the Network and subnet(s) configuration where you want to launch the EC2 instances.
You can select multiple subnets to ensure high availability. After configuration click on the “Next”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e5513db5-6e3c-4b75-9588-f6d2e0afd7b6)

Optional step: Create or attach a Load balancer or target group to distribute traffic across instances.
Additionally, you can define the health check type and the grace period (for example 60 second) for EC2 instances to initialize before being marked as healthy or unhealthy. After configuration click on the “Next”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/8c98a9fa-81cc-41c2-b94a-45330793e143)

Setup the minimum, maximum, and desired number of EC2 instances that should be running at any time.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/52c21b75-d832-44b0-84b9-6faf84a4ec74)

You can define scaling policies if required. Target tracking scaling adjusts the number of instances based on a predefined metric, while step scaling adds or removes instances based on thresholds that you define.
For example, Here for metric type “Average CPU utilization” the target value is 50 defined. After configuration click on the “Next”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/de56a065-0fd7-40b1-9d8a-a519acc7386f)

Optional step: Add notification, Add Tags (skipping for this lab). Click on the “Next”
Review your all configuration and click on the “Create Auto Scaling group” button
After you have created your auto-scaling group, AWS will automatically launch desired EC2 instances based on your defined scaling policies. You need to wait for some time and refresh your EC2 instance dashboard.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/51156231-e47f-45fc-b1aa-d0bf340f9e30)

To validate the AutoScaling configuration, let’s terminate one instance after sometime (using health check configuration), AutoScaling will automatically create a new instance to meet your configured desired capacity of instances.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/a15f6837-a5dc-47e8-96e9-50f27b30bf50)

Note: Make sure to delete all the AWS resources created for this lab to avoid unnecessary charges.
