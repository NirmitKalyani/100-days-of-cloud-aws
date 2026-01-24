# Day 27 – Create Public VPC, Subnet, and EC2 Instance (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on setting up a **public VPC** to host internet-facing resources.

The objective was to create a **public VPC** named **`datacenter-pub-vpc`**, a **public subnet** with automatic public IP assignment, and launch an **EC2 instance** named **`datacenter-pub-ec2`** with **SSH access enabled**.

---

## Concept
A **Virtual Private Cloud (VPC)** provides a logically isolated network in AWS.  
To make resources publicly accessible, the VPC must include:
- A **public subnet**
- **Automatic public IP assignment**
- An **Internet Gateway**
- Correct **route table and security group** configuration

This enables EC2 instances to communicate with the internet securely.

---

## Real-World Use Case
Public VPC setups are commonly used to:
- Host public-facing applications
- Enable SSH access for administrators
- Deploy web servers and APIs
- Separate public and private infrastructure
- Build scalable network architectures

---

## Requirements
- **VPC name:** `datacenter-pub-vpc`
- **Subnet name:** `datacenter-pub-subnet`
- **Subnet type:** Public
- **Auto-assign public IP:** Enabled
- **EC2 instance name:** `datacenter-pub-ec2`
- **Instance type:** `t2.micro`
- **Inbound access:** SSH
- **Port:** 22
- **Source:** `0.0.0.0/0`

---

## AWS Services Used
- Amazon VPC
- Amazon EC2
- Internet Gateway
- Route Tables
- EC2 Security Groups

---

## Steps Performed

1. Navigated to **Services → VPC** from the AWS Management Console.

   ![Open VPC](screenshots/step-1-open-vpc.png)

2. Created a new **VPC** named **`datacenter-pub-vpc`**.

   ![Create VPC](screenshots/step-2-create-vpc.png)

3. Created a subnet named **`datacenter-pub-subnet`** under the VPC.

   ![Create Subnet](screenshots/step-3-name-subnet.png) 

   ![Create Subnet](screenshots/step-3-create-subnet.png)

4. Enabled **auto-assign public IPv4 address** for the subnet.

   ![Enable Auto Assign Public IP](screenshots/step-4-enable-auto-public-ip.png)

5. Created and attached an **Internet Gateway** to the VPC.

   ![Create Internet Gateway](screenshots/step-5-create-igw.png)

   ![Attach Internet Gateway](screenshots/step-5-attach-igw.png)

6. Updated the **route table** to allow internet traffic.

   ![Update Route Table](screenshots/step-6-update-route-table.png)

   ![Verified Updated Route Table](screenshots/step-6-route-table-updated.png) 

7. Navigated to **Services → EC2** from the AWS Management Console.

   ![Open EC2](screenshots/step-7-open-ec2.png)

8. Launched an EC2 instance with the following configuration:

   - **Name:** `datacenter-pub-ec2`
   - **AMI:** Ubuntu

   ![Name EC2](screenshots/step-8-name-ec2-instacne-and-select-ami.png) 

   - **Instance type:** `t2.micro`
   - **Key pair:** Selected Proceed without a keypair

   ![Select EC2 instance type](screenshots/step-8-instance-type-and-key-pair.png) 

   - **VPC:** `datacenter-pub-vpc`
   - **Subnet:** `datacenter-pub-subnet`

   ![Configure VPC and Subnet for EC2](screenshots/step-8-configure-vpc-and-subnet.png)

9. Configured the **security group** to allow SSH access:

   - **Type:** SSH  
   - **Port:** 22  
   - **Source:** `0.0.0.0/0`

   ![Configure Security Group](screenshots/step-9-configure-sg.png)

10.  Verified that the EC2 instance was in the **Running** state.

   ![EC2 Running](screenshots/step-10-ec2-running.png)

---

## Verification
The following screenshots confirm successful completion of the task:

- Public VPC **`datacenter-pub-vpc`** created successfully  
  ![VPC Created](screenshots/verification-vpc-created.png)

- Public subnet with auto-assign public IP enabled  
  ![Public Subnet Verified](screenshots/verification-public-subnet.png)

- EC2 instance **`datacenter-pub-ec2`** running with public IP  
  ![EC2 Public IP](screenshots/verification-ec2-public-ip.png)

- SSH (port 22) allowed in security group  
  ![SSH Rule Verified](screenshots/verification-ssh-rule.png)

---

## Outcome
A public VPC infrastructure was successfully created with a public subnet and internet access.  
The EC2 instance **`datacenter-pub-ec2`** is publicly accessible via **SSH**, enabling deployment of public-facing applications.

---

## Learnings
- Public subnets require Internet Gateway and route table configuration
- Auto-assign public IP is essential for internet access
- Security groups control inbound connectivity
- SSH access should be tightly controlled in real environments
- Proper VPC design is critical for scalable architectures

---

**Status:** Completed
