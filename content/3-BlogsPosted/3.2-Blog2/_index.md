---

title: "Blog 2"
date: 2026-08-03
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
----------------------

#  All Docker Containers Are Running, but the Website Is Still Inaccessible! My First Lesson from Deploying an AI Learning Assistant on AWS EC2

Hello everyone! 

During the development of our **AI Learning Assistant** project, I deployed the system on **Amazon EC2** using **Docker Compose**. I initially thought that the website would work as long as all the containers started successfully. However, the reality was not that simple.

---

## System Deployment Architecture

The diagram below illustrates the architecture of our **AI Learning Assistant**, deployed on **Amazon EC2** using **Docker Compose**.

The system follows a **multi-container architecture**, in which each component has a specific responsibility:

* **Nginx** acts as a reverse proxy, receiving user requests and forwarding them to the appropriate backend services.
* **FastGPT Web** provides the user interface.
* **FastGPT API** processes requests and coordinates the system’s business logic.
* **MongoDB** stores the application data.
* **PostgreSQL** manages relational data.
* **Redis** is used for caching and session storage.
* **Sandbox** executes AI-generated code in an isolated environment.
* **AI Models (OpenAI, Gemini, Ollama, etc.)** provide natural language processing capabilities.

All services are deployed with **Docker Compose** on a single **Amazon EC2 instance**.

### Figure 1. AI Learning Assistant Deployment Architecture

![Figure 1](/images/docker1.png)

---

## The Problem I Encountered

After completing the deployment, I checked the system and found that all containers were in the **Running** state. The application also responded normally when tested directly from the EC2 instance.

However, when I opened a browser and accessed the website through the EC2 instance’s **Public IP address**, the browser displayed the following message:

> **“This site can’t be reached”**

At first, I thought the problem was related to Docker or the application. I spent a considerable amount of time checking the Docker Compose configuration, container logs, and source code, but I could not find the cause.

## Troubleshooting Process

Instead of randomly changing the configuration, I decided to inspect each layer of the system in a logical order.

I checked the following:

*  Was the application running?
*  Were the Docker containers operating correctly?
*  Was the port mapping configured correctly?

After confirming that none of these three areas contained errors, I continued checking the AWS infrastructure.

Eventually, I discovered that the problem was not related to Docker or the application. It was caused by the **Amazon EC2 Security Group**.

## Root Cause

At that time, the Security Group only allowed connections through:

* SSH (Port **22**)

Meanwhile, the two ports required to access the website had not been opened:

* HTTP (Port **80**)
* HTTPS (Port **443**)

This meant that:

* The application was running normally.
* Docker was operating without errors.
* The EC2 instance was working correctly.
* However, AWS was blocking all incoming HTTP and HTTPS traffic from the Internet.

Only after I added inbound rules allowing access through **HTTP (80)** and **HTTPS (443)** did the website become accessible from outside the EC2 instance.

## Lessons Learned

This experience taught me that when deploying an application on AWS, I should not focus only on Docker or the source code.

The entire system should be checked layer by layer:

1. Is the application running?
2. Are the Docker containers operating correctly?
3. Is the port mapping configured properly?
4. Does the Security Group allow traffic through the required ports?
5. Is the Nginx reverse proxy configured correctly?
6. Are the domain and DNS records pointing to the correct destination?

Following this troubleshooting order helped me identify the cause much faster than randomly changing the configuration.

From this experience, I learned that:

> **An application running successfully inside an EC2 instance does not necessarily mean that external users can access it. When deploying on AWS, the application, Docker environment, and network infrastructure must all be checked to ensure that the system works correctly.**

---

## References

 **AWS documentation referenced in this article:**

* **Amazon EC2 Security Groups**
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html

* **Amazon EC2 Networking and Security**
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html

## Article Link

https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2233426700755623&notif_id=1785770202368739&notif_t=feedback_reaction_generic&ref=notif