---
title: "Infrastructure Setup"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

## Objective

Prepare the basic infrastructure required before launching an **Amazon EC2** instance by creating a **Key Pair** for SSH authentication and configuring a **Security Group** to control inbound network traffic.

---

## Implementation

### Create a Key Pair

Before launching the EC2 instance, create a **Key Pair** that will be used for SSH authentication.

Steps:

1. Open the **Amazon EC2 Console**.
2. Select **Key Pairs** from the left navigation pane.
3. Choose **Create Key Pair**.
4. Enter a name, for example: **fastgpt-key**.
5. Select the **.pem** file format for OpenSSH.
6. Download the key file and store it in a secure location.

> **Figure 5.3.1. Key Pair in Amazon EC2.**

> ![Figure 5.3.1](/images/5.3.1.png)

---

### Configure the Security Group

After creating the Key Pair, create a **Security Group** to control inbound traffic to the EC2 instance.

Steps:

1. Open **Security Groups** in the Amazon EC2 Console.
2. Choose **Create Security Group**.
3. Enter a name, for example: **fastgpt-sg**.
4. Configure the following **Inbound Rules**:

| Type | Port | Source | Purpose |
|------|------|--------|---------|
| HTTP | 80 | 0.0.0.0/0 | Allow web traffic. |
| HTTPS | 443 | 0.0.0.0/0 | Allow secure web traffic. |
| SSH | 22 | My IP | Allow SSH access only from the administrator's computer. |

The Security Group acts as a **virtual firewall**, allowing only the required network traffic to reach the EC2 instance.

> **Figure 5.3.2. Security Group inbound rule configuration.**

> ![Figure 5.3.2](/images/5.3.2.png)

---

## Result

After completing this step, a **Key Pair** has been created for SSH access, and a **Security Group** has been configured with the required inbound rules. The environment is now ready for launching an Amazon EC2 instance in the next step.

Theo mình, từ 5.3.1 trở đi bạn nên giữ thống nhất cấu trúc: