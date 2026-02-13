# Day 46 – Automating Secure File Transfer Between S3 Buckets Using Lambda and DynamoDB

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on building a secure and automated file transfer workflow using AWS serverless services.

The objective was to:

- Create a **public S3 bucket** for file uploads  
- Create a **private S3 bucket** for secure storage  
- Configure a **Lambda function** to automatically copy files  
- Store transfer logs in a **DynamoDB table**  
- Monitor execution using **CloudWatch Logs**

Whenever a file is uploaded to the public bucket, the Lambda function is triggered automatically. It copies the file to the private bucket and logs transfer details such as source bucket, destination bucket, object key, status, and timestamp in DynamoDB.

---

## Concept

This task demonstrates important cloud architecture principles:

- Event-driven architecture using S3 triggers  
- Serverless compute with AWS Lambda  
- Secure IAM role-based access  
- NoSQL logging with DynamoDB  
- Monitoring with CloudWatch  
- Public vs Private S3 bucket access control  

This is a real-world pattern used in secure ingestion pipelines.

---

## Real-World Use Case

In production systems:

- Public uploads should not directly expose internal storage.
- Files are processed and moved securely.
- Audit logs are mandatory for compliance.
- Automation eliminates manual intervention.

This pattern is widely used in secure document upload portals and media processing pipelines.

---

## Requirements

- **Public S3 Bucket:** `xfusion-public-22769`
- **Private S3 Bucket:** `xfusion-private-19821`
- **Lambda Function:** `xfusion-copyfunction`
- **IAM Role:** `lambda_execution_role`
- **DynamoDB Table:** `xfusion-S3CopyLogs`
  - Partition Key: `LogID` (String)
- **Trigger Event:** S3 PUT event
- **Test File:** `sample.zip`

---

## AWS Services Used

- Amazon S3  
- AWS Lambda  
- AWS IAM  
- Amazon DynamoDB  
- Amazon CloudWatch  

---

# Steps Performed

---

## Public S3 Bucket Setup

### 1. Navigated to S3 Service
Opened AWS Console → Services → S3 → Clicked **Create Bucket**.

![Go to S3](screenshots/ss1-go-to-s3.png)

---

### 2. Configured Public Bucket Details
Selected **General Purpose** bucket type and entered bucket name `xfusion-public-22769`.

![Public Bucket Name](screenshots/ss2-public-bucket-name.png)

---

### 3. Disabled Block Public Access
Unchecked **Block all public access** to allow public object access and proceeded to create the bucket.

![Disable Block Public Access](screenshots/ss3-disable-public-block.png)

---

### 4. Verified Public Bucket Creation
Confirmed that `xfusion-public-22769` was successfully created.

![Bucket Policy](screenshots/ss5-bucket-policy.png)

---

### 5. Added Bucket Policy
Navigated to **Permissions tab** → Edited bucket policy →  
Allowed `s3:GetObject` permission on all objects with:

- Principal: `*`
- Effect: Allow

This made uploaded objects publicly accessible.

![Public Bucket Created](screenshots/ss4-public-bucket-created.png)

---

## Private S3 Bucket Setup

### 6. Created Private Bucket
Clicked **Create Bucket**, selected **General Purpose**, and named it `xfusion-private-19821`.

![Create Private Bucket](screenshots/ss6-private-bucket.png)

---

### 7. Verified Private Bucket
Confirmed the bucket was created successfully with **Block Public Access enabled by default**.

![Private Bucket Created](screenshots/ss7-private-bucket-created.png)

---

## Lambda Function Configuration

### 8. Navigated to Lambda
Opened AWS Console → Services → Lambda.

![Go to Lambda](screenshots/ss8-go-to-lambda.png)

---

### 9. Created Lambda Function
Clicked **Create Function** → Author from scratch:

- Function name: `xfusion-copyfunction`
- Runtime: Python 3.14

![Create Lambda Function](screenshots/ss9-create-lambda.png)

---

### 10. Selected IAM Role Creation
Under Execution Role, chose to **create a new IAM role**.

![Create Role Option](screenshots/ss10-create-role-option.png)

---

### 11. Configured Trusted Entity
On IAM role creation page:

- Trusted Entity Type: AWS Service  
- Use Case: Lambda  

Clicked Next.

![Trusted Entity](screenshots/ss11-trusted-entity.png)

---

### 12. Added S3 Full Access Policy
Attached `AmazonS3FullAccess` policy.

![S3 Policy](screenshots/ss12-s3-policy.png)

---

