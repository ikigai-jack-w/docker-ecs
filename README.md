# AWS ECS Deployment with CI/CD

## Overview

This project is a containerized application deployed to **AWS ECS (Elastic Container Service)** using **Docker**. It includes a full **CI/CD pipeline** set up with **GitHub Actions** (or another CI/CD tool like Jenkins/GitLab CI) to automate build, test, and deployment processes.

## Features

- **Dockerized Application**: Containerized using Docker.
- **AWS ECS Deployment**: Hosted on AWS ECS with Fargate or EC2.
- **CI/CD Pipeline**: Automates build, test, and deployment using GitHub Actions.
- **Infrastructure as Code**: Uses Terraform or AWS CloudFormation (Optional).
- **Load Balancer**: Configured with AWS ALB (Application Load Balancer).
- **Auto-scaling & Monitoring**: Enabled with CloudWatch.

## Prerequisites

Ensure you have the following installed and configured:

- **AWS CLI** (Configured with necessary credentials)
- **Docker**
- **Terraform** (If using IaC for infrastructure setup)
- **GitHub Actions** (or an alternative CI/CD tool)

## Architecture

```
User --> ALB (Application Load Balancer) --> ECS Service --> ECS Task (Docker Container) --> Database (if applicable)
```

## Getting Started

### 1. Clone the Repository

```sh
git clone https://github.com/your-repo/docker-ecs.git
cd docker-ecs
```

### 2. Build and Run Docker Locally

```sh
docker build -t docker-ecs .
docker run -p 8080:3000 docker-ecs
```

### 3. Push Docker Image to AWS ECR

```sh
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com

docker tag docker-ecs:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/docker-ecs:latest

docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/docker-ecs:latest
```

### 4. Deploy to AWS ECS

#### using AWS CLI:

```sh
aws ecs update-service --cluster my-cluster --service my-service --force-new-deployment
```

## CI/CD Setup

## Monitoring & Logs

- Use **AWS CloudWatch Logs** to monitor container logs.
- Use **AWS ECS Console** to check task status and service health.
- Use **AWS ALB Logs** for request/response monitoring.

## Contributing

Feel free to open issues or submit pull requests!

## License

This project is open-source under the MIT License.
