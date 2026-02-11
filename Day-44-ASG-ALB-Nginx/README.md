# Day 44 – Deploying a Highly Available Web Application Using ASG and ALB

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on building a **highly available and auto-scaled web application architecture** using AWS.

The DevOps team was required to configure:
- An EC2 Launch Template
- An Auto Scaling Group (ASG)
- An Application Load Balancer (ALB)

The EC2 instances needed to automatically install and run **Nginx**, while the Auto Scaling Group dynamically scaled instances based on CPU utilization. The Application Load Balancer was responsible for distributing incoming traffic across healthy instances.

---

## Concept
This task demonstrates core cloud architecture principles:

- Launch Templates for reusable EC2 configuration
- Auto Scaling Groups for elasticity and fault tolerance
- Target Tracking Scaling Policies
- Application Load Balancer for traffic distribution
- Health checks for high availability
- User Data scripts for automated instance configuration

---

## Real-World Use Case
In production environments:
- Traffic fluctuates dynamically
- Applications must remain highly available
- Instances must automatically recover from failures
- Infrastructure must scale based on demand

This architecture reflects a **standard production-ready web application deployment model** used across modern cloud-native systems.

---

## Requirements
- **Launch Template:** `xfusion-launch-template`
- **Instance Type:** t2.micro
- **AMI:** Amazon Linux
- **Security Group:** Allow HTTP (Port 80)
- **Auto Scaling Group:** `xfusion-asg`
  - Min: 1
  - Desired: 1
  - Max: 2
  - Target CPU Utilization: 50%
- **Target Group:** `xfusion-tg`
- **Load Balancer:** `xfusion-alb`
- **Listener Port:** 80
- **Health Checks:** Enabled

---

## AWS Services Used
- Amazon EC2
- EC2 Launch Templates
- Auto Scaling Groups
- Application Load Balancer (ALB)
- Target Groups
- Amazon VPC

---

## Steps Performed

### 1. Navigated to EC2
Opened the AWS Management Console and navigated to **EC2**.

![Go to EC2](screenshots/ss1-go-to-ec2.png)

---

### 2. Created Launch Template
Navigated to **Launch Templates** and clicked on **Create launch template**.

![Create Launch Template](screenshots/ss2-create-launch-template.png)

---

### 3. Named Launch Template
Provided the name `xfusion-launch-template`.

![Launch Template Name](screenshots/ss3-launch-template-name.png)

---

### 4. Selected AMI
Searched for Amazon Linux AMI in the catalog and selected the appropriate Amazon Linux image.

![Select AMI](screenshots/ss4-select-ami.png)

---

### 5. Selected Instance Type
Chose **t2.micro** as the instance type.

![Instance Type](screenshots/ss5-instance-type.png)

---

### 6. Configured Security Group
Created a new security group `xfusion-sg` allowing inbound HTTP traffic (Port 80) from Anywhere.

![Security Group](screenshots/ss6-security-group.png)

---

### 7. Added User Data Script
Added a User Data script to:
- Install Nginx
- Start the Nginx service
- Enable Nginx on boot

Created the launch template.

![User Data](screenshots/ss7-user-data.png)

---

### 8. Verified Launch Template Creation
Confirmed that `xfusion-launch-template` was created successfully.

![Launch Template Created](screenshots/ss8-launch-template-created.png)

---

### 9. Initiated Auto Scaling Group Creation
Navigated to **Auto Scaling Groups** and clicked on **Create Auto Scaling Group**.

![Create ASG](screenshots/ss9-create-asg.png)

---

### 10. Selected Launch Template
Named the ASG `xfusion-asg` and selected `xfusion-launch-template`.

![Select Launch Template](screenshots/ss10-select-launch-template.png)

---

### 11. Configured Network
Selected the default VPC and availability zones A, B, and C for high availability.

![Network Config](screenshots/ss11-network-config.png)

---

### 12. Configured Load Balancer
Selected to attach a new **Application Load Balancer**, named it `xfusion-alb`, and chose **internet-facing** scheme.

![Create ALB](screenshots/ss12-create-alb.png)

---

### 13. Created Target Group
Created a new target group named `xfusion-tg` listening on HTTP (Port 80).

![Create Target Group](screenshots/ss13-create-tg.png)

---

### 14. Configured Health Checks
Enabled additional ELB health checks and set health check grace period to 120 seconds.

![Health Checks](screenshots/ss14-health-check.png)

---

### 15. Configured Group Size
Set:
- Desired capacity: 1
- Minimum capacity: 1
- Maximum capacity: 2

![Group Size](screenshots/ss15-group-size.png)

---

### 16. Configured Scaling Policy
Selected **Target Tracking Scaling Policy**:
- Metric: Average CPU Utilization
- Target value: 50%
- Instance warmup: 120 seconds

![Scaling Policy](screenshots/ss16-scaling-policy.png)

---

### 17–18. Notifications and Tags
Skipped notifications and tags as they were not required.

![Notifications](screenshots/ss17-notifications.png)

![Tags](screenshots/ss18-tags.png)

---

### 19–21. Reviewed Configuration
Reviewed:
- Launch template settings
- Network configuration
- Load balancer configuration
- Scaling policies

Then created the Auto Scaling Group.

![Review Launch Template](screenshots/ss19-review-launch-template.png)

![Review Load Balancing](screenshots/ss20-review-load-balancing.png)

![Review Scaling](screenshots/ss21-review-scaling.png)

---

### 22. Verified ASG Creation
Confirmed `xfusion-asg` was successfully created.

![ASG Created](screenshots/ss22-asg-created.png)

---

### 23. Verified ALB Creation
Confirmed `xfusion-alb` was created successfully.

![ALB Created](screenshots/ss23-alb-created.png)

---

### 24. Verified Target Group Health
Verified that `xfusion-tg` had one healthy registered instance.

![Target Group Healthy](screenshots/ss24-tg-healthy.png)

---

### 25. Verified EC2 Instance
Confirmed that the EC2 instance launched by ASG was running.

![EC2 Running](screenshots/ss25-ec2-running.png)

---

### 26. Verified Application Accessibility
Accessed the ALB DNS name in the browser and confirmed that the **Nginx welcome page** was displayed.

![Nginx Page](screenshots/ss26-nginx-page.png)

---

## Verification
The following validations confirm successful task completion:

- Confirmed `xfusion-alb` was created successfully.

![ALB Created](screenshots/ss23-alb-created.png)

- Verified that `xfusion-tg` had one healthy registered instance.

![Target Group Healthy](screenshots/ss24-tg-healthy.png)

- Confirmed that the EC2 instance launched by ASG was running.

![EC2 Running](screenshots/ss25-ec2-running.png)

- Accessed the ALB DNS name in the browser and confirmed that the **Nginx welcome page** was displayed.

![Nginx Page](screenshots/ss26-nginx-page.png)


---

## Outcome
Successfully deployed a **highly available, auto-scaled web application architecture** using Launch Templates, Auto Scaling Groups, and an Application Load Balancer.

The system can:
- Automatically scale based on CPU utilization
- Distribute traffic across instances
- Recover from instance failures
- Maintain high availability across multiple Availability Zones

---

## Learnings
- Launch Templates simplify EC2 configuration reuse
- Auto Scaling ensures elasticity and resilience
- Target tracking scaling automatically adjusts capacity
- ALB distributes traffic only to healthy instances
- Health checks are critical for production reliability
- User Data enables automated instance provisioning

---

**Status:** Completed
