# Day 21 – Launch EC2 Instance with Elastic IP (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on launching an **EC2 instance** and associating it with an **Elastic IP (EIP)** to ensure a stable and consistent public IP address.

The objective was to create an EC2 instance named **`xfusion-ec2`** using a Linux AMI and associate it with an Elastic IP named **`xfusion-eip`**.

---

## Concept
An **Elastic IP (EIP)** is a static, public IPv4 address designed for dynamic cloud computing. Unlike the default public IP of an EC2 instance (which can change on stop/start), an Elastic IP remains constant until explicitly released.

Associating an Elastic IP with an EC2 instance ensures uninterrupted access to applications hosted on the instance.

---

## Real-World Use Case
Elastic IPs are commonly used to:
- Host public-facing applications and APIs
- Ensure stable IPs for DNS mapping
- Avoid IP changes during instance restarts
- Provide reliable access points for production workloads

---

## Requirements
- **EC2 Instance name:** `xfusion-ec2`
- **AMI:** Any Linux AMI (Ubuntu used)
- **Instance type:** `t2.micro`
- **Elastic IP name:** `xfusion-eip`
- **Action:** Associate Elastic IP with EC2 instance
- **AWS Services:** EC2

---

## AWS Services Used
- Amazon EC2
- Elastic IP (EC2 Networking)

---

## Steps Performed
1. Navigated to **Services → EC2**.

   ![Open EC2](screenshots/step-1-open-ec2.png)

2. Clicked **Launch instance** and Added the instance name tag as **`xfusion-ec2`**.

   ![Name Instance](screenshots/step-2-name-instance.png)

3. Selected a Linux AMI (Ubuntu).

   ![Select AMI](screenshots/step-3-select-ami.png)

4. Chose instance type **t2.micro** and configured basic instance settings.

   ![Instance Type](screenshots/step-4-instance-type.png)

5. Navigated to **Elastic IPs** and clicked on allocate Elastic IP address.

   ![Allocate Elastic IP](screenshots/step-5-allocate-eip.png)

6. Added a name tag **`xfusion-eip`** to the Elastic IP for identification.

   ![Name Elastic IP](screenshots/step-6-name-eip.png)

7. Associated the Elastic IP with the EC2 instance **`xfusion-ec2`**.

   ![Associate EIP](screenshots/step-7-associate-eip.png)

---

## Verification
The following screenshots confirm successful completion of the task:

- EC2 instance list showing `xfusion-ec2` in running state:

  ![EC2 Verification](screenshots/verification-ec2-running.png)

- Elastic IP associated with the instance:

  ![EIP Verification](screenshots/verification-eip-associated.png)

---

## Outcome
The EC2 instance **`xfusion-ec2`** was successfully launched using a Linux AMI and associated with the Elastic IP **`xfusion-eip`**, providing a stable and consistent public IP address for application access.

---

## Learnings
- Default public IPs change when EC2 instances are stopped and started.
- Elastic IPs provide a static public IP for reliable access.
- Elastic IPs must be explicitly released to avoid unnecessary charges.
- Tagging resources improves visibility and management.
- Stable IPs are critical for production and externally accessible applications.

---

**Status:** Completed
