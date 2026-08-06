---
title: "Proposal"
date: 2026-08-04
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI Learning Assistant Platform

## An Intelligent Document-Based Learning Assistant Platform Deployed on AWS

# Part 1. Project Introduction

## 1.1 Background

The rapid advancement of **Artificial Intelligence (AI)**, particularly **Large Language Models (LLMs)**, has significantly transformed the education sector. AI-powered systems are capable of assisting learners in searching for information, explaining concepts, and interacting with learning materials through natural language, thereby improving learning efficiency.

However, most existing AI chatbots rely solely on pre-trained knowledge and are unable to accurately answer questions related to users' personal learning materials. Without sufficient contextual information, AI models may generate inaccurate responses or provide information that is not consistent with the uploaded documents.

In practice, students often work with various learning resources, including textbooks, lecture slides, reference materials, and laboratory manuals. As the volume of these documents continues to grow, locating relevant information becomes increasingly time-consuming and negatively impacts learning efficiency.

To address these challenges, this project proposes the **AI Learning Assistant Platform**, an intelligent learning assistant that enables users to effectively interact with their learning materials using **Retrieval-Augmented Generation (RAG)** technology. The platform is developed based on **FastGPT** and deployed on **Amazon Web Services (AWS)** to ensure scalability, high availability, and security.

---

## 1.2 Objectives

The primary objective of this project is to develop an intelligent learning assistant platform that enables learners to access and utilize knowledge from educational documents efficiently.

The main objectives of the project include:

- Building an AI Learning Assistant system applying **Retrieval-Augmented Generation (RAG)** technology.
- Allowing users to upload and manage learning documents.
- Developing a **Knowledge Base** to support semantic information retrieval.
- Enabling AI to answer questions based on the content of the user's documents.
- Integrating learning support features such as lesson summaries, quiz generation, and Flashcards.
- Deploying the system on **Amazon Web Services (AWS)** following the cloud computing model.

---

## 1.3 Solution Overview

The AI Learning Assistant Platform is an intelligent learning platform that allows users to upload learning materials and interact with AI using natural language.

After a document is uploaded, the system automatically processes the content, splits the document into smaller chunks, generates **Embeddings**, and builds a **Knowledge Base**. When a user asks a question, the system uses the **Retrieval-Augmented Generation (RAG)** mechanism to retrieve relevant document segments and provides context to the AI model to generate an accurate response closely aligned with the document's content.

In addition to Q&A capabilities, the system also supports document management, lesson summarization, quiz generation, Flashcards, and learning history tracking. The entire application is deployed on AWS using Docker Compose and the deployment process is automated through GitHub Actions in conjunction with Amazon ECR, creating a favorable foundation for future scaling and development.

### Quick Overview

| Criteria | Value |
|----------|----------|
| Project Name | AI Learning Assistant Platform |
| Project Type | Intelligent Learning Assistant Platform |
| Target Audience | Students, Instructors |
| Development Platform | FastGPT (Customized) |
| AI Technology | RAG, Knowledge Base, Embedding |
| Cloud Platform | Amazon Web Services (AWS) |
| AWS Services | Amazon EC2, Amazon S3, Amazon CloudWatch |
| Database | MongoDB, PostgreSQL |
| Deployment Method | Docker Compose |

# Part 2. Problem Analysis and Proposed Solution

## 2.1 The Problem

In today's educational environment, students often have to use multiple sources of materials such as textbooks, lecture slides, reference documents, and lab guides. As the amount of material grows, searching for specific content becomes time-consuming and affects learning efficiency.

Although current AI chatbots can answer many questions using natural language, most of them rely only on pre-trained knowledge. This prevents AI from accurately extracting content from users' personal documents and can result in responses that are out of context or not present in the documents.

Therefore, a solution is needed that allows AI to understand and extract data directly from learning materials, helping users find information quickly and receive more accurate answers.

---

## 2.2 Proposed Solution

To solve the above problems, this project proposes building the **AI Learning Assistant Platform** based on **Retrieval-Augmented Generation (RAG)** technology.

Unlike traditional AI chatbots, the system allows users to upload learning materials to build a **Knowledge Base**. When a user asks a question, the system retrieves relevant content segments from the Knowledge Base before sending them to the AI model to generate an answer.

Thanks to this, the AI can:

- Answer based on the content of the user's documents.
- Reduce the phenomenon of AI generating unfounded information (Hallucination).
- Display reference sources for the answers.
- Improve the accuracy and reliability of the results.

In addition to the Q&A function, the system also supports features such as:

