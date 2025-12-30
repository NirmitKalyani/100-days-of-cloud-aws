# Day 02 – Create Security Group (EC2)

## Task Description
Create an EC2 security group as part of the AWS 100 Days of Cloud challenge.

### Requirements
- Region: us-east-1 (N. Virginia)
- Security Group Name: xfusion-sg
- Description: Security group for Nautilus App Servers
- Inbound Rules:
  - HTTP (TCP 80) from 0.0.0.0/0
  - SSH (TCP 22) from 0.0.0.0/0

## Steps Performed
1. Switched AWS region to **us-east-1 (N. Virginia)**.
2. Navigated to **EC2 → Security Groups**.
3. Created a new security group named **xfusion-sg**.
4. Added inbound rules for HTTP and SSH.
5. Verified the security group configuration.

## Screenshots
Screenshots related to the task execution are available in the `screenshots/` folder.

## Outcome
The security group was successfully created and the task was completed as part of Day 02 of the challenge.
