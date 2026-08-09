---
title: "Triển khai AI Learning Assistant"
date: 2026-08-07
weight: 4
chapter: false
pre: " <b> 5.3.4. </b> "
---

## Mục tiêu

Triển khai **AI Learning Assistant Platform** lên máy chủ **Amazon EC2** bằng **Docker Compose**. Nội dung bao gồm việc tải mã nguồn từ GitHub, cấu hình biến môi trường và khởi chạy các Docker Container cần thiết cho hệ thống.

---

## Nội dung thực hiện

### Clone mã nguồn dự án

Trước tiên, tiến hành tải mã nguồn **AI Learning Assistant Platform** từ GitHub Repository về máy chủ EC2.

Thực hiện các lệnh sau:

```bash
# Clone dự án từ GitHub
git clone https://github.com/<YOUR_GITHUB_USER>/AI-Learning-Assistant.git

# Di chuyển vào thư mục dự án
cd AI-Learning-Assistant
```

Sau khi thực hiện thành công, mã nguồn dự án sẽ được lưu trữ trên máy chủ EC2 và sẵn sàng cho bước cấu hình tiếp theo.

---

### Cấu hình biến môi trường

Để bảo vệ các thông tin nhạy cảm như API Key và mật khẩu, hệ thống sử dụng **Environment Variables** thay vì lưu trực tiếp các thông tin này trong mã nguồn.

Sao chép file cấu hình mẫu sang file môi trường cục bộ:

```bash
cp projects/app/.env.template projects/app/.env.local
```

Sau đó mở file **.env.local** để chỉnh sửa:

```bash
nano projects/app/.env.local
```

Trong file **.env.local**, tiến hành cấu hình các biến môi trường cần thiết cho hệ thống, chẳng hạn như:

- Mật khẩu Root.
- OpenAI API Key.
- Các thông tin cấu hình cần thiết khác của ứng dụng.

Sau khi hoàn tất cấu hình, lưu và đóng file **.env.local**.

> **Lưu ý:** Không đưa file **.env.local** chứa API Key, mật khẩu hoặc các thông tin xác thực lên GitHub Repository.

---

### Khởi chạy ứng dụng bằng Docker Compose

Sau khi mã nguồn và các biến môi trường đã được cấu hình, tiến hành khởi chạy hệ thống bằng Docker Compose.

Thực hiện lệnh:

```bash
# Khởi chạy AI Learning Assistant Platform
docker compose -f deploy/dev/docker-compose.yml up -d
```

Tham số `-d` cho phép Docker Compose chạy các container ở chế độ nền (detached mode).

Sau khi quá trình khởi chạy hoàn tất, kiểm tra trạng thái của các Docker Container:

```bash
# Kiểm tra trạng thái các container
docker compose -f deploy/dev/docker-compose.yml ps
```

Các container của hệ thống được mong đợi hiển thị trạng thái **Up** hoặc **Running**.

> **Hình 5.3.7. Trạng thái các Docker Container sau khi triển khai AI Learning Assistant Platform.**

> ![Hình 5.3.7](/images/5.3.7.png)

---

### Kiểm tra hệ thống

Sau khi các Docker Container được khởi chạy thành công, tiến hành kiểm tra khả năng truy cập của hệ thống thông qua trình duyệt Web.

Truy cập địa chỉ **Elastic IP** của Amazon EC2:

```text
http://<ELASTIC_IP>
```

Nếu giao diện **AI Learning Assistant Platform** được hiển thị trên trình duyệt, quá trình triển khai ứng dụng đã hoàn tất thành công.

> **Hình 5.3.8. Giao diện AI Learning Assistant Platform sau khi triển khai trên Amazon EC2.**

> ![Hình 5.3.8](/images/5.3.8.jpg)

---

## Kết quả

Sau khi hoàn thành bước này, mã nguồn **AI Learning Assistant Platform** đã được triển khai trên **Amazon EC2** bằng **Docker Compose**.

Các thành phần của hệ thống được khởi chạy dưới dạng Docker Container và có thể được kiểm tra thông qua lệnh **docker compose ps**. Người dùng có thể truy cập nền tảng thông qua địa chỉ **Elastic IP** của EC2.

Hệ thống đã sẵn sàng để tiếp tục thiết lập quy trình **Continuous Integration & Continuous Deployment (CI/CD)** trong bước tiếp theo.