---
title: "Alerting Configuration"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

## Objective

Set up an **Alerting** system to proactively detect abnormal conditions during the operation of the **AI Learning Assistant Platform**, including high server CPU utilization and AWS costs exceeding the expected budget.

This section uses **Amazon CloudWatch Alarm** to monitor the CPU utilization of the Amazon EC2 instance and **AWS Budgets** to monitor AWS usage costs.

---

## Implementation

### 1. Create a CloudWatch Alarm for CPU Utilization

**Amazon CloudWatch Alarm** is used to detect when the CPU utilization of the Amazon EC2 instance exceeds the configured threshold.

Follow these steps:

1. Access **Amazon CloudWatch**.
2. Select **Alarms**.
3. Select **Create alarm**.
4. Select **Select metric**.
5. Select **EC2 → By Instance Id**.
6. Select the `ai-learning-assistant` instance.
7. Select the **CPUUtilization** metric.
8. Configure the alarm conditions:

```text
Threshold type: Static
Condition: Greater/Equal
Threshold: 80%
Evaluation period: 5 minutes
```

This condition means that CloudWatch will trigger the alarm when the CPU utilization of the EC2 instance reaches or exceeds **80%** during the configured evaluation period.

> **Figure 5.4.3. CPU threshold configuration for the CloudWatch Alarm.**

> ![Figure 5.4.3](/images/5.4.3.png)

---

### 2. Configure Notifications Using Amazon SNS

To receive notifications when the CloudWatch Alarm is triggered, configure **Amazon Simple Notification Service (Amazon SNS)**.

In the **Configure actions** section, perform the following steps:

1. Select the **In alarm** state.
2. Select or create an **SNS Topic**.
3. Enter a personal Email address to receive notifications.
4. Complete the alarm creation process.

After creating the SNS Subscription, AWS will send a confirmation Email to the registered address.

The recipient must confirm the Subscription before receiving notifications from SNS.

> **Note:** Make sure that the Email address used for the SNS Subscription is valid and has been confirmed after creating the Subscription.

---

### 3. Check the CloudWatch Alarm Status

After completing the configuration, access:

**CloudWatch → Alarms**

Check the status of the configured Alarm.

The Alarm can have the following states:

- **OK:** The current Metric value has not exceeded the configured threshold.
- **In alarm:** The alarm condition has been met.
- **Insufficient data:** CloudWatch does not have enough data to determine the alarm state.

Under normal operating conditions, the CPU Alarm is expected to remain in the **OK** state.

> **Figure 5.4.4. CloudWatch Alarm status for the Amazon EC2 instance.**

> ![Figure 5.4.4](/images/5.4.4.png)

---

### 4. Create a Cost Alert Using AWS Budgets

In addition to monitoring server performance, AWS usage costs should also be monitored to prevent unexpected expenses.

Access **AWS Budgets** and create a new budget.

Follow these steps:

1. Access the **AWS Management Console**.
2. Search for and open **AWS Budgets**.
3. Select **Create budget**.
4. Select an appropriate budget type.

The following options can be used:

- **Zero spend budget:** Receive an alert when the account begins to incur charges.
- **Custom budget:** Set a specific monthly budget amount, for example:

```text
Budget amount: $10/month
```

5. Configure the Email address for receiving notifications.
6. Set the cost alert threshold.
7. Review the configuration.
8. Select **Create budget** to complete the setup.

AWS Budgets helps monitor AWS usage and costs, allowing unexpected charges or costs approaching the configured budget threshold to be detected proactively.

> **Figure 5.4.5. AWS Budget configuration and cost alert threshold.**

> ![Figure 5.4.5](/images/5.4.5.png)

---

## Result

After completing this step, the system has been configured with **Alerting** mechanisms to monitor both performance and AWS costs.

Specifically:

- **CloudWatch Alarm** monitors the CPU utilization of the Amazon EC2 instance.
- **Amazon SNS** is used to send Email notifications when the Alarm is triggered.
- **AWS Budgets** is configured to monitor AWS usage costs.
- These alerts help administrators proactively identify resource and cost-related issues.

Combining **Monitoring** and **Alerting** improves the management and operational capabilities of the **AI Learning Assistant Platform** on AWS.