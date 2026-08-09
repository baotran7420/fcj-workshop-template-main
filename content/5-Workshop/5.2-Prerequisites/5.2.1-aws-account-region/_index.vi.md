---
title: "Tài khoản AWS và Region triển khai"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.2.1. </b> "
---




## Mục tiêu

Chuẩn bị tài khoản **Amazon Web Services (AWS)** và lựa chọn **Region** phù hợp trước khi bắt đầu triển khai **AI Learning Assistant Platform**.

Việc lựa chọn cùng một Region cho toàn bộ tài nguyên giúp đảm bảo khả năng kết nối giữa các dịch vụ AWS, thuận tiện trong quá trình triển khai, giám sát và quản lý chi phí.

---

## Nội dung thực hiện

Trước khi triển khai hệ thống, người thực hiện cần đăng nhập vào **AWS Management Console** bằng tài khoản AWS đang hoạt động.

Sau khi đăng nhập thành công, tiến hành lựa chọn Region được sử dụng xuyên suốt trong workshop.

Trong workshop này, hệ thống được triển khai tại:

**US East (N. Virginia) - us-east-1**

Region **us-east-1** được lựa chọn vì các lý do sau:

- Hỗ trợ đầy đủ các dịch vụ AWS được sử dụng trong workshop như Amazon EC2, Amazon ECR, Amazon S3, Amazon CloudWatch và Amazon SNS.
- Là một trong những Region phổ biến và được sử dụng rộng rãi trong các tài liệu hướng dẫn của AWS.
- Có tính ổn định cao, phù hợp cho môi trường học tập, nghiên cứu và phát triển ứng dụng.
- Thuận tiện trong việc tìm kiếm tài liệu tham khảo và xử lý sự cố trong quá trình triển khai.

Trong toàn bộ quá trình triển khai, các tài nguyên AWS sẽ được tạo trong cùng một Region nhằm đảm bảo hệ thống hoạt động ổn định.

---

## Kết quả

Tài khoản AWS đã được chuẩn bị và Region **US East (N. Virginia) - us-east-1** đã được lựa chọn, sẵn sàng cho các bước triển khai tiếp theo.

> **Hình 5.2.1. AWS Management Console và Region được lựa chọn.**
> ![Hình 5.2.1](/images/hinh5.2.1.png)