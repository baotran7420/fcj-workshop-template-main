---
title: " Triển khai chi tiết từng bước"
weight: 3
chapter: false
pre: "<b>5.3.</b>"
---



Trong phần này, người thực hiện sẽ triển khai **AI Learning Assistant Platform** trên nền tảng **Amazon Web Services (AWS)** theo từng bước, từ việc chuẩn bị hạ tầng, khởi tạo máy chủ, cấu hình môi trường, triển khai ứng dụng cho đến thiết lập quy trình **Continuous Integration & Continuous Deployment (CI/CD)**.

Các bước được sắp xếp theo đúng trình tự triển khai thực tế nhằm giúp hệ thống được cài đặt, cấu hình và vận hành một cách ổn định.

---

## Nội dung

Workshop này bao gồm các bước triển khai sau:

###   [1. Thiết lập hạ tầng](./5.3.1-infrastructure-setup)

- Tạo Key Pair.
- Cấu hình Security Group.
- Mở các cổng cần thiết (22, 80 và 443).

---

### [2. Khởi tạo Amazon EC2 ](./5.3.2-launch-amazon-ec2) 

- Khởi tạo EC2 Instance.
- Gán Elastic IP.
- Kết nối đến EC2 thông qua SSH.


---

### [3. Cấu hình máy chủ](./5.3.3-server-configuration)

- Cập nhật hệ điều hành Ubuntu.
- Cài đặt Docker.
- Cài đặt Docker Compose.


---

###  [4. Triển khai AI Learning Assistant](./5.3.4-deploy-ai-learning-assistant)

- Clone mã nguồn từ GitHub.
- Cấu hình tệp `.env`.
- Triển khai bằng Docker Compose.
- Kiểm tra các Docker Containers.
- Cấu hình Nginx.
- Kiểm tra khả năng truy cập hệ thống.

---

### [5. Continuous Integration & Continuous Deployment](./5.3.5-continuous-integration-continuous-deployment)

- Tạo Amazon ECR Repository.
- Cấu hình GitHub Secrets.
- Thiết lập GitHub Actions.
- Build và Push Docker Images.
- Tự động triển khai lên Amazon EC2.

