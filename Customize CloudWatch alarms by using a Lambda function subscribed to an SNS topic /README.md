# Customize CloudWatch alarms by using a Lambda function subscribed to an SNS topic

Prerequisites:

Basic knowledge of AWS services, including CloudWatch, Lambda, and SNS.

1.An AWS account with permissions to create and manage Lambda functions and SNS topics.
2.An existing CloudWatch alarm that triggers when an event occurs, such as a metric exceeding a certain threshold or an API call returning an error code.
3.Familiarity with programming in a language that Lambda supports, such as Python, Node.js, or Java.
4.Access to a development environment with the necessary tools, such as an IDE or text editor, and an AWS SDK for the chosen programming language.
5.An understanding of JSON format and how to parse and modify JSON payloads.
6.Familiarity with SNS subscription protocols and configuration, such as HTTP, HTTPS, email, and SMS.

Step 1: Create SNS topic for notification.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/079bf4a0-3394-4959-a70d-516deafa2e43)

Create an SNS topic and use endpoints to subscribe to it. Later you’ll add the SNS topic ARN to the Lambda function environment variable or in the code.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d3190871-0eb7-4e1e-aaa0-42e311df06aa)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/5a0405a1-3620-450a-b0cc-771d95f26b48)

To create SNS topic

Sign in to the Amazon SNS console, and from the left navigation pane, choose Topics.
On the Topics page, choose Create topic.
By default, the console creates a FIFO topic. Choose Standard.
In Details, enter a name for the topic (for example, ekant-test), and then choose Create topic.
To create a subscription to the topic

In the left navigation pane, choose Subscriptions.
On the Subscriptions page, choose Create subscription.
On the Create subscription page, choose the Topic ARN field to see a list of the topics in your AWS account.
Choose the topic that you created in the previous step.
For Protocol, choose HTTP/HTTPS.
For Endpoint, enter a web server that can receive notifications from Amazon SNS.
Choose Create subscription.
Check your endpoint and choose Confirm subscription.

Step 2:

Create one lambda function with Below code and add the necessary permissions, you can modify the Lambda function’s execution role to include the following policies:

AmazonSNSFullAccess: This policy grants the Lambda function permission to publish messages to an SNS topic.
CloudWatchLogsFullAccess: This policy grants the Lambda function permission to write logs to CloudWatch.

By adding these policies to the Lambda function’s execution role, you can ensure that the Lambda function has the necessary permissions to publish notifications to an SNS topic and send logs to CloudWatch.

// import json
import boto3
client = boto3.client('sns')
 

def lambda_handler(event, context):
    message_payload = json.loads(event['Records'][0]['Sns']['Message'])
    timestamp_payload = (event['Records'][0]['Sns']['Timestamp'])
    alarm_name = message_payload['AlarmName']
    region = message_payload['Region']
    alarm_description = message_payload['AlarmDescription']
    new_state_value = message_payload['NewStateValue']
    state_change_time = message_payload['StateChangeTime']
    alarmarn = message_payload['AlarmArn']
    timestamp = timestamp_payload
    newstatereason = message_payload['NewStateReason']
    account_id = message_payload['AWSAccountId']
    name_space = message_payload['Trigger']['Namespace']
    subject = f"ALARM: {alarm_name} in {region} is {new_state_value}"
    dimensions = message_payload['Trigger']['Dimensions']
    message = (
        f"Alarm Name: {alarm_name}\n"
        f"Region: {region}\n"
        f"New State Value: {new_state_value}\n"
        f"Description: {alarm_description}\n"
        f"State Change Time: {state_change_time}\n"
        f"AlarmArn: {alarmarn}\n"
        f"Timestamp: {timestamp}\n"
        f"NewStateReason: {newstatereason}\n"
        f"AWSAccountId: {account_id}\n"
        f"Namespace: {name_space}\n"
        f"Dimensions: {dimensions}\n"
)
    response = client.publish(TopicArn='arn:aws:sns:ap-southeast-2:*******:',Message=message,Subject=subject)
    print("Message published")
    return(response) //

Step:3 Create new SNS topic and subscription for lambda.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/19c9c3e8-711a-4c86-b35f-e8eb8fcfa98c)

Sign in to the Amazon SNS console, and in the left navigation pane, choose Topics and create another topic for lambda subscription.

On the Topics page, choose Create topic.
By default, the console creates a FIFO topic. Choose Standard.
In the Details section, enter a name for the topic (for example, AlarmActionSNSTopic).
Scroll to the end of the form and choose Create topic.
To create a subscription to the topic for your Lambda function  

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/586933ce-e965-4675-bb7d-a53f6e2c7136)

In the left navigation pane, choose Subscriptions.
On the Subscriptions page, choose Create subscription.
On the Create subscription page, choose the Topic ARN field to see a list of the topics in your AWS account.
Choose the topic that you created in the previous step.
For Protocol, choose AWS Lambda.
For Endpoint, enter the ARN for your Lambda function.
Choose Create subscription.
Step 4: Add Cloudwatch Alarm action.

Edit your alarm action and add the SNS topic ARN for alarm notification actions created in step 1.

To edit your alarm action

Open the CloudWatch console and from the left navigation pane, choose Alarms.
Choose the name of the alarm, choose Edit, and choose Next.
Under Notification, choose In alarm. From Send a notification to, choose your SNS topic for alarm notification, and then choose Next.
Under Preview and create, review the information and conditions, and then choose Update alarm.
Let’s take one cloudwatch alert for any resources which is already created.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/e6dff0c9-fffa-4805-b8d3-c0462a3aa500)

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/d925e335-1b13-4131-84eb-31d58cef0249)

Click Next and save.

Step 5: Let’s trigger the alarm manually for now insted of making changes in the threshold.

Hit below command in the cloudshell.

aws cloudwatch set-alarm-state — alarm-name “testing-alert” — state-value ALARM — state-reason “SET TO ALARM”

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/769bf470-8f86-4b60-8435-433ce9b8c659)

Once you have configured the Lambda function to publish notifications to an SNS topic and send logs to CloudWatch, you can check the CloudWatch logs to see if the function is producing any errors.

If there are no errors, you should receive a response from the Lambda function, rather than a long JSON payload. This is because the Lambda function will have processed the JSON payload and formatted the alert notification before publishing it to the SNS topic.

By checking the CloudWatch logs, you can ensure that the Lambda function is functioning correctly and that the alert notifications are being properly formatted and published to the SNS topic. This can help you to identify and address any issues or errors in the Lambda function, and ensure that your alert notifications are delivered effectively.

Below is the format which you will get it. You can customize this message format according to your specific requirements by modifying the Lambda function code. For example, you can include additional information in the message, such as the value of the metric, the time of the alert, or any relevant tags or metadata associated with the resource being monitored.

![image](https://github.com/haneefmohamed/AWS-Projects/assets/159698808/f8b6dc82-9428-49f9-9f8e-2755dc132bff)

I hope this solution is helpful for those looking to improve the appearance of alerts received from CloudWatch for HTTP/HTTPS endpoints.

