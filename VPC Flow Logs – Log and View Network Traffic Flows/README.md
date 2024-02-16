# VPC Flow Logs – Log and View Network Traffic Flows

Enabling VPC Flow Logs
You can enable VPC Flow Logs from the AWS Management Console or the AWS Command Line Interface (AWS CLI), or by making calls to the EC2 API. Here’s how you would enable them for a VPC:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/93e9c671-82b3-4865-84d2-61072703caaf)

This will display the Create Flow Log wizard:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/4a50f6a2-555a-4da6-be33-ab57a1709554)

New Flow Logs will appear in the Flow Logs tab of the VPC dashboard.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/8f09afdd-5ee0-4c14-ad78-2cc8ced2b347)

The Flow Logs are saved into log groups in CloudWatch Logs. The log group will be created approximately 15 minutes after you create a new Flow Log. You can access them via the CloudWatch Logs dashboard.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/665fbaf2-740e-49c4-9bea-1cb91d97a3c6)

Each group will contain a separate stream for each Elastic Network Interface (ENI):

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/73988039-48cf-48ee-b88d-a4853226ff5c)

Each stream, in turn, contains a series of flow log records:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/6a540561-d0a7-4415-be1d-83d4f75efcbb)

All done !!
