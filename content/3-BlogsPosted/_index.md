---
title: "Blog Posted"
date: 2026-07-16
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



During my internship, I researched official AWS Blog articles and combined them with my own hands-on experience to write technical blog posts. These articles summarize what I learned, share practical experiences, and introduce AWS architectures and best practices to the community.

The following are the blog posts I have published on the **AWS Study Group**:


###  [Blog 1 - I Lost 47.77 USD in AWS Credits Because of a Forgotten Amazon RDS Instance](3.1-Blog1/)
This blog shares my real-world experience of losing 47.77 USD in AWS Credits because of a forgotten Amazon RDS instance that continued running after completing AWS hands-on labs. It explains how unmanaged cloud resources can become Cloud Waste and introduces an automated cost optimization solution using Amazon EventBridge, AWS Lambda, Amazon RDS, and Amazon CloudWatch to schedule database start and stop operations. The blog also highlights the importance of incorporating Cost Optimization into cloud architecture from the beginning, following AWS Well-Architected Framework best practices.

###  [Blog 2 -  All Docker Containers Are Running, but the Website Is Still Inaccessible! My First Lesson from Deploying an AI Learning Assistant on AWS EC2
](3.2-Blog2/)
This blog describes an issue encountered while deploying the AI Learning Assistant on Amazon EC2 using Docker Compose. Although all containers were running correctly, the website remained inaccessible because the Security Group did not allow HTTP traffic on port 80 or HTTPS traffic on port 443. The article emphasizes checking the application, Docker containers, port mapping, Security Group, Nginx, and DNS systematically when troubleshooting deployment issues.

###  [Blog 3 -  Documents Uploaded Successfully, But the AI Still Answered Incorrectly – Lessons Learned About RAG and Knowledge Bases When Building an AI Learning Assistant](3.3-Blog3/)
This blog explains why an AI assistant may provide incorrect answers even after documents have been successfully uploaded to its Knowledge Base. The cause was related to the RAG pipeline, including text extraction, chunking, embedding, vector storage, retrieval, and prompt configuration. After optimizing document indexing, retrieval settings, and the system prompt, the AI produced more accurate answers and significantly reduced hallucinations.