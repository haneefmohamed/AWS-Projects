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
