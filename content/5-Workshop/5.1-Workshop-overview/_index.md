---
title: "Workshop Overview"
date: 2026-08-05
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---



## Introduction

In this workshop, we will deploy the **AI Learning Assistant Platform** on **Amazon Web Services (AWS)**.

The AI Learning Assistant Platform is an intelligent learning platform built on **FastGPT (Customized)** and the **Retrieval-Augmented Generation (RAG)** architecture. It enables users to upload learning materials, build a **Knowledge Base**, and interact with an AI assistant that generates responses based on the uploaded documents.

The entire system is deployed on **Amazon EC2** using **Docker Compose**, together with **Amazon ECR**, **GitHub Actions**, **Amazon S3**, **Amazon CloudWatch**, **AWS IAM**, and **Security Groups** to establish a complete workflow for deployment, monitoring, security, and application management on AWS.

> **Figure 5.1. Deployment Architecture of the AI Learning Assistant Platform on AWS**

![Figure 5.1](/images/5.1.ws.png)

---

# Deployment Architecture

The AI Learning Assistant Platform follows a **Client–Server** architecture deployed on **Amazon Web Services (AWS)**.

Users access the platform through a web browser. Requests are routed through **Nginx**, which forwards them to the **Frontend** and **Backend** services. The Backend is responsible for business logic, Knowledge Base management, and the **Retrieval-Augmented Generation (RAG)** workflow.

The entire application is containerized using **Docker Compose** and deployed on a single **Amazon EC2** instance, integrating AWS services for storage, monitoring, backup, and security.

### System Components

| Component | Description |
|------------|-------------|
| Amazon EC2 | Hosts the entire AI Learning Assistant Platform |
| Docker Compose | Manages and orchestrates Docker containers |
| Nginx | Reverse Proxy |
| Frontend | User interface (Next.js / React) |
| Backend | FastGPT (Customized), AI Chat, and RAG processing |
| MongoDB | Stores application and user data |
| PostgreSQL + pgvector | Stores vector embeddings for semantic retrieval |
| MinIO | Stores uploaded learning materials |
| Amazon S3 | Stores backup data |
| Amazon ECR | Stores Docker images |
| GitHub Actions | Automates the CI/CD pipeline |
| Amazon CloudWatch | Monitors system performance and logs |
| AWS IAM | Manages access permissions |
| Security Group | Controls inbound and outbound network traffic |

---

# System Workflow

After the platform is successfully deployed, it operates as follows:

1. Users sign in to the platform.
2. Users upload learning materials.
3. The system processes documents, performs chunking, and generates vector embeddings.
4. The processed data is stored in the Knowledge Base.
5. Users submit questions through the AI Chat interface.
6. The Backend executes the Retrieval-Augmented Generation (RAG) process to retrieve relevant information.
7. The AI model generates responses based on the retrieved context.
8. The generated answer is returned to the user interface.

> **Figure 5.2. Workflow of the AI Learning Assistant Platform**

![Figure 5.2](/images/5.2.ws.png)

---

# Learning Outcomes

After completing this workshop, you will be able to:

- Deploy the AI Learning Assistant Platform on Amazon EC2 using Docker Compose.
- Deploy and manage a multi-container application on AWS.
- Build a CI/CD pipeline using GitHub Actions and Amazon ECR.
- Configure Amazon S3 for data backup.
- Monitor system performance with Amazon CloudWatch.
- Configure AWS IAM and Security Groups to secure the platform.
- Access and verify all core features of the AI Learning Assistant Platform.

---