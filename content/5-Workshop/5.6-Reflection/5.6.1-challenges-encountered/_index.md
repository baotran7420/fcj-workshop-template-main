---
title: "Challenges"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---



During the deployment of the **AI Learning Assistant Platform**, the team encountered several issues related to server resources and AWS access permissions.

### 1. Out of Memory (OOM)

At the initial stage, the team attempted to deploy the entire system, including the **Application, MongoDB, and PostgreSQL + pgvector**, on low-resource instances such as **t2.micro** or **t3.small**.

However, because the **RAG architecture** and **Vector Database** require a significant amount of memory, the server frequently experienced **Out of Memory (OOM)** issues and crashed.

After identifying the cause, the team upgraded the EC2 Instance to **t3.large** to provide additional CPU and memory resources, allowing the system to operate more reliably.

Through this issue, the team learned that selecting the appropriate **Instance Type** should be based on the actual resource requirements of the application rather than focusing only on using a low-cost configuration.

### 2. IAM Permission Issue

During the configuration of **GitHub Actions**, the team encountered an **Access Denied** error when the Workflow attempted to perform operations on **Amazon ECR**.

After reviewing the IAM configuration, the team identified that the IAM User did not have sufficient permissions required to perform ECR-related operations.

The team then added the appropriate permissions and applied the **Least Privilege** principle by granting only the permissions required for the deployment process.

After updating the permissions, GitHub Actions was able to perform the required ECR operations and continue the CI/CD process successfully.

Through this issue, the team gained a better understanding of the importance of **IAM Permissions** and the **Least Privilege** principle in securing AWS resources.