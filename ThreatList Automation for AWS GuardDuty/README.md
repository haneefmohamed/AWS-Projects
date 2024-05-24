# ThreatList Automation for AWS GuardDuty

This guide provides a step-by-step process to create a threat list, upload it to an S3 bucket, and integrate it with AWS GuardDuty.

## Prerequisites
1.AWS Account with appropriate permissions

2.Text editor (e.g., Notepad)

## Steps
### 1. Create a Threat List File

Open Notepad (or your preferred text editor).

Add the IP addresses you want to include in your threat list. Each IP address should be on a new line. For example:
```
192.168.1.1
203.0.113.45
198.51.100.23
```
Save the file as threatlist.txt.

### 2. Create an S3 Bucket

Open aws cosole

Go to s3

![Screenshot 2024-05-24 123840](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/036be087-a717-4c28-be99-cb67a81dc82e)

click on create bucket

![Screenshot 2024-05-24 123945](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/bdfa552b-c233-4b50-8ac8-7b7cb0ae7aa5)

give bucket details (give a name for your bucket)

![Screenshot 2024-05-24 124041](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/b3638a21-c9a0-435b-a834-5f3d3370e214)

click on create bucket

![Screenshot 2024-05-24 124100](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/b0997ab7-276a-42f0-8dfd-6df3181d8e7e)

### 3. Upload the Threat List to the S3 Bucket

Click on upload -> choose file -> Threatlist.txt -> Upload

![Screenshot 2024-05-24 124229](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d230497f-902a-42c2-a16c-61b07dd08fee)

### 4. Add the Threat List to GuardDuty

Go to the AWS Management Console.

Navigate to GuardDuty.

In the GuardDuty dashboard, select Lists from the left-hand menu.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/89001f2e-52d1-43a6-8721-cfd6b5e1d2f8)

Click on Add a Threat List.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/98bb125c-37b3-4d5a-bd0f-649807913230)

Fill in the details

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/057ebd75-29cf-42a8-9d55-fda74cf0b957)

Click Add.

### 5. Activate the Threat List

After adding the threat list, it needs to be activated.
In the GuardDuty dashboard, go to Lists.
Find your newly added threat list (threatlist) and activate it.

### 6. View GuardDuty Findings

Navigate to the Findings section in the GuardDuty dashboard.
Here you can see the findings based on the threat list you uploaded.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/6f008196-d637-4438-835d-f9ac65bab416)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/bc155b50-e7b7-41d3-82d8-e071f61a1d58)

## Conclusion
By following these steps, you have successfully created and uploaded a threat list to an S3 bucket, integrated it with AWS GuardDuty, and activated it to monitor for threats. If you have any issues or questions, please refer to the AWS GuardDuty Documentation or open an issue in this repository.
