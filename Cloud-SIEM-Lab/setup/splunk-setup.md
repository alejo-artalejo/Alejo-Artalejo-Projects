## AWS Splunk Access Policy Setup
![Splunk Access Policy Screenshot](../documentation/Splunk-User-Policy.png)

- Created **IAM policy** named `SplunkAccess`
- Policy grants Splunk permission to read S3 and SQS data needed for CloudTrail ingestion
- Added required actions using JSON for:
  - Retrieving CloudTrail logs from the S3 bucket  
  - Receiving CloudTrail notifications from SQS
  
## AWS Splunk Access User Setup
![Splunk Access User Screenshot](../documentation/Splunk-User-Group.png)

- Created IAM user named `Splunk_Access`
- Configured user for **Programmatic access only** to provide Access Key + Secret Key for Splunk
- Added user to the **SplunkAccessGroup**
- Attached previously created **SplunkAccess** policy to the group
- Downloaded the credentials `.csv` file for later use inside the Splunk Add-on for AWS
- This user will authenticate Splunk to securely pull CloudTrail, S3, and SQS data
## AWS CloudTrail SNS Event Notification Setup
![CloudTrail SNS Setup Screenshot](../documentation/splunk-sns.png)

- Enabled **SNS event notifications** for the CloudTrail trail and FlowsLogs
- Configured CloudTrail to publish a notification every time a new log file is delivered to S3
- SNS Topic created to act as the event broadcaster
- **Why:** SNS sends real time alerts so services like SQS (and later Splunk) know immediately when new CloudTrail and FlowLogs are ready for ingestion
## AWS CloudTrail SQS Queue Setup
![CloudTrail SQS Setup Screenshot](../documentation/splunk-sqs.png)

- Created **SQS queue** named `cloudtrail` and `flowlog` to receive notifications from the SNS topic
- Subscribed the queue to the CloudTrail SNS topic for automatic message delivery
- Allows Splunk to pull CloudTrail log events from SQS instead of scanning S3 directly
- **Why:** SQS provides reliable, ordered, fault tolerant message delivery that Splunk depends on to ingest CloudTrail logs without missing or duplicating events