- Learning document management.
- Lesson content summarization.
- Quiz generation.
- Flashcard generation for revision.
- Saving learning and conversation history.

---

## 2.3 Workflow

The system's workflow consists of the following steps:

1. The user uploads learning materials to the system.
2. The system extracts content and processes the documents.
3. The content is divided into small segments (Chunking).
4. The system creates Embeddings and saves them to the Vector Database.
5. The user asks a question in natural language.
6. The system retrieves suitable document segments from the Knowledge Base.
7. The AI model uses the document segments as context to generate an answer.
8. The result along with the reference source is displayed to the user.

> **Figure 2.1. Workflow of the AI Learning Assistant Platform using RAG.**

![Retrieval-Augmented Generation Workflow](/images/h3bl3.png)

## 2.4 Benefits of the Solution

Applying RAG technology to the AI Learning Assistant Platform brings many benefits:

- Supports quick information search in learning materials.
- Improves the accuracy of answers by using real data.
- Reduces Hallucination in AI models.
- Saves time for studying and revising.
- Creates an intelligent, flexible, and scalable learning environment on the AWS platform.

The solution is not only suitable for students and instructors but can also be expanded for training organizations or enterprises needing to build an internal document-based Q&A system.

# Part 3. System Design and Architecture

## 3.1 Overall Architecture

The AI Learning Assistant Platform is built on a **Client–Server** model combined with **Retrieval-Augmented Generation (RAG)** architecture and deployed on **Amazon Web Services (AWS)** to build an intelligent learning platform capable of managing documents, semantic searching, and AI-assisted learning.

The system architecture is divided into five main layers:

- **Client Layer:** Students and instructors access the system via web browsers using HTTP or HTTPS protocols.
- **Application Layer:** The entire application is deployed on **Amazon EC2** as **Docker Containers** managed by **Docker Compose**, including Nginx, Frontend, Backend, MongoDB, PostgreSQL with pgvector, and MinIO.
- **AI & Data Layer:** The Backend handles AI Chat, Retrieval-Augmented Generation (RAG), Knowledge Base, Document Processing, and Semantic Search. PostgreSQL with **pgvector** stores vector embeddings, while MongoDB manages user data, conversations, and system configurations.
- **Infrastructure Layer:** Amazon EBS provides persistent storage for Docker Volumes and system data. Amazon S3 is used to store backups and redundant documents.
- **DevOps & Monitoring Layer:** GitHub Actions and Amazon ECR support the CI/CD pipeline, while Amazon CloudWatch, CloudWatch Alarm, and AWS Budgets help monitor the system, alert on issues, and control operational costs.

The architecture is designed following a **Production Lite** approach, suitable for MVP scale while still meeting basic requirements for deployment, security, monitoring, backup, and automation on the AWS platform.

> **Figure 3.1. Overall Architecture of the AI Learning Assistant Platform.**

![Figure 3.1](/images/3.1.d.x.png)

---

## 3.2 Deployment Architecture on AWS

The AI Learning Assistant Platform is deployed on **Amazon Web Services (AWS)** in the **US East (N. Virginia) – us-east-1** Region.

Users access the platform through an **Elastic IP** or the domain name of the Amazon EC2 instance using HTTP or HTTPS protocols. All incoming traffic is controlled by **Security Groups** before reaching the EC2 server.

Inside Amazon EC2, Docker Compose manages the system's containers, including Nginx, Frontend, Backend, MongoDB, PostgreSQL with pgvector, MinIO. Amazon EBS is used for storing Docker Volumes and persistent data.

To ensure data resilience, MongoDB, PostgreSQL, and MinIO are periodically backed up to **Amazon S3**. Amazon CloudWatch combined with CloudWatch Alarm is used to monitor system performance and send alerts when issues occur.

The deployment process is automated using **GitHub Actions** and **Amazon ECR**. When source code is updated on the GitHub Repository, GitHub Actions automatically builds the Docker Image, pushes the Image to Amazon ECR, and deploys the new version to Amazon EC2.

### AWS Services Used

| AWS Service | Role |
|-------------|----------|
| Amazon EC2 | Runs the entire AI Learning Assistant system |
| Amazon EBS | Stores Docker Volumes and persistent data |
| Amazon S3 | Backs up MongoDB, PostgreSQL, and learning documents |
| Amazon ECR | Manages Docker Images |
| Amazon CloudWatch | Monitors Metrics and Logs |
| CloudWatch Alarm | Alerts on CPU, Memory, Disk, and service status |
| Amazon SNS | Sends Email Notifications when alerts occur |
| AWS IAM | Manages access permissions for AWS resources |
| Security Group | Controls network access to the EC2 instance |
| AWS Budgets | Monitors and alerts on AWS costs |

