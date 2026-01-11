# Day 05 – Create EBS Volume (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on creating an Amazon Elastic Block Store (EBS) volume. EBS volumes provide persistent block storage for EC2 instances and are a fundamental component of AWS compute infrastructure.

The objective was to create an EBS volume with specific size and type requirements and ensure proper naming for easy identification.

---

## Concept
Amazon Elastic Block Store (EBS) provides persistent block storage that can be used
with EC2 instances. EBS volumes are independent resources that retain data even
when instances are stopped or terminated.

---

## Real-World Use Case
EBS volumes are commonly used to:
- Store application data separately from the OS
- Persist databases and logs on EC2 instances
- Increase storage capacity without recreating instances
- Support backup and snapshot-based recovery strategies

---

## Requirements
- **Volume name:** `nautilus-volume`
- **Volume type:** `gp3`
- **Volume size:** `2 GiB`

---

## AWS Services Used
- **Amazon EC2**
  - Elastic Block Store (EBS)

---

## Steps Performed
1. Navigated to **EC2 → Elastic Block Store → Volumes**.
2. Created a new EBS volume with:
   - Name: `nautilus-volume`
   - Volume type: `gp3`
   - Size: `2 GiB`
3. Verified that the volume was created successfully and marked as **Available**.

---

## Verification
The following screenshots confirm successful completion of the task:

- **EBS volume list showing name, type, and size:**  
  
  ![EBS Volume List Screenshot](screenshots/ebs-volume-list.png)

- **EBS volume details view confirming configuration:**  
  
  ![EBS Volume Details Screenshot](screenshots/ebs-volume-details.png)

---

## Outcome
The EBS volume `nautilus-volume` was successfully created with the required specifications, fulfilling all task constraints.

---

## Learnings
- EBS volumes provide persistent block storage independent of EC2 instance lifecycle.
- Volume type selection (gp3) affects performance and cost.
- EBS volumes are created within a specific Availability Zone.
- Proper naming and verification simplify resource management.

---

**Status:** Completed
