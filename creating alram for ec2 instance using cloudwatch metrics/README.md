# Create an alarm for an ec2 instance using cloudwatch

Ensure the right permissions
Ensure you have the proper CloudWatch permissions to create and manage
Alarms. In general, Access control and writing permission policies are attached to IAM identities, AWS provides a table with API operations with the respectively required permissions.

Initiate the process
To start the process, you will have to first open the CloudWatch Console and use the navigation page to expand “Alarms”, then press on “All Alarms” >“Create Alarm”: 

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/17b88911-c526-4e6c-a8ae-0a244c6b3159)

Condition phase
The first step in creating an Alarm is specifying the metric and conditions. When pressing the “Select Metric” button on the user interface below, the user will have to specify a single CloudWatch metric or add an algebraic expression built around that value metric. Usually, the action that will come next would be associated with a threshold value assigned to a specific metric over a number of time periods.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/090eb370-ebda-4fc4-baef-f6dea3d6c3d8)

Choosing the metric
Select the metric to monitor with the alarm. The metric options include the free provided insights into resources like Amazon EC2 instances, Amazon EBS volumes, and Amazon RDS DB instances. Detailed monitoring is also supported if enabled, in addition to personal application metrics as those can be added for search, graphing, and alarms.

In the example below, we are monitoring CPU utilization across all EC2 instances:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/931455cf-d7f2-404e-8621-92b8987b3530)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/fd53b876-742e-44a2-8730-1549f540f60e)

Statistics and time periods
After choosing the proper metric, you can now choose the statistics which represent aggregations over a time frame pre-determined by the user. In this step, it’s important to wisely pick the Period of time as the values collected will span the specified timeframe. CloudWatch supports a list of statistics documented by AWS here.

As for the conditional options, the user will have the option to define a value or band as a threshold with a specific mathematical condition (greater, lower, lower\equal, greater\equal).

In the example below, we are setting the alarm threshold to 10% of the average CPU utilization over 5 minutes:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/b2a458bc-02a8-4fa5-ae9e-c95005a3f732)

Configure actions
After deliberately defining the conditions, next comes choosing the actions that will be triggered given said conditions. The user will have multiple actionable options such as: sending a notification to an Amazon SNS topic, performing an Amazon EC2 action or an Amazon EC2 Auto Scaling action, or creating an OpsItem or incident in Systems Manager.

In the example below, we are choosing an SNS notification, with an existing SNS topic:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/f3a4c4ab-c022-45de-9cdb-981a47be3219)

Name and description
Next, enter a name for the new alarm. Users can briefly describe the alarm – this is optional, but is recommended if you create many similar alarms:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/0f1159d5-f61c-4b12-829c-2cca1c9c2b9c)

Summary
Finally, the user can review the alarm preview which summarizes the alarm metric, conditions, and action:

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/76b8ee41-0037-4639-b902-1f97230b9c89)

After thoroughly assessing the summary; if the alarm has been configured correctly, the user simply clicks “Create Alarm”.


