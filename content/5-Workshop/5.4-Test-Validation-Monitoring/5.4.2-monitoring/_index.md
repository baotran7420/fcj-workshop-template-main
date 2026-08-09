---
title: "Monitoring Metrics with Amazon CloudWatch"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

## Objective

Use **Amazon CloudWatch** to monitor the operational metrics of **Amazon EC2**, allowing the status and resource utilization of the server running the **AI Learning Assistant Platform** to be evaluated.

---

## Implementation

### Check Amazon EC2 Metrics

By default, **Amazon EC2** sends basic metrics to **Amazon CloudWatch**, allowing the operational status of the Instance to be monitored without installing additional software on the server.

Follow these steps:

1. Access the **AWS Management Console**.
2. Search for and open **Amazon CloudWatch**.
3. Select **Metrics**.
4. Select **All metrics**.
5. Select **EC2**.
6. Select the appropriate Metrics group for the **Instance**.
7. Find and select the **Instance ID** of the server running the **AI Learning Assistant Platform**.

After selecting the Instance, CloudWatch displays the available Metrics for the server.

The monitored Metrics include:

- **CPU Utilization:** The CPU usage level of the EC2 Instance.
- **Network In:** The amount of network data received by the Instance.
- **Network Out:** The amount of network data sent from the Instance.

These Metrics help monitor the resource utilization of the EC2 Instance and support the detection of abnormal conditions during system operation.

> **Figure 5.4.2. CPU Utilization chart of the Amazon EC2 Instance in Amazon CloudWatch.**

> ![Figure 5.4.2](/images/5.4.2.png)

---

## Result

After configuring and checking **Amazon CloudWatch**, the basic Metrics of the **Amazon EC2** Instance can be monitored directly through the AWS Management Console.

Monitoring **CPU Utilization**, **Network In**, and **Network Out** helps evaluate the operational status of the server and provides a basis for identifying potential resource-related issues during system operation.