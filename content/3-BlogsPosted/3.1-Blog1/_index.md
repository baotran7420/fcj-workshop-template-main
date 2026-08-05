---
title: "Blog 1"
date: 2026-07-16
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#  I Lost 47.77 USD in AWS Credits Because of a Forgotten Amazon RDS Instance

While learning AWS and completing hands-on labs, I encountered an experience that many beginners in Cloud computing may also face.

Initially, I received **100 USD in AWS Credits** to learn and practice with AWS services. After completing **five additional AWS hands-on tasks**, I earned **another 100 USD in AWS Credits**, giving me a total of **200 USD in AWS Credits**. I was confident that this amount would be sufficient for my entire learning journey on AWS.

However, after finishing several lab exercises, I checked **AWS Billing** and was surprised to find that **27 USD** had already been deducted. Thinking I had simply forgotten to delete a few resources, I carefully reviewed my **Amazon EC2** instances, **AWS Lambda** functions, **Amazon VPC**, **Amazon S3**, and other AWS services. What I discovered later was the real reason why my total AWS Credits loss eventually reached **47.77 USD**.

To my surprise, the next day my AWS bill increased again, and the total cost eventually reached **47.77 USD**.

After investigating AWS Billing and AWS Cost Explorer in detail, I discovered the real cause: **an Amazon RDS instance was still running**, even though it was no longer being used by any application.

This experience taught me an important lesson: **in the cloud, resources continue to generate costs as long as they remain active—even if no one is using them.**

---

## What I Learned from the AWS Enterprise Strategy Blog

After this incident, I read the AWS Enterprise Strategy Blog article **"Money Matters: Four Methods to Unlock Investment Capacity in IT."**

One idea particularly resonated with me:

> **Cost Optimization is not simply about reducing costs—it is about eliminating spending that no longer creates business value.**

Looking back at my own environment, I realized that my Amazon RDS instance:

- Had no active application connected.
- Had no incoming traffic.
- Delivered no business value.

However, it continued consuming AWS Credits every day.

This is a perfect example of **Cloud Waste**—resources that continue to incur costs without providing any value.

---

## Solution

To avoid repeating the same mistake, I decided to implement an automated solution recommended by AWS for development and testing environments.

The architecture consists of:

- **Amazon EventBridge** to schedule database operations.
- **AWS Lambda** to automatically start and stop the Amazon RDS instance.
- **IAM Role** to grant Lambda the required permissions.
- **Amazon CloudWatch Logs** to monitor execution and troubleshoot issues.

With this approach, the database only runs during working hours instead of operating 24/7.

---

## Benefits

* Prevents forgotten Amazon RDS instances from running continuously.
* Reduces costs for development and testing environments.
* Eliminates repetitive manual operations.
* Provides execution logs through Amazon CloudWatch.
* Follows AWS Cost Optimization best practices.

---

## Lessons Learned

This experience completely changed how I think about using AWS.

Previously, I focused mainly on deploying cloud resources.

Now I understand that **managing the lifecycle of cloud resources is just as important as deploying them.**

A forgotten Amazon RDS instance may seem insignificant, but it can continuously generate unnecessary costs.

By combining **Amazon EventBridge**, **AWS Lambda**, and **Amazon RDS**, I can automate routine operations, reduce operational risks, and optimize cloud spending.

More importantly, this experience reminded me that **Cost Optimization should be considered during system design—not after receiving the monthly AWS bill.**

---

## Architecture

### Figure 1. Amazon RDS Running Continuously Causes Unexpected Costs

![Figure 1](/images/hinh1.png)

### Figure 2. Automated Amazon RDS Start/Stop Architecture

![Figure 2](/images/hinh2.png)

### Figure 3. Automated Workflow

![Figure 3](/images/hinh3.png)

### Figure 4. Daily Amazon RDS Schedule

![Figure 4](/images/hinh4.png)

---

## References

 **Original articles and documentation that inspired this blog:**

- **Money Matters: Four Methods to Unlock Investment Capacity in IT**  
  AWS Enterprise Strategy Blog  
  https://aws.amazon.com/blogs/enterprise-strategy/it-money-matters-four-methods-to-unlock-investment-capacity/

- **Schedule Amazon RDS Stop and Start Using AWS Lambda**  
  AWS Database Blog  
  https://aws.amazon.com/vi/blogs/database/schedule-amazon-rds-stop-and-start-using-aws-lambda/

- **AWS Well-Architected Framework – Cost Optimization Pillar**  
  https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html

  ## Article link
  https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2215517809213179&notif_id=1784349094559062&notif_t=feedback_reaction_generic&ref=notif