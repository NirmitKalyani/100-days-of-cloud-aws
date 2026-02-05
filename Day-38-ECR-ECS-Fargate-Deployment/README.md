# Day 38 – Deploy Containerized Application Using Amazon ECR and ECS (Fargate)

## Task Overview
As part of the **100 Days of Cloud (AWS)** challenge by **KodeKloud**, this task focuses on deploying a **containerized application** using **Amazon Elastic Container Registry (ECR)** and **Amazon Elastic Container Service (ECS)** with the **Fargate launch type**.

The objective was to create a **private ECR repository**, build and push a Docker image from the aws-client host, create an **ECS cluster**, define a **task definition**, and deploy the application using an **ECS service** running on **AWS Fargate**.

---

## Concept
This task demonstrates a complete container deployment workflow on AWS:

- **Amazon ECR** for private Docker image storage
- **Docker** for image build and push
- **Amazon ECS** for container orchestration
- **AWS Fargate** for serverless container execution

Key concepts involved:
- Private container registries
- Docker image lifecycle
- ECS clusters, task definitions, and services
- Serverless container deployment using Fargate

---

## Real-World Use Case
This architecture is widely used to:
- Deploy microservices and web applications
- Eliminate EC2 instance management
- Scale container workloads automatically
- Integrate CI/CD pipelines with ECS
- Run production-grade containerized workloads securely

---

## Requirements
- **ECR Repository:** `nautilus-ecr`
- **Dockerfile location:** `/root/pyapp` (aws-client host)
- **Image tag:** `latest`
- **ECS Cluster:** `nautilus-cluster`
- **Task Definition:** `nautilus-taskdefinition`
- **Service:** `nautilus-service`
- **Launch type:** Fargate
- **Running tasks:** Minimum 1

---

## AWS Services Used
- Amazon Elastic Container Registry (ECR)
- Amazon Elastic Container Service (ECS)
- AWS Fargate
- Docker
- AWS CLI

---

## Steps Performed

### 1. Created a Private ECR Repository
Navigated to **Amazon ECR** from the AWS Management Console and initiated repository creation.

![Go to ECR](screenshots/ss1-go-to-ecr.png)

Created a **private repository** named `nautilus-ecr`.

![Create Repository](screenshots/ss2-create-repo.png)  

![Private Repo Name](screenshots/ss3-private-repo-name.png)

Verified that the repository was successfully created.

![Verify Repo](screenshots/ss4-verify-repo.png)

---

### 2. Built Docker Image on aws-client Host
Navigated to `/root/pyapp` on the aws-client host and verified the existing **Dockerfile** and application files.

![Verify Dockerfile](screenshots/ss5-verify-dockerfile.png)

Built the Docker image using the ECR repository URI.

![Docker Build](screenshots/ss6-docker-build.png)

Verified the Docker image was created locally.

![Docker Images](screenshots/ss7-docker-images.png)

---

### 3. Authenticated Docker and Pushed Image to ECR
Authenticated Docker with Amazon ECR using AWS CLI.

![Docker Login](screenshots/ss8-docker-login.png)

Pushed the Docker image to the **nautilus-ecr** repository.

![Docker Push](screenshots/ss9-docker-push.png)

Verified the image was successfully pushed in the ECR console.

![Verify Image in ECR](screenshots/ss10-verify-image-ecr.png)

---

### 4. Created ECS Cluster (Fargate)
Navigated to **Amazon ECS** service.

![Go to ECS](screenshots/ss11-go-to-ecs.png)

Started cluster creation.

![Create Cluster](screenshots/ss12-create-cluster.png)

Created a cluster named **`nautilus-cluster`** using **Fargate only** infrastructure.

![Cluster Configuration](screenshots/ss13-cluster-config.png)

Verified the ECS cluster was created successfully.

![Cluster Created](screenshots/ss14-verify-cluster.png)

---

### 5. Created ECS Task Definition
Navigated to **Task Definitions** and created a new task definition.

![Create Task Definition](screenshots/ss15-create-task-definition.png)

Configured infrastructure requirements:
- Launch type: **AWS Fargate**
- CPU: **0.5 vCPU**
- Memory: **1 GB**

![Task Size](screenshots/ss16-task-size.png)

Added container details:
- Container name: `pyapp`
- Image source: Amazon ECR

![Container Details](screenshots/ss17-container-details.png)

Selected the **nautilus-ecr** private repository and image tag.

![Select ECR Image](screenshots/ss18-select-ecr-image.png)

Verified task definition creation.

![Task Definition Created](screenshots/ss19-task-definition-created.png)

---

### 6. Created ECS Service
Navigated to the ECS cluster and created a new service.

![Create Service](screenshots/ss20-create-service.png)

Selected the previously created task definition and Provided service name **`nautilus-service`**..

![Select Task Definition](screenshots/ss21-select-task-definition.png)

Configured compute options:
- Launch type: **Fargate**

![Compute Configuration](screenshots/ss22-service-name.png)

Created a new security group **`nautilus-web-sg`** allowing inbound HTTP traffic.

![Security Group](screenshots/ss23-service-sg.png)

Verified the ECS service was created and active.

![Service Active](screenshots/ss24-service-active.png)

---

## Verification
The following steps and screenshots confirm successful completion of the task:

- Docker image successfully pushed to the private ECR repository `nautilus-ecr`.

  ![Verify Image in ECR](screenshots/ss10-verify-image-ecr.png)

- ECS cluster `nautilus-cluster` created and available.

  ![Cluster Created](screenshots/ss14-verify-cluster.png)

- ECS task definition created successfully using the ECR image.

  ![Task Definition Created](screenshots/ss19-task-definition-created.png)

- ECS service `nautilus-service` created and in **Active** state.

  ![Service Active](screenshots/ss24-service-active.png)

- ECS task running successfully under the service.

  ![Task Running](screenshots/ss25-task-running.png)

- Public IPv4 address assigned to the running task.

  ![Public IPv4](screenshots/ss26-public-ip.png)

- Application accessible via browser and serving HTML content as expected.

  ![Application Running](screenshots/ss27-app-running.png)


---

## Outcome
A containerized application was successfully deployed using **Amazon ECR**, **Amazon ECS**, and **AWS Fargate**. The application runs in a fully serverless container environment without managing EC2 instances.

---

## Learnings
- ECR enables secure private image storage
- ECS simplifies container orchestration
- Fargate removes infrastructure management overhead
- Task definitions control container runtime behavior
- ECS services ensure application availability

---

## Status
**Status:** Completed
