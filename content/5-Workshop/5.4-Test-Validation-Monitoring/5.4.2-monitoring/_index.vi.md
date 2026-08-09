---
title: "Giám sát Metrics với Amazon CloudWatch"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

## Mục tiêu

Sử dụng **Amazon CloudWatch** để theo dõi các chỉ số hoạt động của **Amazon EC2**, từ đó đánh giá tình trạng tài nguyên của máy chủ trong quá trình vận hành **AI Learning Assistant Platform**.

---

## Nội dung thực hiện

### Kiểm tra Metrics của Amazon EC2

Mặc định, **Amazon EC2** gửi các chỉ số cơ bản đến **Amazon CloudWatch**, cho phép theo dõi tình trạng hoạt động của Instance mà không cần cài đặt thêm phần mềm trên máy chủ.

Thực hiện các bước sau:

1. Truy cập **AWS Management Console**.
2. Tìm kiếm và mở dịch vụ **Amazon CloudWatch**.
3. Chọn **Metrics**.
4. Chọn **All metrics**.
5. Chọn **EC2**.
6. Chọn nhóm Metrics phù hợp với **Instance**.
7. Tìm và chọn **Instance ID** của máy chủ đang chạy **AI Learning Assistant Platform**.

Sau khi chọn Instance, CloudWatch hiển thị các biểu đồ Metrics của máy chủ.

Các chỉ số có thể quan sát bao gồm:

- **CPU Utilization:** Mức độ sử dụng CPU của EC2 Instance.
- **Network In:** Lượng dữ liệu mạng đi vào Instance.
- **Network Out:** Lượng dữ liệu mạng đi ra khỏi Instance.

Các Metrics này giúp theo dõi mức độ sử dụng tài nguyên của EC2 và hỗ trợ phát hiện các tình trạng bất thường trong quá trình vận hành.

> **Hình 5.4.2. Biểu đồ CPU Utilization của Amazon EC2 trên Amazon CloudWatch.**

> ![Hình 5.4.2](/images/5.4.2.png)

---

## Kết quả

Sau khi cấu hình và kiểm tra **Amazon CloudWatch**, các Metrics cơ bản của **Amazon EC2** có thể được theo dõi trực tiếp trên AWS Management Console.

Việc theo dõi **CPU Utilization**, **Network In** và **Network Out** giúp đánh giá tình trạng hoạt động của máy chủ và cung cấp cơ sở cho việc phát hiện các vấn đề về tài nguyên trong quá trình vận hành hệ thống.