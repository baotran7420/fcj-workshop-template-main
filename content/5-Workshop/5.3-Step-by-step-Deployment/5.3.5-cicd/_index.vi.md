---
title: "Continuous Integration & Continuous Deployment"
date: 2026-08-07
weight: 5
chapter: false
pre: " <b> 5.3.5. </b> "
---

## Mục tiêu

Thiết lập quy trình **Continuous Integration & Continuous Deployment (CI/CD)** sử dụng **GitHub Actions** và **Amazon Elastic Container Registry (Amazon ECR)** nhằm tự động hóa quá trình xây dựng, lưu trữ và triển khai **AI Learning Assistant Platform**.

Quy trình CI/CD cho phép hệ thống tự động cập nhật phiên bản ứng dụng mỗi khi có mã nguồn mới được đẩy lên nhánh `main` của GitHub Repository.

---

## Nội dung thực hiện

### Khởi tạo Amazon ECR Repository

**Amazon Elastic Container Registry (Amazon ECR)** được sử dụng để lưu trữ và quản lý các Docker Image của AI Learning Assistant Platform.

Các bước thực hiện:

1. Truy cập **AWS Management Console**.
2. Tìm kiếm và mở dịch vụ **Amazon Elastic Container Registry (ECR)**.
3. Chọn **Repositories**.
4. Chọn **Create repository**.
5. Đặt tên Repository: **ai-learning-aassistant**
6. Chọn chế độ **Private**.
7. Chọn **Create repository**.

Sau khi Repository được tạo thành công, Amazon ECR sẽ cung cấp **Repository URI** được sử dụng trong quá trình GitHub Actions đẩy Docker Image lên ECR.

> **Hình 5.3.9. Amazon ECR Repository của AI Learning Assistant Platform.**

> ![Hình 5.3.9](/images/5.3.9.png)

---

### Cấu hình GitHub Secrets

GitHub Actions cần các thông tin xác thực và thông tin triển khai để có thể truy cập tài nguyên AWS và máy chủ EC2.

Để bảo vệ các thông tin nhạy cảm, các giá trị này được lưu trữ bằng **GitHub Secrets** thay vì ghi trực tiếp vào file workflow.

Các bước thực hiện:

1. Truy cập **GitHub Repository** của dự án.
2. Chọn **Settings**.
3. Chọn **Secrets and variables**.
4. Chọn **Actions**.
5. Chọn **New repository secret**.

Cấu hình các Secret cần thiết:

| Secret | Mục đích |
|--------|----------|
| **AWS_ACCESS_KEY_ID** | Access Key được GitHub Actions sử dụng để truy cập AWS |
| **AWS_SECRET_ACCESS_KEY** | Secret Key được GitHub Actions sử dụng để xác thực với AWS |
| **EC2_HOST** | Elastic IP của EC2 Instance |
| **EC2_USERNAME** | Username dùng để kết nối đến EC2 Instance |
| **EC2_SSH_KEY** | Private SSH Key dùng để truy cập EC2 |

Thông tin xác thực AWS được sử dụng trong quy trình CI/CD được tạo và cấu hình từ phần **IAM Configuration** ở bước trước.

Đối với quá trình triển khai lên EC2:

```text
EC2_HOST = Elastic IP của EC2
EC2_USERNAME = ubuntu
```

**EC2_SSH_KEY** chứa private SSH key được sử dụng để GitHub Actions thiết lập kết nối SSH đến EC2 Instance.

> **Lưu ý bảo mật:** Không commit AWS Credentials, Private SSH Key, API Key, Password hoặc các thông tin nhạy cảm khác trực tiếp vào GitHub Repository.

> **Hình 5.3.10. GitHub Repository Secrets được cấu hình cho quy trình CI/CD.**

> ![Hình 5.3.10](/images/5.3.10.png)

---

### Cấu hình GitHub Actions Workflow

Sau khi cấu hình GitHub Secrets, tạo file workflow cho GitHub Actions tại:

```text
.github/workflows/deploy-aws.yml
```

Workflow chịu trách nhiệm tự động xây dựng Docker Image, đẩy Image lên Amazon ECR và triển khai phiên bản mới nhất lên Amazon EC2.

Quy trình hoạt động tổng quát:

```text
Git Push
   |
   v
GitHub Actions
   |
   v
Build Docker Image
   |
   v
Amazon ECR
   |
   v
Deploy to Amazon EC2
   |
   v
Updated Application
```

Workflow được kích hoạt mỗi khi có mã nguồn mới được push lên nhánh `main`.

Ví dụ cấu trúc workflow:

```yaml
name: Deploy AI Learning Assistant

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      - name: Login to Amazon ECR
        uses: aws-actions/amazon-ecr-login@v2

      - name: Build Docker Image
        run: |
          docker build -t ai-learning-assistant .

      - name: Tag Docker Image
        run: |
          docker tag ai-learning-assistant:latest \
            <ECR_REPOSITORY_URI>:latest

      - name: Push Docker Image to Amazon ECR
        run: |
          docker push <ECR_REPOSITORY_URI>:latest

      - name: Deploy to Amazon EC2
        run: |
          ssh -i "${{ secrets.EC2_SSH_KEY }}" \
            -o StrictHostKeyChecking=no \
            ${{ secrets.EC2_USERNAME }}@${{ secrets.EC2_HOST }} \
            "cd ~/AI-Learning-Assistant && git pull && docker compose up -d"
```

> **Lưu ý:** Thay **<ECR_REPOSITORY_URI>** bằng URI thực tế của Amazon ECR Repository đã tạo ở bước trước.

---

### Chạy quy trình CI/CD

Sau khi thêm file workflow vào Repository, commit và push các thay đổi lên nhánh `main`.

Ví dụ:

```bash
git add .
git commit -m "Configure AWS CI/CD pipeline"
git push origin main
```

Sau khi mã nguồn được push thành công, GitHub Actions sẽ tự động phát hiện commit mới và bắt đầu thực hiện workflow.

Quy trình thực hiện bao gồm:

1. Checkout mã nguồn mới nhất từ GitHub.
2. Cấu hình AWS Credentials.
3. Đăng nhập vào Amazon ECR.
4. Build Docker Image.
5. Tag Docker Image.
6. Push Docker Image lên Amazon ECR.
7. Kết nối đến Amazon EC2.
8. Triển khai phiên bản ứng dụng mới.

Có thể theo dõi quá trình thực thi bằng cách truy cập:

**GitHub Repository → Actions**

Nếu tất cả các bước được thực hiện thành công, GitHub Actions sẽ hiển thị trạng thái **Success** màu xanh.

> **Hình 5.3.11. GitHub Actions Workflow thực hiện thành công.**

> ![Hình 5.3.11](/images/5.3.11.png)

---

## Kết quả

Sau khi hoàn thành bước này, quy trình **Continuous Integration & Continuous Deployment (CI/CD)** đã được thiết lập bằng **GitHub Actions** và **Amazon ECR**.

Mỗi khi có mã nguồn mới được push lên nhánh `main`, GitHub Actions sẽ tự động build Docker Image, push Image lên Amazon ECR và triển khai phiên bản mới của ứng dụng lên Amazon EC2.

Quy trình tự động này giúp giảm các thao tác triển khai thủ công, đảm bảo quá trình cập nhật ứng dụng được thực hiện nhất quán và thuận tiện hơn.

Hệ thống CI/CD đã sẵn sàng để được kiểm tra và đánh giá trong các bước tiếp theo.