The current architecture is optimized for internship environments and the MVP phase. Deploying on a single Amazon EC2 instance helps reduce operational costs while ensuring future scalability through CI/CD, Docker Containers, and AWS management services.

> **Figure 3.2. System Deployment Architecture on AWS.**

![Figure 3.2](/images/3.2.d.s.png)

---

## 3.3 Database Design

The system utilizes multiple storage components to meet requirements for data management, semantic retrieval, and learning document storage.

| Component | Role |
|------------|----------|
| MongoDB | Stores user information, conversations, Knowledge Base, and system configurations |
| PostgreSQL + pgvector | Stores Vector Embeddings for Semantic Search and Retrieval-Augmented Generation |
| MinIO | Stores learning documents uploaded by users |
| Amazon S3 | Backs up MongoDB, PostgreSQL, and learning documents |
| Amazon EBS | Stores Docker Volumes and persistent system data |

MongoDB, PostgreSQL, and MinIO operate within the internal Docker network and are not directly exposed to the Internet to enhance system security.

> **Figure 3.3. Database Schema of the System.**

![Figure 3.3](/images/3.3.pr.drawio.png)

---

## 3.4 Workflow Process

After a user uploads a document to the system, the AI Learning Assistant Platform executes the Retrieval-Augmented Generation (RAG) process through the following steps:

1. The user uploads learning materials to the system.
2. The Backend extracts content from the document.
3. The document is divided into small segments (Chunking).
4. The system creates Vector Embeddings for each segment.
5. Embeddings are stored in PostgreSQL with pgvector, while Metadata is stored in MongoDB.
6. The user submits a question from the AI Chat interface.
7. The Backend generates an Embedding for the question and performs Semantic Search in the Vector Database.
8. Relevant document segments are retrieved and combined with the question to form a Prompt.
9. The Prompt is sent to the Large Language Model (LLM).
10. The AI generates a response based on the document's context and returns the result along with reference sources to the user.

This process helps AI reduce Hallucination, improve response accuracy, and effectively utilize users' learning resources.

> **Figure 3.4. Workflow of the AI Learning Assistant Platform using RAG.**

![Figure 3.4](/images/3.4.p.r.png)

---

## 3.5 Technology Stack

| Component | Technology |
|------------|-----------|
| Frontend | Next.js, React, TypeScript |
| Backend | FastGPT (Customized) |
| AI | Large Language Models (LLMs) |
| AI Framework | Retrieval-Augmented Generation (RAG) |
| Database | MongoDB, PostgreSQL + pgvector |
| Object Storage | MinIO |
| Containerization | Docker, Docker Compose |
| Version Control | GitHub |
| CI/CD | GitHub Actions |
| Container Registry | Amazon ECR |
| Cloud Platform | Amazon Web Services (AWS) |
| Monitoring | Amazon CloudWatch, CloudWatch Alarm |
| Backup Storage | Amazon S3 |
| Persistent Storage | Amazon EBS |
| Cost Management | AWS Budgets |

# Part 4. Deployment and Testing

## 4.1 Deployment Environment

The AI Learning Assistant Platform is deployed on **Amazon Web Services (AWS)** in the **US East (N. Virginia) – us-east-1** Region.

The entire system is deployed on an **Amazon EC2** instance using **Docker Compose**, including **Nginx**, **Frontend (Next.js/React)**, **Backend (FastGPT Customized)**, **MongoDB**, **PostgreSQL with pgvector**, and **MinIO**.

The system uses **Amazon EBS** for persistent data storage, **Amazon S3** for data backup, **Amazon ECR** for managing Docker Images, **GitHub Actions** for CI/CD automation, **Amazon CloudWatch** for system monitoring, and **AWS IAM**, **Security Group**, and **AWS Budgets** for managing security and costs.

### Environment Configuration

| Component | Technology / Service |
|------------|----------------------|
| Cloud Platform | Amazon Web Services (AWS) |
| Region | us-east-1 |
| Compute | Amazon EC2 |
| Persistent Storage | Amazon EBS |
| Container | Docker, Docker Compose |
| Reverse Proxy | Nginx |
| Frontend | Next.js, React |
| Backend | FastGPT (Customized) |
| Database | MongoDB, PostgreSQL + pgvector |
| Object Storage | MinIO |
| Container Registry | Amazon ECR |
| CI/CD | GitHub Actions |
| Monitoring | Amazon CloudWatch |
| Backup Storage | Amazon S3 |
| Security | AWS IAM, Security Group |
| Cost Monitoring | AWS Budgets |

