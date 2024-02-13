# Create an alarm using the Amazon EC2 console

Open the Amazon EC2 console at https://console.aws.amazon.com/ec2/.

In the navigation pane, choose Instances.

Select the instance and choose Actions, Monitor and troubleshoot, Manage CloudWatch alarms.

On the Manage CloudWatch alarms detail page, under Add or edit alarm, select Create an alarm.

For Alarm notification, choose whether to configure Amazon Simple Notification Service (Amazon SNS) notifications. Enter an existing Amazon SNS topic or enter a name to create a new topic.

![sns_-_topic_details](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/30900026-d51c-43b2-81d5-cc6b6e800552)


For Alarm action, choose whether to specify an action to take when the alarm is triggered. Choose an action from the list.

For Alarm thresholds, select the metric and criteria for the alarm. For example, to create an alarm that is triggered when CPU utilization reaches 80% for a 5 minute period, do the following:


![Example-Picture-1-2](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/437fdd9a-027c-4d2c-9753-a07a52eae125)



Keep the default setting for Group samples by (Average) and Type of data to sample (CPU utilization).

Choose >= for Alarm when and enter 0.80 for Percent.

Enter 1 for Consecutive period and select 5 minutes for Period.

(Optional) For Sample metric data, choose Add to dashboard.

Choose Create.

You can edit your CloudWatch alarm settings from the Amazon EC2 console or the CloudWatch console. If you want to delete your alarm, you can do so from the CloudWatch console. For more information, see Editing or deleting a CloudWatch alarm in the Amazon CloudWatch User Guide.
