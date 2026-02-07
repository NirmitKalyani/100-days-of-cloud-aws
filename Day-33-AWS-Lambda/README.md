# Day 33 – AWS Lambda Basic Function (Serverless)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge, this task focuses on creating a **basic AWS Lambda function** to demonstrate the fundamentals of serverless computing.

The objective was to deploy a simple Lambda function that returns a custom greeting message with a successful HTTP status code, highlighting **rapid deployment, scalability, and zero server management** using AWS Lambda.

---

## Concept
**AWS Lambda** is a serverless compute service that allows you to run code without provisioning or managing servers.

Key concepts involved:
- Serverless architecture
- AWS Lambda functions
- Lambda runtime (Python)
- IAM execution roles
- HTTP response handling
- Status codes

---

## Real-World Use Case
AWS Lambda is commonly used to:
- Build event-driven microservices
- Create lightweight APIs
- Automate operational tasks
- Handle backend logic without managing infrastructure
- Scale applications automatically based on demand

---

## Requirements
- **IAM role name:** `lambda_execution_role`
- **Lambda function name:** `nautilus-lambda`
- **Runtime:** Python
- **Response body:** `Welcome to KKE AWS Labs!`
- **Status code:** `200`

---

## AWS Services Used
- AWS IAM
- AWS Lambda

---

## Steps Performed

1. Opened **AWS Console → IAM → Roles**.

   ![Open IAM Roles](screenshots/step-1-open-iam.png)

2. Clicked **Create role**

   ![Create IAM Role](screenshots/step-2-create-role.png)

3. Selected **AWS service** as the trusted entity and Chose **Lambda** as the use case.

   ![Select Lambda Use Case](screenshots/step-3-select-lambda.png)

4. Attached the policy **`AdministratorAccess`** to allow lambda function to call AWS Services on my behalf.

   ![Attach Policy](screenshots/step-4-attach-policy.png)

5. Named the role **`lambda_execution_role`** and created it successfully.

   ![Role Created](screenshots/step-5-name-role.png)

   ![Role Created](screenshots/step-5-role-created.png)

6. Opened **AWS Console → Lambda**.

   ![Open Lambda Console](screenshots/step-6-open-lambda.png)

7. Clicked **Create function** and selected **Author from scratch**.

   ![Create Lambda Function](screenshots/step-7-create-function.png)

   ![Select Author from Scratch](screenshots/step-7-author-from-scratch.png)

8. Configured the function:
   - **Function name:** `nautilus-lambda`
   - **Runtime:** Python
   - **Execution role:** Use existing role
   - **IAM role:** `lambda_execution_role`

   ![Lambda Configuration](screenshots/step-8-function-config.png)

9. Created the Lambda function successfully and Added Python code to return the `Welcome to KKE AWS Labs!` message with status code `200`.

    ![Lambda Code](screenshots/step-9-lambda-code.png)

10. Clicked **Deploy** to save the changes.

    ![Deploy Lambda](screenshots/step-10-deploy.png)

11. Created a test event and executed the function.

    ![Test Lambda](screenshots/step-11-test-event.png)

    ![Test Executed](screenshots/verification-response.png)

---

## Verification
- IAM role **`lambda_execution_role`** created successfully  

  ![IAM Role Verified](screenshots/step-5-role-created.png)

- Lambda function **`nautilus-lambda`** created successfully  

  ![Lambda Verified](screenshots/step-9-lambda-code.png)

- Function returned response body **`Welcome to KKE AWS Labs!`** and status **200**

  ![Response Verified](screenshots/verification-response.png)

---

## Key Learnings
- IAM execution roles are mandatory for Lambda permissions
- Lambda requires CloudWatch access for logging
- Serverless architecture simplifies deployment
- Python is ideal for quick Lambda prototypes
- Proper sequencing (IAM → Lambda) is critical in AWS

---

**Status:** Completed 
