#  Creating an IAM user 

Step 1: AWS Login
Log into your AWS Management Console and select the IAM service.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/15d9cc08-d75b-4b0a-9719-b5fd7edc9d0d)

Step 2: Create a New User
In the side navigation menu, select Access management | Users, and then select Add user.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/37d1860d-cde0-48c2-b5ef-41fcfefb49d8)

Step 3: Set the User's Access Permissions and Name
In the Set user details section,

-In the User name field, enter the name of the new user (for example, "Provazio" — recommended).

-In the Access type field, check the Programmatic access option to allow the user only programmatic access.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/456a77df-3e4f-40f5-ace3-7caf0538bc95)

When you're done, select Next: Permissions.

Step 4: Create a Policy
Select Attach existing policies directly, and then select Create policy.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/a4a22dcf-2449-49a0-acb9-539dbf2220db)

Download the platform IAM policy file provazio-eks.json for an EKS cluster. Edit the file to replace all $AWS_ACCOUNT_ID instances with your AWS Account ID.

Paste the contents of your selected policy file in the JSON tab of the AWS Management Console and select Review policy. Give the policy a name (for example, "ManageIguazioSystems" — recommended), optionally add a description, and select Create policy.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/5dcf41c4-72bf-4b3d-9b47-3485abada4ab)

Step 5: Create the User
Filter the policies for the name of the policy that you created and select the policy.

Select Next: Tags and optionally assign user tags.

Select Next: Review and review your role definition. When you're ready, select Create user.

Step 6: Save the User Credential
Download and save the credentials of the new user (Access key iD and Secret access key).

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/c558b1f4-cd19-483e-bfbf-5be49dc53f41)