> **Figure 4.1. Deployment Environment of the AI Learning Assistant Platform on AWS.**

![Figure 4.1](/images/4.1.d.x.png)

---

## 4.2 System Deployment Process

The deployment workflow is executed through the following steps:

1. Initialize and configure **Amazon EC2**, **Security Group**, and **Elastic IP**.
2. Install **Docker** and **Docker Compose** on Amazon EC2.
3. Push the source code to the **GitHub Repository**.
4. **GitHub Actions** automatically builds the Docker Image and pushes it to **Amazon ECR**.
5. Amazon EC2 pulls the new Docker Image and starts the containers using **Docker Compose**.
6. **Amazon CloudWatch** monitors the system's operational status.
7. MongoDB, PostgreSQL, and MinIO data are periodically backed up to **Amazon S3**.

> **Figure 4.2. Deployment Workflow of the AI Learning Assistant Platform on AWS.**

![Figure 4.2](/images/4.2.d.x.png)

---

## 4.3 System Testing

After successful deployment, the system was tested to evaluate the stability and functionality of its core features.

| Function | Result |
|-----------|----------|
| User Authentication and Login | Passed |
| Course Management | Passed |
| Learning Document Upload | Passed |
| Knowledge Base Generation | Passed |
| AI Chat (RAG) | Passed |
| Lesson Summary | Passed |
| Quiz Generation | Passed |
| Flashcard Generation | Passed |
| CI/CD Deployment | Passed |

The testing results demonstrate that the system operates stably, the Docker Containers function normally, and the core functionalities meet the platform's requirements.

---

## 4.4 Monitoring and Operations

During system operation, **Amazon CloudWatch** is used to monitor performance and operational status.

The monitored metrics include:

- CPU Utilization
- Memory Usage
- Disk Usage
- Network Traffic
- Docker Container Logs

Additionally, data from MongoDB, PostgreSQL, and learning documents are periodically backed up to **Amazon S3** to ensure data recovery capabilities in case of incidents. **AWS Budgets** is used to track costs and alert when usage exceeds the established budget.

# Part 5. Security and Cost Optimization

## 5.1 System Security

The AI Learning Assistant Platform stores user accounts, learning materials, and conversation histories. Therefore, the system applies multiple measures to ensure data safety when deployed on Amazon Web Services (AWS).

The primary security measures include:

- Using **AWS IAM** to manage access permissions following the **Least Privilege** principle.
- Using **Security Groups** to control access ports to the Amazon EC2 instance.
- Using **HTTPS** to encrypt data transmitted between users and the system.
- Storing configuration information and API Keys using **Environment Variables**, rather than hardcoding them in the source code.
- Restricting access permissions to **Amazon S3** for backup data.
- MongoDB, PostgreSQL, and MinIO operate exclusively within the internal Docker network and cannot be accessed directly from the Internet.
- Using **Amazon CloudWatch** to monitor operational status and detect system anomalies.

---

## 5.2 Estimated Deployment Cost

The system is deployed following a **Production Lite** model to optimize costs while still meeting requirements for performance, security, and scalability.

### Table 5.1. Estimated Deployment Cost

| AWS Service | Purpose | Estimated Cost (USD/Month) |
|--------------|---------|---------------------------:|
| Amazon EC2 (t3.large) | Application Hosting | 60 |
| Amazon EBS (50 GB) | Persistent Storage | 4 |
| Amazon S3 | Backup Storage | 2 |
| Amazon ECR | Docker Image Registry | 1 |
| Amazon CloudWatch | Monitoring | 3 |
| Data Transfer | Internet Traffic | 8 |
| Google Gemini / OpenAI API | AI Processing | 15–50 |

| | **Estimated Total** | **93–128 USD/Month** |

### Cost Optimization

The platform applies the following cost optimization strategies:

- Deploy all services on a single Amazon EC2 instance during the MVP phase.
- Monitor AWS spending using **AWS Budgets**.
- Store backups on **Amazon S3** instead of maintaining multiple copies on EC2.
- Remove unused AWS resources after testing.
- Optimize AI API requests to reduce token consumption.
- Scale to **Application Load Balancer** and **Amazon ECS** only when user demand increases.

---

# Part 6. Evaluation and Future Development

## 6.1 Evaluation Based on AWS Well-Architected Framework

The AI Learning Assistant Platform is evaluated based on the principles of the **AWS Well-Architected Framework**.

### Table 6.1. System Evaluation

