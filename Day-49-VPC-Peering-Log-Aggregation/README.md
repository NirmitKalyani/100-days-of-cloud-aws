# Day 49 – Secure Log Aggregation Across VPCs  

## Task Overview  

As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on designing a secure and automated log aggregation pipeline across two VPCs.

The devops DevOps team required a setup that:

- Transfers logs from a private EC2 instance
- Securely sends them to a public EC2 instance
- Pushes those logs into a private S3 bucket
- Uses VPC Peering for secure communication
- Uses IAM roles instead of access keys
- Automates log transfer using cron jobs

---

## Architecture  

Private VPC (Existing)
- VPC: `devops-priv-vpc`
- Subnet: `devops-priv-subnet`
- Route Table: `devops-priv-rt`
- EC2: `devops-priv-ec2`

Public VPC (Created)
- VPC: `devops-pub-vpc`
- Subnet: `devops-pub-subnet`
- Route Table: `devops-pub-rt`
- EC2: `devops-pub-ec2`

Storage
- S3 Bucket: `devops-s3-logs-4702`

Peering
- `devops-vpc-peering`

---

# Steps Performed  

---

## 1. Public VPC Creation  

Created VPC:

- Name: `devops-pub-vpc`
- Proper CIDR block assigned

![Public VPC Created](screenshots/01-public-vpc-created.png)

---

## 2. Public Subnet Creation  

Created subnet:

- Name: `devops-pub-subnet`
- Associated with public VPC

![Public Subnet](screenshots/02-public-subnet.png)

![Public Subnet](screenshots/02-enable-auto-assign-ip.png)

---

## 3. Internet Gateway Configuration  

- Created Internet Gateway
- Attached to `devops-pub-vpc`
- Added route `0.0.0.0/0` to route table

![Internet Gateway](screenshots/04-internet-gateway.png)

![Internet Gateway](screenshots/04-internet-gateway-attached.png)

---

## 4. Route Table Creation  

Created route table:

- Name: `devops-pub-rt`
- Associated with public subnet

![Public Route Table](screenshots/03-public-route-table-01.png)

![Public Route Table](screenshots/03-public-route-table-02.png)

![Public Route Table](screenshots/03-public-route-table-03.png)

---

## 5. Public EC2 Launch  

Launched EC2 instance:

- Name: `devops-pub-ec2`
- Subnet: `devops-pub-subnet`
- Key Pair: `devops-key.pem`
- Public IP enabled

![Public EC2 Instance](screenshots/05-public-ec2-01.png)

![Public EC2 Instance](screenshots/05-public-ec2-02.png)

---

## 6. Security Group Configuration  

Configured security groups to allow:

- SSH access
- Internal communication from peer VPC CIDR

![Security Group Rules](screenshots/06-security-group.png)

---

## 7. S3 Bucket Creation  

Created private bucket:

- Name: `devops-s3-logs-4702`
- Kept other settings default

![S3 Bucket Created](screenshots/07-s3-bucket.png)

---

## 8. IAM Role Creation  

Created IAM Role:

- Name: `devops-s3-role`
- Policy: Select `S3FullAccess` Policy

![IAM Role Created](screenshots/08-iam-role-01.png)

![IAM Role Created](screenshots/08-iam-role-02.png)

![IAM Role Created](screenshots/08-iam-role-03.png)

---

## 9. Attach IAM Role to EC2  

Attached `devops-s3-role` to `devops-pub-ec2`.

![Attach IAM Role](screenshots/09-attach-role.png)

---

## 10. VPC Peering Creation  

Created peering connection:

- Name: `devops-vpc-peering`
- Between private and public VPC

![Peering Created](screenshots/10-peering-created.png)

---

## 11. Peering Accepted  

Accepted Peering connection request

![Peering Active](screenshots/11-peering-active.png)

---

## 12. Update Private Route Table  

Modified:

- `devops-priv-rt`
- Added route to public VPC CIDR via peering connection

![Private Route Update](screenshots/12-private-route-updated-01.png)

![Private Route Update](screenshots/12-private-route-updated-02.png)

---

## 13. Update Public Route Table  

Modified:

- `devops-pub-rt`
- Added route to private VPC CIDR via peering connection

![Public Route Update](screenshots/13-public-route-updated-01.png)

![Public Route Update](screenshots/13-public-route-updated-02.png)

---

## 14. Connectivity Test  

Verified connectivity between:

- `devops-priv-ec2`
- `devops-pub-ec2`

Used private IP communication.

![Connectivity Test](screenshots/14-connectivity-test.png)

---

## 15. Cron Job on Private Instance  

Configured cron job:

- Transfers `/var/log/boots.log`
- Uses SCP or rsync
- Runs periodically

![Private Cron Job](screenshots/15-private-cron-01.png)

![Private Cron Job](screenshots/15-private-cron-02.png)

---

## 16. Cron Job on Public Instance  

Installed and enabled cronie on public instance

Configured cron job:

- Uploads file to S3 bucket
- Path:  
  `devops-priv-vpc/boot/boots.log`

![Public Cron Job](screenshots/16-public-cron-01.png)

![Public Cron Job](screenshots/16-public-cron-02.png)

![Public Cron Job](screenshots/16-public-cron-03.png)

![Public Cron Job](screenshots/16-public-cron-04.png)

---

## 17. S3 Upload Verification  

Verified file exists in S3:

Bucket:
`devops-s3-logs-4702`

Path:
`devops-priv-vpc/boot/boots.log`

![S3 Object Verified](screenshots/17-s3-object.png)

---

# Verification  

- Public VPC created successfully  

![Verification – Public VPC](screenshots/18-verify-public-vpc.png)

- Internet access configured correctly  

![Verification – Internet Route](screenshots/19-verify-igw-route.png)

- EC2 instance launched in public subnet  

![Verification – Public EC2 Running](screenshots/20-verify-public-ec2.png)

- IAM role attached correctly  

![Verification – IAM Attached](screenshots/21-verify-iam-attachment.png)

- VPC Peering status Active  

![Verification – Peering Active](screenshots/22-verify-peering.png)

- Route tables updated properly  

![Verification – Route Tables](screenshots/23-verify-route-table-01.png)

![Verification – Route Tables](screenshots/23-verify-route-table-02.png)

- Object stored in required path  

![Verification – S3 Object](screenshots/24-verify-s3-object.png)

---

# Outcome  

Successfully implemented:

- Secure cross-VPC log transfer
- Automated cron-based file movement
- IAM-based secure S3 upload
- Centralized durable log storage

This architecture reflects a real-world secure log aggregation pipeline.

---

# Learnings  

- VPC Peering requires explicit routing on both sides  
- IAM roles eliminate need for access keys  
- Route tables control traffic flow strictly  
- Cron jobs provide simple automation  
- S3 is ideal for centralized log storage  

---

**Status:** Completed  
