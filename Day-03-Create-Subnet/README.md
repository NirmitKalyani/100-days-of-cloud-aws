# Day 03 – Create Subnet (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on creating a subnet inside an existing Virtual Private Cloud (VPC). The objective is to understand subnet creation, CIDR planning, and resource placement within a specific AWS region.

The task required creating a single subnet under the **default VPC** while ensuring no CIDR conflicts with existing subnets.

---

## Requirements
- **Subnet name:** `nautilus-subnet`
- **VPC:** Default VPC
- **AWS Region:** `us-east-1` (N. Virginia)

---

## AWS Services Used
- **Amazon VPC**
  - Subnets

---

## Steps Performed
1. Switched AWS Console region to **N. Virginia (us-east-1)**.
2. Navigated to **VPC → Subnets**.
3. Selected the **default VPC**.
4. Created a new subnet with:
   - Name: `nautilus-subnet`
   - An available IPv4 CIDR block that did not overlap with existing subnets
   - Availability Zone within `us-east-1`
5. Verified that the subnet was created successfully and marked as **Available**.

---

## Verification
The following screenshots confirm successful completion of the task:

- **Subnet listing showing name, VPC, and CIDR block:**  
  `screenshots/subnet-list.png`

- **Subnet details view confirming default VPC and availability zone:**  
  `screenshots/subnet-details.png`

---

## Outcome
The subnet `nautilus-subnet` was successfully created under the default VPC in the `us-east-1` region, fulfilling all task requirements without CIDR overlap.

---

## Learnings
- Subnets must use **non-overlapping IPv4 CIDR blocks** within a VPC.
- Default VPCs often already contain multiple subnets, requiring careful CIDR selection.
- Subnets are tied to a **specific Availability Zone** within a region.
- Proper CIDR planning is essential in real-world cloud networking scenarios.

---

**Status:** Completed
