---
title: "Launch Amazon EC2"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

## Objective

Launch an **Amazon EC2 Instance** to host the **AI Learning Assistant Platform** and assign an **Elastic IP** to provide a static public IP address for system access and management.

---

## Implementation

### Launch an Amazon EC2 Instance

Sign in to the **Amazon EC2 Console**, then select **Launch Instance** to create a new virtual server.

The EC2 Instance used in this workshop is configured as follows:

| Property | Value |
|----------|-------|
| Name | AI Learning Assistant |
| Amazon Machine Image (AMI) | Ubuntu Server 22.04 LTS |
| Instance Type | t3.large |
| Key Pair | AWS |
| Security Group | launch-wizard-2 |
| Storage | 50 GB (gp3) |

After completing the configuration, choose **Launch Instance** to create the EC2 instance.

> **Figure 5.3.3. Amazon EC2 instance configuration.**

> ![Figure 5.3.3](/images/5.3.3ws.png)

---

### Assign an Elastic IP

After the EC2 instance has been launched successfully, assign an **Elastic IP** to provide a static public IP address for the server.

Perform the following steps:

1. Open **Elastic IPs** in the Amazon EC2 Console.
2. Choose **Allocate Elastic IP Address**.
3. Select **Allocate** to create a new Elastic IP.
4. Select the allocated Elastic IP.
5. Choose **Actions → Associate Elastic IP Address**.
6. Select the target EC2 instance and confirm the association.

Using an Elastic IP ensures that the public IP address remains unchanged even after the EC2 instance is stopped and restarted, making it easier to access the application and configure DNS settings.

> **Figure 5.3.4. Elastic IP associated with the Amazon EC2 instance.**

> ![Figure 5.3.4](/images/5.3.4.png)

---

## Result

After completing this step, an **Amazon EC2 Instance** has been launched successfully and associated with an **Elastic IP**. The server is now ready for environment configuration and deployment of the **AI Learning Assistant Platform** in the following steps.