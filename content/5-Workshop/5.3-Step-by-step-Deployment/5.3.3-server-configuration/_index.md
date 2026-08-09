---
title: "Server Configuration"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---

## Objective

Set up the environment on **Amazon EC2** to prepare for the deployment of the **AI Learning Assistant Platform**, including connecting to the server, updating the operating system, and installing the necessary tools such as Docker, Docker Compose, Git, and AWS CLI.

---

## Implementation

### Connecting to Amazon EC2

After the EC2 Instance has been successfully launched and assigned an **Elastic IP**, connect to the server using **EC2 Instance Connect** through the AWS Management Console.

Follow these steps:

1. Open the **Amazon EC2 Console**.
2. Select **Instances**.
3. Select the EC2 Instance **ai-learning-aassistant**.
4. Click **Connect**.
5. Select **EC2 Instance Connect**.
6. Click **Connect** to open the Terminal directly in the web browser.

EC2 Instance Connect allows the user to access the server directly through a web browser without requiring the private key **.pem** file to be stored or used on the local computer.

> **Figure 5.3.5. Successful connection to Amazon EC2 using EC2 Instance Connect.**
>
> ![Figure 5.3.5](/images/5.3.5.png)

---

### Environment Setup

After successfully connecting to the EC2 Instance, update the operating system and install the necessary tools for the deployment process.

Run the following commands:

```bash
# Update package information
sudo apt update && sudo apt upgrade -y

# Install Docker, Docker Compose, Git and AWS CLI
sudo apt install -y docker.io docker-compose-v2 git awscli

# Allow the ubuntu user to run Docker without sudo
sudo usermod -aG docker ubuntu

# Apply the new group
newgrp docker

# Verify Docker installation
docker --version

# Verify Docker Compose installation
docker compose version

# Verify Git installation
git --version

# Verify AWS CLI installation
aws --version
```

After completing the installation, verify the Docker and Docker Compose versions to confirm that the environment has been configured successfully.

> **Figure 5.3.6. Docker, Docker Compose, Git, and AWS CLI successfully installed on Amazon EC2.**

> ![Figure 5.3.6](/images/5.3.6.png)

---

## Result

After completing this step, the **Amazon EC2** environment has been successfully configured with all the necessary components, including **Docker, Docker Compose, Git, and AWS CLI**. The server is now ready to deploy the **AI Learning Assistant Platform** in the next step.