| Pillar | Implementation |
|---------|----------------|
| Operational Excellence | Docker Compose, GitHub Actions, Amazon CloudWatch |
| Security | AWS IAM, Security Group, HTTPS, Environment Variables |
| Reliability | Amazon S3 Backup, Docker Restart Policy, Amazon CloudWatch |
| Performance Efficiency | PostgreSQL + pgvector, Retrieval-Augmented Generation (RAG) |
| Cost Optimization | Amazon EC2, AWS Budgets, Amazon CloudWatch |
| Sustainability | Architecture can be extended to Amazon ECS and Application Load Balancer |

The current architecture satisfies the fundamental principles of the AWS Well-Architected Framework for an AI application deployed on AWS. It is suitable for an MVP while remaining scalable for future development.

> **Figure 6.1. Evaluation of the AI Learning Assistant Platform Based on the AWS Well-Architected Framework.**

![Figure 6.1](/images/6.1.p.r.png)

---

## 6.2 Future Development

In the future, the system can be expanded in the following directions:

- Deploy **Amazon ECS** to enhance scalability.
- Use an **Application Load Balancer** to distribute incoming traffic.
- Expand the Knowledge Base for multiple subjects and users.
- Integrate additional AI models such as **Amazon Bedrock**, **Google Gemini**, or **OpenAI**.
- Add AI features such as AI Tutor, Mindmap, Speech-to-Text, and Text-to-Speech.
- Perfect the Monitoring, Alerting, and Backup system to improve reliability.

With its current architecture, the AI Learning Assistant Platform can effectively meet deployment needs during the MVP phase and is ready to scale as the number of users increases in the future.

# Part 7. Conclusion

## 7.1 Achievements

The AI Learning Assistant Platform was built to support learners in exploiting educational materials through artificial intelligence combined with Retrieval-Augmented Generation (RAG) technology. The system allows users to upload documents, build a Knowledge Base, and interact with AI using natural language, thereby improving the accuracy of responses compared to traditional AI chatbots.

Besides Q&A functionality, the system integrates learning support features such as document management, lesson summarization, quiz generation, Flashcards, and conversation history tracking. The entire application is deployed on Amazon Web Services (AWS), meeting basic requirements for performance, security, scalability, and system management.

Through the project's execution, the following primary objectives were achieved:

- Built an AI Learning Assistant platform based on FastGPT.
- Applied Retrieval-Augmented Generation (RAG) to improve response quality.
- Deployed the system on Amazon EC2 using Docker Compose.
- Integrated MongoDB, PostgreSQL, MinIO, and various AWS services.
- Established a scalable architecture suitable for the MVP phase.

---

## 7.2 Limitations

Although the intended objectives have been met, the system still has some limitations:

- The current architecture uses a single Amazon EC2 instance, so it does not yet meet High Availability requirements.
- Auto Scaling and Load Balancers have not been deployed.
- Response quality remains dependent on the content and quality of the uploaded documents.
- Mobile applications and offline capabilities are not yet supported.
- Some advanced AI features are still in the research and development phase.

---

## 7.3 Future Development

In the future, the AI Learning Assistant Platform will be expanded in the following directions:

- Deploy Amazon ECS or Amazon EKS to improve scalability.
- Use an Application Load Balancer and Auto Scaling to support many concurrent users.
- Integrate additional AI models such as Amazon Bedrock, Google Gemini, or OpenAI.
- Expand learning functionalities such as AI Tutor, Mindmap, Speech-to-Text, and Text-to-Speech.
- Develop applications on Android and iOS platforms.
- Optimize the RAG process to enhance system speed and accuracy.
- Perfect mechanisms for monitoring, backup, and data recovery to increase stability and safety during operations.

These directions will help the AI Learning Assistant Platform become an intelligent learning platform capable of serving diverse user groups and better meeting the needs of modern educational environments.

---

## 7.4 Conclusion

The AI Learning Assistant Platform is a learning support solution utilizing artificial intelligence, built on the FastGPT platform and deployed on Amazon Web Services (AWS). Combining Retrieval-Augmented Generation (RAG) technology with a Knowledge Base allows the system to provide answers closely tied to learning materials, contributing to improved learning efficiency and reducing unfounded information generation by AI.

With an open-architecture design, the system can continue to expand and integrate more AI services as well as AWS services in the future. The project not only fulfills the goal of building an intelligent learning assistant but also establishes a foundation for the research, development, and application of Generative AI in the education sector.

In addition to building a smart learning platform, the project also illustrates how to deploy a Generative AI application on Amazon Web Services using Docker Compose, Amazon EC2, Amazon ECR, GitHub Actions, Amazon S3, Amazon CloudWatch, and AWS security services.