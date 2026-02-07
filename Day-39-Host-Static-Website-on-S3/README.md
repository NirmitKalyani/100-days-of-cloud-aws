# Day 39 – Host a Static Website Using Amazon S3

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on hosting a **static website** using **Amazon S3**.

The objective was to create an **S3 bucket**, configure it for **static website hosting**, allow **public access**, upload an `index.html` file from the aws-client host, and verify that the website is accessible via the **S3 website endpoint**.

---

## Concept
This task demonstrates how Amazon S3 can be used as a **serverless web hosting platform** for static content.

Key concepts involved:
- Amazon S3 bucket creation
- Static website hosting configuration
- Public access permissions
- Bucket policies
- Hosting HTML content without servers

---

## Real-World Use Case
Hosting static websites on S3 is commonly used for:
- Company landing pages
- Documentation portals
- Personal blogs
- Error pages for applications
- Lightweight public websites with low cost and high availability

---

## Requirements
- **AWS Region:** `us-east-1`
- **S3 Bucket Name:** `devops-web-328`
- **Index Document:** `index.html`
- **Source File Location:** `/root/index.html` (aws-client host)
- **Public Access:** Enabled
- **Website Access:** Via S3 website URL

---

## AWS Services Used
- Amazon S3
- AWS CLI

---

## Steps Performed

### 1. Navigated to Amazon S3
Logged in to the AWS Management Console and navigated to the **Amazon S3** service.

![Go to S3](screenshots/ss1-go-to-s3.png)

---

### 2. Created an S3 Bucket
Clicked **Create bucket** and selected:
- Bucket type: **General purpose**
- Bucket name: `devops-web-328`

![Create Bucket](screenshots/ss2-create-bucket.png)

Disabled **Block all public access** to allow public website hosting.

![Disable Public Access Block](screenshots/ss3-disable-public-access.png)

Successfully created the bucket.

![Bucket Created](screenshots/ss4-bucket-created.png)

---

### 3. Enabled Static Website Hosting
Navigated to the **Properties** tab of the bucket.

![Bucket Properties](screenshots/ss5-bucket-properties.png)

Edited **Static website hosting** settings and enabled it with:
- Index document: `index.html`

![Enable Website Hosting](screenshots/ss6-enable-website-hosting.png)

Verified the static website configuration and copied the **bucket website endpoint**.

![Website Endpoint](screenshots/ss7-website-endpoint.png)

---

### 4. Configured Bucket Policy for Public Access
Navigated to the **Permissions** tab and edited the bucket policy to allow public read access.

![Edit Bucket Policy](screenshots/ss8-edit-bucket-policy.png)

Added a policy allowing `s3:GetObject` on all objects in the bucket.

![Bucket Policy Added](screenshots/ss9-bucket-policy-added.png)

---

### 5. Uploaded index.html File
Copied the `index.html` file from `/root/` directory of the aws-client host to the S3 bucket.

![Upload File](screenshots/ss10-upload-index-file.png)

Verified that the file was successfully uploaded.

![File Uploaded](screenshots/ss11-file-uploaded.png)

---

## Verification
The following steps confirm successful completion of the task:

- S3 bucket `devops-web-328` created successfully.

  ![Bucket Created](screenshots/ss4-bucket-created.png)

- Static website hosting enabled with `index.html` as the index document.

  ![Website Hosting Enabled](screenshots/ss6-enable-website-hosting.png)

- Public bucket policy applied allowing read access.

  ![Bucket Policy](screenshots/ss9-bucket-policy-added.png)

- `index.html` file uploaded successfully to the bucket.

  ![File Uploaded](screenshots/ss11-file-uploaded.png)

- Website accessible via S3 website endpoint and displaying expected content.

  ![Website Accessible](screenshots/ss12-website-accessible.png)

---

## Outcome
A static website was successfully hosted using **Amazon S3**, making the content publicly accessible without using any servers or compute services.

---

## Learnings
- S3 can host static websites efficiently
- Public access must be explicitly allowed
- Bucket policies control object-level permissions
- Static website hosting is cost-effective and highly available
- S3 website endpoints differ from standard S3 object URLs

---

**Status:** Completed