### 13. Added DynamoDB Full Access Policy
Attached `AmazonDynamoDBFullAccess` policy.

![DynamoDB Policy](screenshots/ss13-dynamodb-policy.png)

---

### 14. Added Lambda Basic Execution Role
Attached `AWSLambdaBasicExecutionRole` policy and proceeded.

![Lambda Basic Policy](screenshots/ss14-lambda-basic-policy.png)

---

### 15. Named the IAM Role
Provided role name as `lambda_execution_role` and created the role.

![Role Named](screenshots/ss15-role-name.png)

---

### 16. Linked Role to Lambda
Returned to Lambda creation page → Selected **Use existing role** → Chose `lambda_execution_role`.

![Select Existing Role](screenshots/ss16-select-role.png)

---

### 17. Verified Lambda Creation
Confirmed that `xfusion-copyfunction` was successfully created.

![Lambda Created](screenshots/ss17-lambda-created.png)

---

### 18. Accessed Lambda Code from Client
On AWS client host, viewed `lambda-function.py` located under `/root/` using `cat` command and copied the entire code.

![View Lambda Code](screenshots/ss18-view-lambda-code.png)

---

### 19. Updated Lambda Function Code
Pasted the code into Lambda editor and replaced:

- `REPLACE-WITH-YOUR-DYNAMODB-TABLE` → `xfusion-S3CopyLogs`
- `REPLACE-WITH-YOUR-PRIVATE-BUCKET` → `xfusion-private-19821`

Clicked **Deploy** to update the function.

![Deploy Lambda Code](screenshots/ss19-deploy-lambda.png)

---

## DynamoDB Configuration

### 20. Navigated to DynamoDB
Opened AWS Console → Services → DynamoDB → Clicked **Create Table**.

![Go to DynamoDB](screenshots/ss20-go-to-dynamodb.png)

---

### 21. Created DynamoDB Table
Configured:

- Table Name: `xfusion-S3CopyLogs`
- Partition Key: `LogID`
- Type: String

Kept remaining settings default and created table.

![Create DynamoDB Table](screenshots/ss21-create-dynamodb.png)

---

### 22. Verified Table Status
Confirmed table was successfully created and status showed **Active**.

![DynamoDB Active](screenshots/ss22-dynamodb-active.png)

---

## Trigger Configuration

### 23. Added Trigger to Lambda
Opened Lambda function → Clicked **Add Trigger**.

![Add Trigger](screenshots/ss23-add-trigger.png)

---

### 24. Configured S3 Trigger
Configured trigger as:

- Trigger Type: S3  
- Bucket: `xfusion-public-22769`  
- Event Type: PUT  
- Enabled recursive invocation  

Clicked Create.

![Configure Trigger](screenshots/ss24-configure-trigger.png)

---

### 25. Verified Trigger
Confirmed trigger was successfully added to Lambda function.

![Trigger Added](screenshots/ss25-trigger-added.png)

---

## Verification
The following validations confirm successful task completion:

- Copied `sample.zip` from `/root/` on AWS client and uploaded it to the public S3 bucket.

    ![Upload File CLI](screenshots/ss26-upload-cli.png)

- Confirmed `sample.zip` was visible inside `xfusion-public-22769`.

    ![Public Bucket File](screenshots/ss27-public-file.png)

- Checked `xfusion-private-19821` and confirmed the file was automatically copied by Lambda.

    ![Private Bucket File](screenshots/ss28-private-file.png)

- Reviewed CloudWatch Logs to confirm successful Lambda execution and file copy operation.

    ![CloudWatch Logs](screenshots/ss29-cloud-watch.png)

- Confirmed a new item was created in `xfusion-S3CopyLogs`.

    ![DynamoDB Attributes](screenshots/ss31-dynamodb-attributes.png)

- Opened the item and verified the following attributes:
  - DestinationBucket  
  - ObjectKey  
  - SourceBucket  
  - Status  
  - Timestamp  

    ![DynamoDB Item](screenshots/ss30-dynamodb-item.png)    

---

## Outcome

Successfully implemented an **automated, secure, event-driven file transfer architecture**.

The solution now:

- Automatically copies uploaded files  
- Secures internal storage  
- Maintains audit logs  
- Provides monitoring and observability  
- Eliminates manual file management  

---

## Learnings

- S3 events can trigger automated workflows  
- IAM roles enable secure service-to-service communication  
- Lambda allows serverless automation  
- DynamoDB is efficient for logging structured events  
- CloudWatch is essential for debugging and monitoring  
- Public and private bucket configurations are critical for security  

---

**Status:** Completed 
