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
