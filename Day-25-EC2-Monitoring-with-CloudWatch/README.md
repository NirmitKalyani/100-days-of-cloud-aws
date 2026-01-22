# Day 25 – Monitor EC2 CPU Utilization with CloudWatch Alarm (AWS)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by KodeKloud, this task focuses on **monitoring an EC2 instance using Amazon CloudWatch**.

The objective was to launch an EC2 instance named **`nautilus-ec2`** and configure a **CloudWatch alarm** named **`nautilus-alarm`** that triggers when **CPU utilization exceeds 90% for one consecutive 5-minute period**, sending notifications via an existing **SNS topic**.

---

## Concept
**Amazon CloudWatch** provides real-time monitoring of AWS resources.  
By creating **CloudWatch alarms**, we can automatically react to metric thresholds and trigger actions such as **SNS notifications**.

Monitoring **CPU utilization** is critical to detect performance bottlenecks, unexpected traffic spikes, or inefficient application behavior.

---

## Real-World Use Case
CloudWatch alarms are commonly used to:
- Detect high CPU or memory usage
- Trigger alerts before outages occur
- Integrate with auto-scaling policies
- Monitor application performance
- Improve system reliability and observability

---

## Requirements
- **EC2 instance name:** `nautilus-ec2`
- **CloudWatch alarm name:** `nautilus-alarm`
- **Metric:** CPUUtilization
- **Statistic:** Average
- **Threshold:** ≥ 90%
- **Evaluation period:** 1 × 5 minutes
- **SNS topic:** `nautilus-sns-topic`
- **AMI:** Ubuntu
- **Region:** `us-east-1`

---

## AWS Services Used
- Amazon EC2
- Amazon CloudWatch
- Amazon SNS

---

## Steps Performed

1. Navigated to **Services → EC2** from the AWS Management Console.

   ![Open EC2](screenshots/step-1-open-ec2.png)

2. Launched a new EC2 instance with the following configuration:

   - **Name:** `nautilus-ec2`
   - **AMI:** Ubuntu

   ![Name EC2 Instance and Select AMI](screenshots/step-2-name-ec2-and-select-ami.png) 

   - **Instance type:** t3.micro
   - **Key pair:** Proceed Without KeyPair

   ![Select Instance Type and configure KeyPair](screenshots/step-2-configure-instance-type-and-key-pair.png)

   - **Security group:** Create launch-wizard-1 and click launch instance

   ![Review SG and Launch EC2 Instance](screenshots/step-2-configure-security-group-and-launch-ec2.png)

3. Verified that the EC2 instance was running successfully.

   ![EC2 Running](screenshots/step-3-ec2-running.png)

4. Navigated to **Services → CloudWatch → Metrics** and verified the **CPUUtilization** metric for the EC2 instance.

   ![Navigate to CloudWatch](screenshots/step-4-navigate-to-cloudwatch.png) 

   ![CPU Metric](screenshots/step-4-cpu-metric.png)

5. Navigated to **CloudWatch → Alarms** and clicked **Create alarm**.

   ![Create Alarm](screenshots/step-5-create-alarm.png)

6. Selected the **EC2 → Per-Instance Metrics → CPUUtilization** metric.

   ![Select Metric](screenshots/step-6-select-metric.png)

7. Configured the alarm conditions:

   - **Statistic:** Average
   - **Period:** 5 minutes

   ![Configure Period and Statistics](screenshots/step-7-configure-period-and-statistics.png) 

   - **Threshold:** Greater than or equal to 90
   - **Datapoints to alarm:** 1 out of 1

   ![Configure Threshold and Datapoints](screenshots/step-7-configure-threshold-and-datapoints.png)

8. Configured the alarm action to send notifications to the SNS topic **`nautilus-sns-topic`**.

   ![Configure SNS Action](screenshots/step-8-configure-sns.png)

9. Named the alarm **`nautilus-alarm`** and created it.

   ![Create Alarm Final](screenshots/verification-alarm-created.png)

---

## Verification
The following screenshots confirm successful completion of the task:

- CloudWatch alarm **`nautilus-alarm`** created successfully

  ![Alarm Created](screenshots/verification-alarm-created.png)

- Alarm in **OK** state while CPU utilization is below threshold

  ![Alarm OK State](screenshots/verification-alarm-ok.png)

- SNS topic correctly attached to the alarm

  ![SNS Attached](screenshots/verification-sns-attached.png)

---

## Outcome
The EC2 instance **`nautilus-ec2`** is now actively monitored using **Amazon CloudWatch**, and the alarm **`nautilus-alarm`** will notify via **SNS** whenever CPU utilization exceeds **90% for 5 minutes**, enabling proactive monitoring and alerting.

---

## Learnings
- CloudWatch provides native monitoring for EC2 instances
- CPUUtilization is a critical performance metric
- Alarms can trigger automated notifications using SNS
- Proper thresholds help detect issues early
- Monitoring is essential for production-grade systems

---

**Status:** Completed
