---
title: "Cấu hình máy chủ"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.3.3. </b> "
---


## Mục tiêu

Thiết lập môi trường trên **Amazon EC2** để sẵn sàng triển khai **AI Learning Assistant Platform**, bao gồm kết nối đến máy chủ, cập nhật hệ điều hành và cài đặt các công cụ cần thiết như Docker, Docker Compose, Git và AWS CLI.

---

## Nội dung thực hiện

### Kết nối đến Amazon EC2

Sau khi EC2 Instance được khởi tạo và gán **Elastic IP**, tiến hành kết nối đến máy chủ thông qua **EC2 Instance Connect** trên AWS Management Console.

Các bước thực hiện:

1. Truy cập **Amazon EC2 Console**.
2. Chọn **Instances**.
3. Chọn EC2 Instance **ai-learning-assistant**.
4. Chọn **Connect**.
5. Chọn **EC2 Instance Connect**.
6. Chọn **Connect** để mở Terminal trực tiếp trên trình duyệt.

EC2 Instance Connect cho phép người thực hiện truy cập vào máy chủ thông qua trình duyệt mà không cần sử dụng trực tiếp file private key **.pem** trên máy tính cá nhân.

> **Hình 5.3.5. Kết nối thành công đến Amazon EC2 bằng EC2 Instance Connect.**
> ![Hình 5.3.5](/images/5.3.5.png)

---

### Cài đặt môi trường

Sau khi đăng nhập thành công vào EC2 Instance, cập nhật hệ điều hành và cài đặt các công cụ cần thiết.

Thực hiện các lệnh sau:

```bash
# Update package information
sudo apt update && sudo apt upgrade -y

# Install Docker, Docker Compose, Git and AWS CLI
sudo apt install -y docker.io docker-compose-v2 git awscli

# Allow the ubuntu user to run Docker without sudo
sudo usermod -aG docker ubuntu

# Apply the new group
newgrp docker

# Verify Docker installation
docker --version

# Verify Docker Compose installation
docker compose version

# Verify Git installation
git --version

# Verify AWS CLI installation
aws --version
```

Sau khi cài đặt hoàn tất, kiểm tra phiên bản Docker và Docker Compose để xác nhận môi trường đã được cấu hình thành công.

> **Hình 5.3.6. Kết quả cài đặt Docker trên Amazon EC2.**

> ![Hình 5.3.6](/images/5.3.6.png)

---

## Kết quả

Sau khi hoàn thành bước này, Amazon EC2 đã được cấu hình với đầy đủ các thành phần cần thiết, bao gồm Docker, Docker Compose, Git và AWS CLI. Máy chủ đã sẵn sàng để triển khai AI Learning Assistant Platform trong bước tiếp theo.