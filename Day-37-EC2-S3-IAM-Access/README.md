# Day 37 – EC2 to S3 Access Using IAM Role and SSH Key Authentication (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on enabling an **EC2 instance to securely interact with a private S3 bucket** using **IAM roles and policies**, along with configuring **passwordless SSH access**.

The objective was to allow an existing EC2 instance **`datacenter-ec2`** to upload and retrieve files from a **private S3 bucket**, without using static AWS credentials.

---

## Concept
AWS **IAM Roles** provide temporary credentials to EC2 instances, allowing secure access to AWS services without embedding access keys.

By combining:
- IAM roles and policies
- Private S3 buckets
- SSH key-based authentication
  
we achieve a **secure and scalable EC2-to-S3 integration**.

---

## Real-World Use Case
This setup is commonly used when:
- Applications on EC2 store data in S3
- Credentials must not be hardcoded
- Buckets must remain private
- Secure administration access is required
- Least-privilege access is enforced

---

## Requirements
- **EC2 instance:** `datacenter-ec2`
- **S3 bucket:** `datacenter-s3-7325`
- **IAM role:** `datacenter-role`
- **IAM policy permissions:**
  - `s3:PutObject`
  - `s3:GetObject`
  - `s3:ListBucket`
- **SSH key pair:** `id_rsa` / `id_rsa.pub`

---

## AWS Services Used
- Amazon EC2
- Amazon S3
- AWS IAM
- Security Groups

---

## Steps Performed

### EC2 Verification and Security Group Configuration

1. Navigated to **Services → EC2**.

   ![Open EC2](screenshots/step-01-open-ec2.png)

2. Verified that **`datacenter-ec2`** was in running state.

   ![EC2 Running](screenshots/step-02-datacenter-ec2-running.png)

3. Reviewed the security group attached to the EC2 instance.

   ![View EC2 SG](screenshots/step-03-view-ec2-sg.png)

4. Opened the default security group attached to the EC2 instance.

   ![Open Default SG](screenshots/step-04-open-default-sg.png)

5. Edited inbound rules to allow SSH access from anywhere.

   ![Add SSH Rule](screenshots/step-05-add-ssh-rule.png)

6. Verified the SSH rule was added successfully.

   ![SSH Rule Verified](screenshots/step-06-ssh-rule-verified.png)

---

### SSH Key Pair Setup

7. Generated a new SSH key pair using `ssh-keygen` and copied the public key.

   ![Generate SSH Keys](screenshots/step-07-generate-ssh-keys.png)

8. Connected to the EC2 instance using **EC2 Instance Connect**.

   ![EC2 Instance Connect](screenshots/step-08-ec2-instance-connect.png)

9. Edited the `authorized_keys` file for the root user.

   ![Edit Authorized Keys](screenshots/step-09-edit-authorized-keys.png)

10. Pasted the public key into `authorized_keys`.

    ![Paste Public Key](screenshots/step-10-paste-public-key.png)

11. Verified the public key was saved correctly.

    ![Verify Authorized Keys](screenshots/step-11-verify-authorized-keys.png)

12. Successfully SSHed into **`datacenter-ec2`** from `aws-client` without a password.

    ![SSH Success](screenshots/step-12-ssh-success.png)

---

### Private S3 Bucket Creation

13. Navigated to **Services → S3** and started bucket creation.

    ![Open S3](screenshots/step-13-open-s3.png)

14. Created a bucket named **`datacenter-s3-7325`**.

    ![Create S3 Bucket](screenshots/step-14-create-s3-bucket.png)

15. Set object ownership to **ACLs disabled**.

    ![Object Ownership](screenshots/step-15-object-ownership.png)

16. Enabled **Block all public access** to keep the bucket private.

    ![Block Public Access](screenshots/step-16-block-public-access.png)

17. Verified the S3 bucket was created successfully.

    ![S3 Created](screenshots/step-17-s3-created.png)

---

### IAM Policy and Role Configuration

18. Navigated to **IAM → Policies**.

    ![Open IAM Policies](screenshots/step-18-open-iam-policies.png)

19. Clicked **Create policy**.

    ![Create Policy](screenshots/step-19-create-policy.png)

20. Switched to JSON editor and defined S3 permissions.

    ![IAM Policy JSON](screenshots/step-20-policy-json.png)

21. Named the policy **`datacenter-policy`**.

    ![Name Policy](screenshots/step-21-name-policy.png)

22. Verified the IAM policy was created successfully.

    ![Policy Created](screenshots/step-22-policy-created.png)

23. Navigated to **IAM → Roles** and clicked **Create role**.

    ![Create Role](screenshots/step-23-create-role.png)

24. Selected **AWS Service** as trusted entity and **EC2** as use case.

    ![Role Use Case](screenshots/step-24-role-usecase.png)

25. Attached **`datacenter-policy`** to the role.

    ![Attach Policy](screenshots/step-25-attach-policy.png)

26. Named the role **`datacenter-role`** and created it.

    ![Create Role Final](screenshots/step-26-create-role-final.png)

27. Verified the IAM role was created successfully.

    ![Role Created](screenshots/step-27-role-created.png)

---

### Attach IAM Role and Test S3 Access

28. Modified IAM role of **`datacenter-ec2`**.

    ![Modify IAM Role](screenshots/step-28-modify-iam-role.png)

29. Attached **`datacenter-role`** to the EC2 instance.

    ![Attach Role](screenshots/step-29-attach-role.png)

30. Created a file `nirmit.txt` and uploaded it to the S3 bucket.

    ![Upload File](screenshots/step-30-upload-file.png)

31. Verified the uploaded file exists in the S3 bucket.

    ![Verify File](screenshots/step-31-verify-file.png)

---

## Verification
The following confirms successful task completion:

- Passwordless SSH access to EC2

  ![SSH Success](screenshots/step-12-ssh-success.png)

- Private S3 bucket created successfully

  ![S3 Created](screenshots/step-17-s3-created.png)

- IAM role attached to EC2

  ![Role Created](screenshots/step-29-attach-role.png)

- File upload and listing from S3 successful

  ![Upload File](screenshots/step-30-upload-file.png)

---

## Outcome
The EC2 instance successfully accessed a **private S3 bucket** using an **IAM role**, without storing credentials. Secure SSH access was configured, and S3 file operations were verified.

---

## Learnings
- IAM roles are the safest way to grant AWS access to EC2
- Private S3 buckets can be accessed securely
- SSH key authentication improves server security
- Least-privilege policies reduce attack surface
- EC2-to-S3 integration is a core AWS pattern

---

**Status:** Completed 
