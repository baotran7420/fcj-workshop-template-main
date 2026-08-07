---
title: "Overview & Architecture"
weight: 1
chapter: false
pre: "<b>5.1.</b>"
---

## Introduction

In this workshop, we will deploy the **AI Learning Assistant Platform** on **Amazon Web Services (AWS)**. The objective of this workshop is to demonstrate the complete deployment process of a real-world AI application in a cloud environment, including infrastructure preparation, server configuration, application deployment with Docker, CI/CD implementation, system monitoring, and post-deployment validation.

The AI Learning Assistant Platform is an intelligent learning system built on **FastGPT (Customized)** and the **Retrieval-Augmented Generation (RAG)** architecture. The platform enables users to upload learning materials, build a **Knowledge Base**, and interact with an AI assistant that generates responses based on the uploaded documents. Deploying the platform on AWS provides a scalable, manageable, and production-ready environment while simplifying system operations and monitoring.

---

## Problem & Goal

Students and lecturers often work with a large collection of learning materials, including textbooks, lecture slides, research papers, and technical documents. Searching for relevant information manually is time-consuming and becomes increasingly inefficient as the volume of documents grows.

Although **Large Language Models (LLMs)** have powerful natural language understanding capabilities, they still struggle to answer questions related to private or organization-specific documents. This limitation may lead to **hallucinations**, where the model generates inaccurate responses that are not supported by actual data.

To address this problem, the AI Learning Assistant Platform adopts the **Retrieval-Augmented Generation (RAG)** architecture. Users can upload their own documents, create a **Knowledge Base**, and ask questions directly about the uploaded content, significantly improving answer accuracy and learning efficiency.

This workshop aims to deploy the AI Learning Assistant Platform on AWS with the following objectives:

- Deploy the complete application on Amazon EC2.
- Package and manage all services using Docker Compose.
- Implement a CI/CD pipeline with GitHub Actions and Amazon ECR.
- Configure data backup using Amazon S3.
- Monitor system performance with Amazon CloudWatch.
- Configure automated notifications using CloudWatch Alarm and Amazon SNS.
- Build a secure, stable, and scalable deployment environment.

---

## Architecture Diagram

The AI Learning Assistant Platform is designed using a **Client–Server** architecture combined with the **Retrieval-Augmented Generation (RAG)** approach. The system consists of a web interface, backend services, databases, and AI components that work together to process user requests and generate responses based on uploaded documents.

> **Figure 5.1. Overall Architecture of the AI Learning Assistant Platform**

![Figure 5.1](/images/3.1.d.x.png)

Users access the platform through a web browser using the HTTP or HTTPS protocol. Requests are first received by the **Frontend** and then forwarded to the **Backend**, which handles business logic, user management, document processing, Knowledge Base management, and the Retrieval-Augmented Generation (RAG) workflow.

Within the system, **MongoDB** stores user information, conversations, and system configurations. **PostgreSQL** together with **pgvector** stores vector embeddings for semantic search, while **MinIO** stores uploaded learning materials used to build the Knowledge Base.

The architecture follows a **Production Lite** approach, making it suitable for a Minimum Viable Product (MVP) while still satisfying the essential requirements for deployment, scalability, data management, and cloud-based operation.

After completing the application architecture, the entire platform is deployed on Amazon Web Services (AWS), as illustrated in Figure 5.2.

> **Figure 5.2. AWS Deployment Architecture of the AI Learning Assistant Platform**

![Figure 5.2](/images/5.1.ws.png)

Users access the application through an **Elastic IP** or the domain name associated with the **Amazon EC2** instance using HTTP or HTTPS. All incoming traffic is controlled by **Security Groups** before reaching the EC2 instance.

Inside the EC2 instance, **Docker Compose** manages multiple Docker containers, including **Nginx**, **Frontend**, **Backend**, **MongoDB**, **PostgreSQL with pgvector**, and **MinIO**. Container data is stored on **Amazon EBS**, ensuring persistent storage during system operation.

The deployment process is fully automated using **GitHub Actions** and **Amazon ECR**. Whenever source code is updated in the GitHub repository, GitHub Actions automatically builds Docker images, pushes them to Amazon ECR, and deploys the latest version to Amazon EC2.

To ensure reliable operation, **Amazon CloudWatch** collects logs and system metrics, **CloudWatch Alarm** monitors critical resources such as CPU and memory usage, and **Amazon SNS** sends email notifications whenever an issue is detected. Additionally, **Amazon S3** is used to store backup data, helping protect the system against data loss and supporting disaster recovery.

Together, these two architecture diagrams provide an overview of the AI Learning Assistant Platform and serve as the foundation for the deployment procedures presented in the following sections of this workshop.

---

## Why These AWS Services?

To support the deployment, operation, and management of the AI Learning Assistant Platform, this workshop leverages several AWS services, each serving a specific purpose within the overall architecture.

| AWS Service | Reason for Selection |
|--------------|----------------------|
| **Amazon EC2** | Hosts the entire application on a single virtual server, simplifying Docker Compose management and reducing deployment costs for the MVP stage. |
| **Amazon EBS** | Provides persistent storage for Docker volumes and application data, ensuring data remains available after instance restarts. |
| **Amazon ECR** | Stores Docker images securely and integrates seamlessly with GitHub Actions for automated CI/CD workflows. |
| **Amazon S3** | Provides cost-effective, highly durable storage for backup data and uploaded documents. |
| **Amazon CloudWatch** | Collects logs, monitors system metrics, and provides real-time operational visibility. |
| **CloudWatch Alarm** | Monitors CPU, memory, disk usage, and other metrics, triggering alerts when predefined thresholds are exceeded. |
| **Amazon SNS** | Sends email notifications whenever CloudWatch Alarm detects system issues. |
| **AWS IAM** | Manages user identities and access permissions following the Principle of Least Privilege. |
| **Security Group** | Controls inbound network traffic by allowing only required ports such as SSH (22), HTTP (80), and HTTPS (443). |
| **Elastic IP** | Provides a static public IP address, ensuring consistent access to the deployed application. |

The combination of these AWS services enables a complete deployment workflow, including application deployment, CI/CD automation, data storage, monitoring, backup, and security management. These services also provide a solid foundation for the detailed deployment steps presented in the following sections of this workshop.