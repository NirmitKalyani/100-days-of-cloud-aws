# Day 11 – Attach Elastic Network Interface to EC2 (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on attaching an existing Elastic Network Interface (ENI) to an existing Amazon EC2 instance. ENIs enable flexible and advanced networking configurations in AWS.

The objective was to attach a specified ENI to a running EC2 instance and verify that the attachment was successful.

---

## Concept
An Elastic Network Interface (ENI) is a virtual network interface that can be attached
to an EC2 instance. ENIs allow advanced networking features such as multiple private IP
addresses, traffic isolation, and flexible network configurations independent of the
instance lifecycle.

---

## Real-World Use Case
Elastic Network Interfaces are commonly used to:
- Implement multi-homed EC2 instances with multiple network interfaces
- Separate network traffic for different applications or environments
- Support high-availability and failover architectures
- Retain network configurations while moving interfaces between instances

---

## Requirements
- **Region:** us-east-1
- **EC2 Instance:** `datacenter-ec2`
- **Elastic Network Interface:** `datacenter-eni`
- **Condition:** ENI status must be **attached** before submission
- **Note:** Instance initialization must be completed

---

## AWS Services Used
- **Amazon EC2**
  - EC2 Instances
  - Elastic Network Interfaces (ENI)

---

## Verification
The following screenshots confirm successful completion of the task:

- **EC2 instance list showing instance is running and associated network interface:**  
  
  ![EC2 Instance List Screenshot](screenshots/ec2-instance-list.png)

- **Network interface details showing attached status and associated instance:**  
  
  ![Network Interface Attached Screenshot](screenshots/network-interface-attached.png)

---

## Outcome
The Elastic Network Interface `datacenter-eni` was successfully attached to the EC2 instance `datacenter-ec2`. The network interface status shows **attached**, confirming all task requirements were fulfilled.

---

## Learnings
- Elastic Network Interfaces can be attached or detached independently of EC2 instances.
- ENIs enable advanced networking features such as multiple private IPs and network isolation.
- EC2 instance initialization must complete before attaching additional network interfaces.
- Attachment status can be verified from the EC2 → Network Interfaces section.

---

**Status:** Completed
