# AWS Serverless Architecture Project

## 🚀 Overview

This project demonstrates the integration of several AWS services to create a **serverless event-driven architecture**. It includes automatic reactions to file uploads, notifications, and data storage.

---

## 📦 AWS S3, Lambda, SNS, Slack, CloudWatch, DynamoDB Integration

### 🛠️ Architecture Components

1. **Amazon S3 Bucket**
   - **Versioning**: Enabled
   - **Encryption**: SSE-S3
   - **Public Access**: Blocked
   - **Event Trigger**: Triggers Lambda on object upload (PUT)

2. **Amazon SNS (Simple Notification Service)**
   - Topic created
   - Email subscription confirmed

3. **Slack Integration**
   - Slack channel: `#aws-alerts`
   - Webhook URL configured for incoming alerts

4. **Amazon DynamoDB**
   - Table: `s3-upload-metadata`
   - Partition Key: `fileName` (String)
   - Sort Key: `uploadTimestamp` (String, optional)

5. **AWS Lambda**
   - Runtime: Python 3.12
   - Triggered by S3 PUT events
   - Sends notifications to Slack and SNS
   - Stores metadata in DynamoDB
   - **Environment Variables**:
     - `SLACK_WEBHOOK_URL`
     - `SNS_TOPIC_ARN`
     - `DDB_TABLE_NAME`

6. **IAM Role and Permissions**
   - Lambda basic execution
   - S3 read-only
   - SNS publish
   - DynamoDB write

### 📈 Workflow

```text
S3 Upload ➜ Lambda Trigger ➜ Slack Notification
                             ➜ SNS Email Notification
                             ➜ DynamoDB Metadata Storage

