## AWS Splunk Access Policy Setup
![Splunk Access Policy Screenshot](../documentation/splunk-access-policy.png)

- Created **IAM policy** named `SplunkAccess`
- Policy grants Splunk permission to read S3 and SQS data needed for CloudTrail ingestion
- Added required actions for:
  - Retrieving CloudTrail logs from the S3 bucket  
  - Receiving CloudTrail notifications from SQS  
- Policy JSON used:

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": [
       "sqs:GetQueueAttributes",
       "sqs:ListQueues",
       "sqs:ReceiveMessage",
       "sqs:GetQueueUrl",
       "sqs:SendMessage",
       "sqs:DeleteMessage",
       "s3:ListBucket",
       "s3:GetObject",
       "s3:GetBucketLocation"
     ]
   }
 ]
}
