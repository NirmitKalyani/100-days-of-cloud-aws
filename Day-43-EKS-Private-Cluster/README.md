# Day 43 – Creating a Private Amazon EKS Cluster with Custom Configuration

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on provisioning a secure and highly available **Amazon EKS (Elastic Kubernetes Service)** cluster.

The Nautilus DevOps team is preparing infrastructure for a Kubernetes-based application. The requirement was to create an EKS cluster using the **latest stable Kubernetes version**, restrict external exposure by keeping the **cluster endpoint private**, and deploy the cluster in the **default VPC** across multiple availability zones for high availability.

---

## Concept
This task highlights how **Amazon EKS** enables organizations to run Kubernetes clusters securely and reliably without managing the control plane infrastructure.

Key concepts involved:
- Amazon EKS cluster creation
- Custom cluster configuration
- IAM roles for EKS
- Kubernetes version selection
- Private cluster endpoint access
- Multi-AZ high availability
- Managed EKS add-ons

---

## Real-World Use Case
In real-world production environments:
- Kubernetes control planes are often kept private for security reasons
- Clusters are deployed across multiple availability zones for fault tolerance
- IAM roles are used to securely grant permissions to AWS-managed services

This setup reflects **enterprise-grade Kubernetes deployments** where security, scalability, and reliability are critical.

---

## Requirements
- **Cluster Name:** `xfusion-eks`
- **Cluster Configuration:** Custom
- **IAM Role:** `eksClusterRole`
- **Kubernetes Version:** 1.30
- **VPC:** Default VPC
- **Availability Zones:** a, b, c
- **Cluster Endpoint Access:** Private
- **EKS Auto Mode:** Disabled

---

## AWS Services Used
- Amazon Elastic Kubernetes Service (EKS)
- AWS Identity and Access Management (IAM)

---

## Steps Performed

### 1. Navigated to Amazon EKS
Opened the AWS Management Console and navigated to **Elastic Kubernetes Service (EKS)**.

![Go to EKS](screenshots/ss1-go-to-eks.png)

---

### 2. Initiated Cluster Creation
Navigated to **Clusters** and clicked on **Create cluster**.

![Create Cluster](screenshots/ss2-create-cluster.png)

---

### 3. Selected Custom Configuration
Chose **Custom configuration**, disabled **EKS Auto Mode**, and provided the cluster name as `xfusion-eks`.

![Custom Configuration](screenshots/ss3-custom-config.png)

---

### 4. Started IAM Role Creation
Clicked on **Create IAM role** to define permissions for the EKS cluster.

![Create IAM Role](screenshots/ss4-create-iam-role.png)

---

### 5. Selected Trusted Entity
Selected **AWS Service** as the trusted entity and chose **EKS** with the use case **EKS-Cluster**.

![Trusted Entity](screenshots/ss5-trusted-entity.png)

---

### 6. Attached Required Policy
Attached the **AmazonEKSClusterPolicy** permission policy to the role.

![Attach Policy](screenshots/ss6-attach-policy.png)

---

### 7. Named the IAM Role
Provided the role name as `eksClusterRole` along with a suitable description.

![Role Name](screenshots/ss7-role-name.png)

---

### 8. Verified IAM Role Creation
Confirmed that the IAM role `eksClusterRole` was created successfully.

![Role Created](screenshots/ss8-role-created.png)

---

### 9. Selected Cluster IAM Role
Returned to the EKS cluster creation wizard and selected **eksClusterRole** as the cluster IAM role.

![Select IAM Role](screenshots/ss9-select-role.png)

---

### 10. Selected Kubernetes Version
Chose **Kubernetes version 1.30**, as mentioned in the instructions.

![Kubernetes Version](screenshots/ss10-k8s-version.png)

---

### 11. Configured Network Settings
Under network configuration, retained only the subnets belonging to **availability zones a, b, and c**.

![Network Configuration](screenshots/ss11-network-config.png)

---

### 12. Set Cluster Endpoint Access
Configured the cluster endpoint access to **Private** to restrict public exposure.

![Private Endpoint](screenshots/ss12-private-endpoint.png)

---

### 13. Configured Add-ons
Deselected all add-ons except:
- kube-proxy
- CoreDNS
- AWS VPC CNI

![Add-ons](screenshots/ss13-addons.png)

---

### 14. Reviewed and Created Cluster
Reviewed all cluster details and initiated cluster creation.

![Review Cluster](screenshots/ss14-review-cluster.png)

---

### 15. Verified Cluster Status
Confirmed that the EKS cluster `xfusion-eks` was created successfully and reached the **Active** state.

![Cluster Active](screenshots/ss15-cluster-active.png)

---

## Verification
The following validations confirm successful task completion:

- EKS cluster `xfusion-eks` was created successfully

  ![Cluster Active](screenshots/ss15-cluster-active.png)

- Cluster endpoint access was set to **Private**

  ![Private Endpoint](screenshots/ss12-private-endpoint.png)

- Cluster was deployed across multiple availability zones

  ![Network Configuration](screenshots/ss11-network-config.png)

- Correct IAM role `eksClusterRole` was attached to the cluster

  ![Select IAM Role](screenshots/ss9-select-role.png)

---

## Outcome
The task successfully provisioned a **secure, private, and highly available Amazon EKS cluster** using a custom configuration, meeting all internal security and scalability requirements.

---

## Learnings
- Custom EKS configuration provides greater control over security settings
- Private cluster endpoints reduce external attack surfaces
- IAM roles are mandatory for EKS control plane operations
- Multi-AZ deployments improve fault tolerance
- Choosing the latest Kubernetes version ensures access to new features and security updates

---

**Status:** Completed
