---
title: "Thiết lập hạ tầng"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---


## Mục tiêu

Chuẩn bị các thành phần hạ tầng cơ bản trước khi khởi tạo máy chủ **Amazon EC2**, bao gồm tạo **Key Pair** để xác thực kết nối SSH và cấu hình **Security Group** nhằm kiểm soát lưu lượng mạng ra vào hệ thống.

---

## Nội dung thực hiện

### Tạo Key Pair

Trước khi khởi tạo EC2 Instance, cần tạo một **Key Pair** để phục vụ quá trình xác thực khi kết nối đến máy chủ thông qua giao thức SSH.

Các bước thực hiện:

1. Truy cập **Amazon EC2 Console**.
2. Chọn **Key Pairs** trong thanh điều hướng bên trái.
3. Chọn **Create Key Pair**.
4. Đặt tên Key Pair, ví dụ: **fastgpt-key**.
5. Chọn định dạng **.pem** để sử dụng với OpenSSH.
6. Tải tệp Key Pair về máy tính và lưu trữ tại vị trí an toàn.

> **Hình 5.3.1. Danh sách Key Pair đã tạo trên Amazon EC2.**

> ![Hình 5.3.1](/images/5.3.1.png)

---

### Cấu hình Security Group

Sau khi tạo Key Pair, tiến hành tạo **Security Group** để kiểm soát lưu lượng truy cập đến EC2 Instance.

Các bước thực hiện:

1. Chọn **Security Groups** trong Amazon EC2 Console.
2. Chọn **Create Security Group**.
3. Đặt tên Security Group, ví dụ: **fastgpt-ssg**.
4. Cấu hình các **Inbound Rules** như sau:

| Type | Port | Source | Mục đích |
|------|------|--------|----------|
| HTTP | 80 | 0.0.0.0/0 | Cho phép truy cập Website. |
| HTTPS | 443 | 0.0.0.0/0 | Cho phép truy cập Website qua HTTPS. |
| SSH | 22 | My IP | Chỉ cho phép máy quản trị kết nối đến EC2. |

Security Group hoạt động như một **Virtual Firewall**, giúp giới hạn các kết nối đến máy chủ và chỉ mở những cổng cần thiết phục vụ quá trình triển khai và vận hành hệ thống.

> **Hình 5.3.2. Cấu hình Inbound Rules của Security Group.**

> ![Hình 5.3.2](/images/5.3.2.png)

---

## Kết quả

Sau khi hoàn thành bước này, hệ thống đã có **Key Pair** phục vụ kết nối SSH và **Security Group** được cấu hình với các quy tắc mạng phù hợp, sẵn sàng cho việc khởi tạo Amazon EC2 Instance trong bước tiếp theo.