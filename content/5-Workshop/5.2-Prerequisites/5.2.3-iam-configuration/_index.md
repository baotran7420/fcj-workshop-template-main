---
title: "IAM Configuration"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.2.3. </b> "
---


## Objective

Configure AWS access permissions to support the deployment and management of the **AI Learning Assistant Platform** while following AWS security best practices.

---

## Implementation

AWS recommends avoiding the use of the **Root Account** for daily deployment and operational tasks. Instead, each team member should use a dedicated **IAM User** to access and manage AWS resources.

In this workshop, two IAM Users were created for the two team members participating in the project. In addition, a separate IAM User was created for **GitHub Actions** to support the CI/CD automation workflow.

To simplify the hands-on deployment process and avoid permission-related issues during the workshop, the IAM Users were assigned the **AdministratorAccess** policy. In production environments, AWS recommends following the **Principle of Least Privilege**, where users are granted only the permissions required for their specific tasks.

The following security practices were also applied:

- Do not use the Root Account for routine deployment activities.
- Never store **Access Key ID** or **Secret Access Key** directly in the application source code.
- Never commit AWS credentials to a GitHub repository.
- Store sensitive credentials securely using **GitHub Secrets** when configuring the CI/CD pipeline.

---

## IAM Configuration Process

The IAM configuration was performed using the following steps:

1. Sign in to the **AWS Management Console**.
2. Open the **AWS Identity and Access Management (IAM)** service.
3. Select **Users** and create an IAM User for each team member.
4. Attach the **AdministratorAccess** policy to the IAM Users used during the workshop.
5. Review the list of IAM Users and verify the assigned permissions.

---

## Result

The IAM Users were created and configured successfully, providing secure access for deploying and managing the AWS resources of the **AI Learning Assistant Platform**.

> **Figure 5.2.3. IAM Users created for the workshop.**
> ![Figure 5.2.3](/images/5.2.3.png)

> **Figure 5.2.4. Permissions attached to the IAM User.**
> ![Figure 5.2.4](/images/5.2.4.png)