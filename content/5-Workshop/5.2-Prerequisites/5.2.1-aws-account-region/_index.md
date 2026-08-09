---
title: "AWS Account & Region"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---




## Objective

Prepare an **Amazon Web Services (AWS)** account and select the appropriate **AWS Region** before deploying the **AI Learning Assistant Platform**.

Using the same Region for all AWS resources ensures proper communication between services, simplifies deployment, monitoring, and resource management throughout the workshop.

---

## Implementation

Before starting the deployment, sign in to the **AWS Management Console** using an active AWS account.

After signing in successfully, select the Region that will be used throughout the entire workshop.

In this workshop, all resources are deployed in:

**US East (N. Virginia) – us-east-1**

The **us-east-1** Region is selected for the following reasons:

- It supports all AWS services used in this workshop, including Amazon EC2, Amazon ECR, Amazon S3, Amazon CloudWatch, and Amazon SNS.
- It is one of the most widely used AWS Regions and receives new AWS features early.
- It provides high availability and reliability for learning and development environments.
- It is commonly used in AWS documentation, tutorials, and community examples, making troubleshooting easier.

Throughout this workshop, all AWS resources will be created within the same Region to ensure stable communication among services.

---

## Result

The AWS account has been prepared successfully, and the deployment Region has been configured as **US East (N. Virginia) – us-east-1**, which is ready for the next deployment steps.

> **Figure 5.2.1. AWS Management Console and the selected Region.**
> ![Figure 5.2.1](/images/hinh5.2.1.png)