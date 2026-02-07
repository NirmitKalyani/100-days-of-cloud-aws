# Day 36 – EC2 Web Server with Application Load Balancer (ALB)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on deploying an **EC2-based web server** and integrating it with an **Application Load Balancer (ALB)** to ensure **high availability and efficient traffic distribution**.

The objective was to launch an EC2 instance running **Nginx**, configure a **target group**, set up an **Application Load Balancer**, adjust **security groups**, and verify that the web server is accessible using the **ALB DNS name**.

---

## Concept
An **Application Load Balancer (ALB)** distributes incoming HTTP traffic across backend targets such as EC2 instances. This improves availability, fault tolerance, and scalability while enabling better traffic control.

Key concepts involved:
- EC2 instance provisioning
- Security Groups
- Application Load Balancer
- Target Groups
- Nginx web server
- Health checks and traffic routing

---

## Real-World Use Case
This architecture reflects real-world cloud applications where:
- Web servers run on EC2 instances
- Load balancers handle incoming traffic
- Security groups enforce controlled access
- High availability is a core requirement
- Applications must scale reliably

---

## Requirements
- EC2 instance name: `devops-ec2`
- AMI: Ubuntu
- Instance type: `t3.micro`
- Security group: `devops-sg`
- Application Load Balancer: `devops-alb`
- Target group: `devops-tg`
- Listener port: 80
- Target port: 80

---

## AWS Services Used
- Amazon EC2
- Application Load Balancer
- Target Groups
- Security Groups
- Amazon VPC

---

## Steps Performed

### Security Group Configuration

1. Navigated to EC2 security groups and initiated creation of a new security group.

   ![Open EC2 Security Groups](screenshots/step-01-open-ec2-security-groups.png)

2. Created a security group named `devops-sg` and selected the appropriate VPC.

   ![Create devops-sg](screenshots/step-02-create-devops-sg-details.png)

3. Added an inbound rule allowing HTTP traffic on port 80 from the default security group.

   ![HTTP Rule for devops-sg](screenshots/step-03-devops-sg-http-inbound-rule.png)

4. Verified that the `devops-sg` security group was created successfully.

   ![devops-sg Created](screenshots/step-04-devops-sg-created.png)

5. Edited inbound rules of the default security group to allow HTTP traffic from anywhere.

   ![Edit Default SG](screenshots/step-05-edit-default-sg-http-anywhere.png)

6. Verified inbound HTTP rules in the default security group.

   ![Default SG Verified](screenshots/step-06-default-sg-http-verified.png)

---

### EC2 Instance Creation

7. Navigated to EC2 instances and clicked on launch instance.

   ![Launch EC2](screenshots/step-07-launch-ec2-instance.png)

8. Named the EC2 instance as `devops-ec2`.

   ![Name devops-ec2](screenshots/step-08-name-devops-ec2.png)

9. Selected an Ubuntu AMI.

   ![Select Ubuntu AMI](screenshots/step-09-select-ubuntu-ami.png)

10. Selected instance type `t3.micro` and proceeded without a key pair.

    ![Select Instance Type](screenshots/step-10-select-instance-type.png)

11. In network settings, selected an existing security group and chose `devops-sg`.

    ![Attach devops-sg](screenshots/step-11-attach-devops-sg-to-ec2.png)

12. Kept storage configuration as default.

    ![Default Storage](screenshots/step-12-storage-default.png)

13. Added user data to install and start the Nginx web server during launch.

    ![User Data Script](screenshots/step-13-user-data-nginx.png)

14. Verified that the `devops-ec2` instance was in running state.

    ![EC2 Running](screenshots/step-14-devops-ec2-running.png)

---

### Application Load Balancer Setup

15. Navigated to Load Balancers service.

    ![Open Load Balancers](screenshots/step-15-open-load-balancers.png)

16. Initiated creation of an Application Load Balancer.

    ![Create ALB](screenshots/step-16-create-alb.png)

17. Configured basic settings with:
    - Name: `devops-alb`
    - Scheme: Internet-facing
    - IP type: IPv4

    ![ALB Basic Config](screenshots/step-17-devops-alb-basic-config.png)

18. Selected default VPC and availability zones containing the EC2 instance.

    ![ALB Network Mapping](screenshots/step-18-alb-network-mapping.png)

19. Attached the default security group to the ALB.

    ![ALB Security Group](screenshots/step-19-alb-default-sg.png)

---

### Target Group Configuration

20. Created a target group named `devops-tg` with protocol HTTP and port 80.

    ![Create Target Group](screenshots/step-20-create-devops-target-group.png)

21. Registered `devops-ec2` as the target instance.

    ![Register Target](screenshots/step-21-register-devops-ec2-target.png)

22. Reviewed target group configuration and created the target group.

    ![Review Target Group](screenshots/step-22-review-create-target-group.png)

23. Verified that the target group was created successfully.

    ![Target Group Created](screenshots/step-23-devops-tg-created.png)

---

### Traffic Routing and Verification

24. Configured ALB listener to forward traffic to `devops-tg`.

    ![Listener Routing](screenshots/step-24-alb-listener-forward-to-tg.png)

25. Verified that the Application Load Balancer was active.

    ![ALB Active](screenshots/step-25-devops-alb-active.png)

26. Confirmed that `devops-ec2` passed health checks and was marked healthy.

    ![Healthy Target](screenshots/step-26-target-healthy.png)

27. Accessed the ALB DNS name in a browser and verified the Nginx welcome page.

    ![Nginx via ALB](screenshots/step-27-nginx-via-alb-dns.png)

---

## Verification
The following confirms successful completion:
- Target group shows healthy EC2 instance

    ![Healthy Target](screenshots/step-26-target-healthy.png)    

- EC2 instance is running with Nginx installed
- ALB is active and routing traffic correctly
- Web server is accessible via ALB DNS

    ![Nginx via ALB](screenshots/step-27-nginx-via-alb-dns.png)

---

## Outcome
A highly available web server environment was successfully deployed using an EC2 instance behind an Application Load Balancer. This setup demonstrates proper security configuration, load balancing, and real-world AWS web architecture.

---

## Key Takeaways
- ALB improves application availability and traffic handling
- Security groups control service-to-service access
- Target groups manage backend routing
- Automated instance setup reduces manual effort
- Load-balanced architectures are production standards

---

**Status:** Completed
