# Day 35 – Private Amazon RDS (MySQL) Setup and EC2 Connectivity

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on creating a **private Amazon RDS MySQL instance** and integrating it with an existing **EC2 instance**.

The objective was to provision a **secure, non-public RDS database**, configure **security groups for controlled access**, enable **password-less SSH** between hosts, deploy a PHP application, and verify successful **EC2 → RDS connectivity** via a browser.

---

## Concept
Amazon RDS provides a fully managed relational database service that simplifies database administration while improving security and reliability. Keeping the RDS instance private and allowing access only from trusted EC2 instances is a **recommended production best practice**.

Key concepts involved:
- Amazon RDS (MySQL)
- Private database deployment
- Security Groups and inbound rules
- EC2 to RDS connectivity
- SSH key-based authentication
- PHP–MySQL integration

---

## Real-World Use Case
This architecture closely resembles real-world cloud applications where:
- Databases are isolated from public access
- Applications run on EC2 instances
- Network access is tightly controlled using security groups
- SSH access is secured using key pairs
- Backend services communicate securely within a VPC

---

## Requirements
- **RDS Instance Identifier:** `datacenter-rds`
- **Database Engine:** MySQL `8.4.5`
- **Instance Class:** `db.t3.micro`
- **Storage Type:** `gp2`
- **Allocated Storage:** `5 GiB`
- **Initial Database Name:** `datacenter_db`
- **Master Username:** `datacenter_admin`
- **Public Access:** Disabled
- **EC2 Instance Name:** `datacenter-ec2`
- **Allowed Ports:** `22`, `80`, `3306`

---

## AWS Services Used
- Amazon RDS
- Amazon EC2
- Amazon VPC
- Security Groups

---

## Steps Performed

### RDS Creation

1. Opened the Amazon RDS service from the AWS console.

   ![Open RDS](screenshots/ss1.png)

2. Clicked on **Create database**.

   ![Create Database](screenshots/ss2.png)

3. Selected **Full Configuration** as the database creation method.

   ![DB Creation Method](screenshots/ss3.png)

4. Selected **MySQL** as the engine and version **8.4.5**.

   ![Engine Options](screenshots/ss4.png)

5. Chose the **Free Tier** template and **Single-AZ** deployment.

   ![Template Selection](screenshots/ss5.png)

6. Configured database settings:
   - DB instance identifier: `datacenter-rds`
   - Master username: `datacenter_admin`
   - Enabled auto-generated password

   ![DB Identifier and Credentials](screenshots/ss6.png)

7. Selected **Burstable classes** and instance type **db.t3.micro**.

   ![Instance Class](screenshots/ss7.png)

8. Configured storage:
   - Storage type: `gp2`
   - Allocated storage: `5 GiB`

   ![Storage Configuration](screenshots/ss8.png)

9. Disabled public access and created a new security group named `datacenter-db-sg`.

   ![Public Access Disabled](screenshots/ss9.png)

10. Under additional configuration, specified the initial database name as `datacenter_db`.

    ![Initial Database Name](screenshots/ss10.png)

---

### Security Group Configuration

11. Navigated to the **Security Groups** service.

    ![Open Security Groups](screenshots/ss11.png)

12. Selected the default security group attached to the EC2 instance and edited inbound rules.

    ![Edit EC2 Security Group](screenshots/ss12.png)

13. Added inbound rules to allow:
    - SSH (port 22)
    - HTTP (port 80)

    ![Add SSH and HTTP Rules](screenshots/ss13.png)

14. Verified that the inbound rules were successfully added.

    ![Verify EC2 SG Rules](screenshots/ss14.png)

15. Selected the RDS security group `datacenter-db-sg` and edited inbound rules.

    ![Edit RDS Security Group](screenshots/ss15.png)

16. Added a **MySQL/Aurora (3306)** inbound rule with the EC2 security group as the source.

    ![Add MySQL Rule](screenshots/ss16.png)

17. Verified the inbound rule was added successfully.

    ![Verify RDS SG Rules](screenshots/ss17.png)

18. Confirmed that the RDS instance `datacenter-rds` was in the **Available** state.

    ![RDS Available](screenshots/ss18.png)

---

### SSH Key Setup and EC2 Access

19. On the `aws-client` host, generated SSH keys under `/root/.ssh`.

    ![Generate SSH Keys](screenshots/ss19.png)

20. Displayed and copied the public key.

    ![Copy Public Key](screenshots/ss20.png)

21. Connected to the EC2 instance using **EC2 Instance Connect**.

    ![EC2 Instance Connect](screenshots/ss21.png)

22. Added the public key to `/root/.ssh/authorized_keys` on the EC2 instance.

    ![Add Authorized Key](screenshots/ss22.png)

23. Verified the public key was saved correctly.

    ![Verify Authorized Key](screenshots/ss23.png)

24. Confirmed password-less SSH access from the `aws-client` to the EC2 instance.

    ![SSH Verification](screenshots/ss24.png)

---

### Application Deployment and Testing

25. Copied the `index.php` file from the `aws-client` host to the EC2 instance using `scp`.

    ![Copy PHP File](screenshots/ss25.png)

26. Removed the default `index.html` file and verified that `index.php` exists in `/var/www/html`.

    ![Verify PHP File](screenshots/ss26.png)

27. Edited `index.php` to update:
    - Database name
    - Username
    - Password
    - RDS endpoint

    ![Edit index.php](screenshots/ss27.png)

28. Verified the updated database configuration.

    ![Verify PHP Configuration](screenshots/ss28.png)

29. Tested the application locally using `curl`.

    ![Curl Test](screenshots/ss29.png)

30. Accessed the EC2 instance using its public IP and confirmed successful database connectivity.

    ![Browser Verification](screenshots/ss30.png)

---

## Verification
The following confirms successful completion of the task:

- RDS instance is private and in **Available** state
- EC2 instance can connect to RDS on port **3306**
- PHP application connects successfully to MySQL
- Browser displays **Connected successfully** message
  
  ![Browser Verification](screenshots/ss30.png)

---

## Outcome
A **private MySQL RDS instance** was successfully provisioned and securely connected to an EC2-hosted PHP application. The setup follows **production-grade cloud security practices** and demonstrates real-world AWS architecture.

---

## Key Takeaways
- Private RDS deployment improves security
- Security group references are preferred over IP-based rules
- EC2 and RDS integration is common in backend architectures
- SSH key-based access is more secure than password authentication
- End-to-end validation is critical in cloud deployments

---

## Status

**Status:** Completed
