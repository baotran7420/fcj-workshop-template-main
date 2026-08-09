---
title: "Future Enhancements"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

If the project is upgraded from the **MVP** version to an **Enterprise Production** environment, the current architecture using a single **Amazon EC2** instance should be restructured to improve scalability, availability, and system manageability.

### 1. Migrate to Amazon ECS / EKS

Instead of running all Docker Containers directly on a single EC2 Instance, the system can be deployed on a Cluster using **Amazon ECS** or **Amazon EKS**.

In particular, **Amazon ECS with AWS Fargate** allows Docker Containers to run without directly managing EC2 servers.

This approach can help the system:

- Automatically scale resources when traffic increases.
- Distribute workloads across multiple Containers.
- Improve system availability.
- Reduce manual server management.

### 2. Separate the Databases

In the current architecture, the Databases are deployed together with the application using Docker Compose.

In the future, the Databases can be migrated to AWS **Managed Services**, such as:

- **Amazon RDS for PostgreSQL** for PostgreSQL.
- **Amazon DocumentDB** for MongoDB-compatible workloads.

Using Managed Services can reduce database administration tasks and provide capabilities such as **Backup, Monitoring, and High Availability (Multi-AZ)** depending on the selected configuration.

### 3. Use an Application Load Balancer

An **Application Load Balancer (ALB)** can be placed in front of the system to distribute incoming traffic across multiple Application Servers or Containers.

The ALB can be integrated with **AWS Certificate Manager (ACM)** to manage certificates and provide **SSL/TLS (HTTPS)** connections.

This architecture is more suitable when the system is expanded to multiple EC2 Instances or multiple Application Containers.

---

## Development Direction

These improvements would allow the **AI Learning Assistant Platform** to evolve from a simple deployment on a single EC2 Instance into a more scalable architecture suitable for a Production environment.

The main development directions focus on three key aspects:

- **Scalability:** Ability to scale the system as the number of users increases.
- **High Availability:** Reduce system downtime and service interruptions.
- **Manageability:** Reduce manual administration and increase automation.