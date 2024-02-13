# Building an AWS bastion host
 The basic steps for creating a bastion host for your AWS infrastructure:

Launch an EC2 instance as you normally would for any other instance.
Apply OS hardening as required.
Set up the appropriate security groups (SG).
Implement to connect local Using SSH-agent forwarding or Remote Desktop Gateway.
Deploy an AWS for each of the Availability Zones you’re using.
Create Ec2 Instance
Create 2 Ec2 instances(Public and Private) using custom VPC, Route table, internet gateway and subnet (Public or Private subnet). And connect to the local using the SSH client.

First Create a custom VPC with public & private subnet, Route table and Internet gateway

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/562ae64e-9e41-48c8-b6cd-4a364c9baf88)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/86d7095c-ad05-48b0-8f88-a80af7206430)

Create 2 ec2 instances Public and Private. In a public instance use custom VPC with Public subnet and enable Auto-assign Public IP. Private Instance using custom VPC with Private subnet and Disable Auto-assign Public IP.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/6223b65b-c711-40da-858d-6d0a29009be7)

connect to the Public network using the SSH Client.

chmod 400 ec2.pem
ssh -i "ec2.pem" ubuntu@ec2-3-216-23-4.compute-1.amazonaws.com

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/55b303d6-1f52-4985-b77d-cff5d298f866)

Connect to the local Using ssh

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/9e1f4d12-0adf-435d-97dc-d9a64a8bb8bd)
Ubuntu@ip-10.0.7.202 is the Public Instance of the Network. In the public network use the Public key to log in to the private network on the local machine.

Connect Private network using Public Network
1.log in or SSH Public Instance to the Local Machine.
2.Sudo su (Inside the Public Instance).
3.You need of Public Key (.pem file) to access or log in to the private instance.
4.Then you copy the.pem file from the local to the Public server using the SCP command.
5.scp -i ec2.pem ec2.pem ubuntu@3.216.23.4(Private IP):(destination path of .pem file).
6.Using private Instance IP inside the public instance.
7.Then you will be inside your private Network.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/ab692799-9936-428e-ba50-912838a91097)

SCP command copy .pem file Local to Public Network

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e7796280-c3c6-4bd3-80b2-b7f1eac345c3)
Log in to Private Network using Public Network

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/2e2c0fd9-fb20-4fa9-9604-0ac43a3a8b0b)
Aws Private Ec2 instance metadata

Thats it , all done !
