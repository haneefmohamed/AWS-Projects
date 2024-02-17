# Getting Started with CloudWatch Logs

Step 1: Permissions
CloudWatch uses the Identity and Access Management (IAM) service for authentication and authorization. In this blog post, we’re using a feature of IAM called IAM Roles for EC2, which lets us associate specific permissions with an Amazon EC2 instance when you launch it.

In this case, we have an instance we launched with the permissions for the IAM role for all logs actions with the following policy
    
    “Version”: “2012-10-17”,
 
      “Statement”: [
   
    {
     “Effect”: “Allow”,
      “Action”: [
        “logs:*”
      ],
      “Resource”: [
        “arn:aws:logs:*:*:*”
      ]
    }
