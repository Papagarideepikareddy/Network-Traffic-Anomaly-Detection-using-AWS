# Network-Traffic-Anomaly-Detection-using-AWS
# Description:
This AWS CloudFormation template sets up VPC Flow Logs with CloudWatch monitoring and SNS email alerts to detect network traffic anomalies. It creates an S3 bucket, IAM roles, CloudWatch Log Group with metric filters, alarms for unusual traffic patterns, and an SNS topic for notifications. This infrastructure helps identify and respond to potential security or operational issues in your VPC traffic.
# Overview
This repository contains an AWS CloudFormation template that provisions the core infrastructure to monitor VPC network traffic anomalies using VPC Flow Logs, CloudWatch, and SNS email alerts. This setup helps detect unusual network traffic patterns that could indicate security issues, misconfigurations, or unexpected spikes in usage.
# What This Template Deploys
1. An S3 bucket with restricted public access for storing logs or additional monitoring data.
2.  A VPC Flow Log configuration that captures all network traffic for a specified VPC and sends the logs to CloudWatch Logs.
3.  An IAM Role with permissions for VPC Flow Logs to publish logs to CloudWatch.
4.  A CloudWatch Log Group and Metric Filter that converts specific log patterns into custom CloudWatch metrics.
5.  A CloudWatch Alarm that triggers when the number of flow log records exceeds a threshold within a short period — indicating possible network anomalies.
6.  An SNS Topic and Email Subscription to notify stakeholders immediately when an anomaly is detected.
# How It Works
1. Flow Logs: Captures VPC-level network traffic.
2. CloudWatch Metric Filter: Creates a custom metric (FlowCount) each time a flow log entry matches the filter.
3. CloudWatch Alarm: Watches the FlowCount metric and triggers if traffic exceeds the defined threshold (Threshold: 30 in 30 seconds).
4. SNS Topic: Sends an email alert to the specified email address when the alarm is triggered.
# Parameters
| Parameter      | Description                                         |
| -------------- | --------------------------------------------------- |
| `VPCId`        | The ID of the existing VPC you want to monitor.     |
| `EmailAddress` | The email address that will receive anomaly alerts. |
# Outputs
| Output               | Description                                               |
| -------------------- | --------------------------------------------------------- |
| `S3BucketName`       | The name of the created S3 bucket for traffic monitoring. |
| `SNSTopicArn`        | ARN of the SNS topic used for alerting.                   |
| `CloudWatchLogGroup` | Name of the CloudWatch Log Group storing VPC Flow Logs.   |
# Deployment Instructions
1. Download or copy this cloudformation.yml file.
2. Go to your AWS CloudFormation Console.
3. Click Create Stack → With new resources (standard).
4. Upload the template file or paste the YAML directly.
5. Provide required parameters (VPCId and EmailAddress).
6. Review and launch the stack.
7. Confirm your email subscription: After the stack is created, check your email inbox and confirm the SNS subscription to start receiving alerts.
# Notes
1. This template creates an alarm on VPC Flow Logs, not directly on S3 access logs. However, unusual VPC traffic may indirectly indicate abnormal S3 usage.
2. Always review IAM roles and permissions for security best practices.
3. Adjust thresholds to suit your environment’s normal traffic levels.
# Technologies Used
1. AWS CloudFormation
2. VPC Flow Logs
3. CloudWatch Logs & Alarms
4. SNS (Simple Notification Service)
5. I AM Roles & Policies
6. S3 Bucket
   
