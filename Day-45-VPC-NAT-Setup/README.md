# Day 45 – Enabling Internet Access for Private EC2 Using NAT Gateway

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on enabling **internet access for an EC2 instance running inside a private subnet** using a **NAT Gateway**.

The Nautilus DevOps team needed to configure networking components so that a private EC2 instance could upload a test file to a public S3 bucket once outbound internet access was established.

The EC2 instance had a cron job configured to upload a test file to:

**S3 Bucket:** datacenter-nat-29614

Once NAT configuration was completed, the instance would automatically upload the test file.

---

## Concept
This task demonstrates core AWS networking concepts:

- Public vs Private Subnets
- Internet Gateway (IGW)
- NAT Gateway
- Elastic IP (EIP)
- Route Tables
- Outbound Internet Access from Private Subnets
- VPC Resource Mapping

A NAT Gateway allows instances in a private subnet to initiate outbound internet traffic while preventing inbound internet access.

---

## Real-World Use Case
In production environments:
- Application servers run in private subnets for security.
- Only outbound internet access is required (e.g., updates, S3 uploads, API calls).
- Direct internet exposure must be avoided.
- NAT Gateway ensures secure outbound connectivity.

This setup reflects a secure, production-ready VPC architecture widely used in real-world AWS deployments.

---

## Requirements

### Already Available:
- **VPC:** datacenter-priv-vpc
- **Private Subnet:** datacenter-priv-subnet
- **EC2 Instance:** datacenter-priv-ec2
- **S3 Bucket:** datacenter-nat-29614

### To Configure:
- **Public Subnet:** datacenter-pub-subnet
- **Internet Gateway:** datacenter-igw
- **Public Route Table:** datacenter-pub-rt
- **Elastic IP:** datacenter-eip
- **NAT Gateway:** datacenter-natgw

---

## AWS Services Used
- Amazon VPC
- Amazon EC2
- Internet Gateway
- NAT Gateway
- Elastic IP
- Route Tables
- Amazon S3

---

## Steps Performed

### 1–2. Verified Existing EC2 Instance
Navigated to EC2 and confirmed that `datacenter-priv-ec2` was running inside `datacenter-priv-vpc` and `datacenter-priv-subnet`.

![Go to EC2](screenshots/ss1.png)

![Verify EC2](screenshots/ss2.png)

---

### 3–7. Created Public Subnet
Checked the VPC CIDR and created a new public subnet:

- Name: `datacenter-pub-subnet`
- CIDR: 10.2.0.0/24
- VPC: `datacenter-priv-vpc`

Verified successful creation.

![Check VPC](screenshots/ss3.png)

![Create Subnet](screenshots/ss4.png)

![Select VPC](screenshots/ss5.png)

![Subnet Details](screenshots/ss6.png)

![Subnet Created](screenshots/ss7.png)

---

### 8–12. Created Public Route Table
Created a new route table:

- Name: `datacenter-pub-rt`
- VPC: `datacenter-priv-vpc`

Associated it with datacenter-pub-subnet.

![Create Route Table](screenshots/ss8.png)

![Route Table Name](screenshots/ss9.png)

![Route Table Created](screenshots/ss10.png)

![Edit Subnet Association](screenshots/ss11.png)

![Association Verified](screenshots/ss12.png)

---

### 13–17. Created and Attached Internet Gateway
Created an Internet Gateway: `datacenter-igw` and attached it to `datacenter-priv-vpc`.

![Create IGW](screenshots/ss13.png)

![Name IGW](screenshots/ss14.png)

![Attach IGW](screenshots/ss15.png)

![Select VPC](screenshots/ss16.png)

![IGW Attached](screenshots/ss17.png)

---

### 18–20. Updated Public Route Table
Added route:

- Destination: 0.0.0.0/0
- Target: `datacenter-igw`

This enabled internet access for the public subnet.

![Edit Routes](screenshots/ss18.png)

![Add Route](screenshots/ss19.png)

![Route Verified](screenshots/ss20.png)

---

### 21–23. Allocated Elastic IP
Allocated an Elastic IP:

- Name: `datacenter-eip`
- Region: `us-east-1`

Verified successful allocation.

![Allocate EIP](screenshots/ss21.png)

![EIP Details](screenshots/ss22.png)

![EIP Created](screenshots/ss23.png)

---

### 24–26. Created NAT Gateway
Created NAT Gateway:

- Name: `datacenter-natgw`
- VPC: `datacenter-priv-vpc`
- Subnet: `datacenter-pub-subnet`
- Elastic IP: `datacenter-eip`

Verified NAT Gateway was available.

![Create NAT Gateway](screenshots/ss24.png)

![NAT Details](screenshots/ss25.png)

![NAT Created](screenshots/ss26.png)

---

### 27–31. Updated Private Route Table
Associated the private subnet with the NAT route table and added route:

- Destination: 0.0.0.0/0
- Target: `datacenter-natgw`

Verified route was successfully added.

![Associate Private Subnet](screenshots/ss27.png)

![Association Verified](screenshots/ss28.png)

![Edit Routes](screenshots/ss29.png)

![Add NAT Route](screenshots/ss30.png)

![Route Verified](screenshots/ss31.png)

---

### 32. Verified VPC Resource Mapping
Used VPC Resource Map to confirm:

- IGW attached
- NAT Gateway in public subnet
- Proper route table associations
- Correct routing configuration

![Resource Map](screenshots/ss32.png)

---

## Verification
The following validations confirm successful task completion:

- Navigated to Amazon S3 and confirmed that the test file (datacenter-test.txt) was successfully uploaded to `datacenter-nat-29614`

- This confirmed that the private EC2 instance had outbound internet access via NAT Gateway.

![Go to S3](screenshots/ss33.png)

![File Uploaded](screenshots/ss34.png)

---

## Outcome
Successfully configured a **secure VPC networking architecture** where:

- Private EC2 instances do not have direct internet exposure.
- Outbound internet access is enabled via NAT Gateway.
- Public subnet routes through Internet Gateway.
- Private subnet routes through NAT Gateway.
- EC2 cron job successfully uploaded file to S3.

This mirrors a secure production-grade VPC setup used in real-world AWS environments.

---

## Learnings
- NAT Gateway enables outbound internet access for private subnets.
- Internet Gateway is required for public subnet connectivity.
- Route tables control traffic flow inside a VPC.
- Elastic IP is required for NAT Gateway.
- Proper subnet association is critical for routing.
- Always verify architecture using VPC Resource Map.
- Real-world architectures separate public and private workloads for security.

---

**Status:** Completed
