---
title: "Khởi chạy Amazon EC2"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---


## Mục tiêu

Khởi tạo một **Amazon EC2 Instance** làm máy chủ triển khai **AI Learning Assistant Platform** và gán **Elastic IP** để đảm bảo hệ thống có địa chỉ IP tĩnh phục vụ việc truy cập và quản lý.

---

## Nội dung thực hiện

### Khởi tạo Amazon EC2 Instance

Đăng nhập vào **Amazon EC2 Console**, sau đó chọn **Launch Instance** để tạo một máy chủ mới.

Trong workshop này, EC2 Instance được cấu hình như sau:

| Thuộc tính | Giá trị |
|------------|----------|
| Name | AI Learning Assistant |
| Amazon Machine Image (AMI) | Ubuntu Server 22.04 LTS |
| Instance Type | t3.large |
| Key Pair | AWS |
| Security Group | launch-wizard-2 |
| Storage | 50 GB (gp3) |

Sau khi hoàn tất cấu hình, chọn **Launch Instance** để khởi tạo máy chủ.

> **Hình 5.3.3. Cấu hình Amazon EC2 Instance.**

> ![Hình 5.3.3](/images/5.3.3ws.png)

---

### Gán Elastic IP

Sau khi EC2 Instance được khởi tạo thành công, tiến hành gán **Elastic IP** để máy chủ sử dụng địa chỉ IP tĩnh.

Các bước thực hiện:

1. Truy cập **Elastic IPs** trong Amazon EC2 Console.
2. Chọn **Allocate Elastic IP Address**.
3. Chọn **Allocate** để tạo địa chỉ IP.
4. Chọn Elastic IP vừa tạo.
5. Chọn **Actions → Associate Elastic IP Address**.
6. Chọn EC2 Instance cần gán Elastic IP và xác nhận.

Việc sử dụng Elastic IP giúp địa chỉ IP của máy chủ không thay đổi sau khi khởi động lại EC2, thuận tiện cho việc truy cập hệ thống và cấu hình DNS trong các bước tiếp theo.

> **Hình 5.3.4. Elastic IP được gán cho Amazon EC2 Instance.**

> ![Hình 5.3.4](/images/5.3.4.png)

---

## Kết quả

Sau khi hoàn thành bước này, một Amazon EC2 Instance đã được khởi tạo thành công và được gán Elastic IP. Máy chủ đã sẵn sàng cho quá trình cấu hình môi trường và triển khai AI Learning Assistant Platform trong các bước tiếp theo.
