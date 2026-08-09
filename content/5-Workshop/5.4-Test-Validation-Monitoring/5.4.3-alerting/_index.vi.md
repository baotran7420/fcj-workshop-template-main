---
title: "Thiết lập Cảnh báo"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

## Mục tiêu

Thiết lập hệ thống **Cảnh báo** nhằm chủ động phát hiện các tình trạng bất thường trong quá trình vận hành **AI Learning Assistant Platform**, bao gồm tình trạng máy chủ sử dụng CPU cao và chi phí AWS vượt quá mức dự kiến.

Trong phần này, sử dụng **Amazon CloudWatch Alarm** để giám sát CPU của Amazon EC2 và **AWS Budgets** để theo dõi chi phí sử dụng AWS.

---

## Nội dung thực hiện

### 1. Tạo CloudWatch Alarm cảnh báo CPU

**Amazon CloudWatch Alarm** được sử dụng để phát hiện khi mức sử dụng CPU của Amazon EC2 vượt quá ngưỡng cho phép.

Thực hiện các bước sau:

1. Truy cập **Amazon CloudWatch**.
2. Chọn **Alarms**.
3. Chọn **Create alarm**.
4. Chọn **Select metric**.
5. Chọn **EC2 → By Instance Id**.
6. Chọn Instance `ai-learning-assistant`.
7. Chọn Metric **CPUUtilization**.
8. Thiết lập điều kiện cảnh báo:

```text
Threshold type: Static
Condition: Greater/Equal
Threshold: 80%
Evaluation period: 5 minutes
```

Điều kiện trên có nghĩa là CloudWatch sẽ phát cảnh báo khi mức sử dụng CPU của EC2 đạt hoặc vượt quá **80%** trong khoảng thời gian đánh giá được cấu hình.

> **Hình 5.4.3. Cấu hình ngưỡng CPU cho CloudWatch Alarm.**

> ![Hình 5.4.3](/images/5.4.3.png)

---

### 2. Cấu hình thông báo qua Amazon SNS

Để nhận thông báo khi CloudWatch Alarm được kích hoạt, cấu hình **Amazon Simple Notification Service (Amazon SNS)**.

Tại phần **Configure actions**, thực hiện:

1. Chọn trạng thái cảnh báo **In alarm**.
2. Chọn hoặc tạo một **SNS Topic**.
3. Nhập địa chỉ Email cá nhân để nhận thông báo.
4. Hoàn tất quá trình tạo Alarm.

Sau khi tạo SNS Subscription, AWS sẽ gửi một Email xác nhận đến địa chỉ đã đăng ký.

Người nhận cần xác nhận Subscription để có thể nhận các thông báo từ SNS.

> **Lưu ý:** Địa chỉ Email sử dụng cho SNS nên được kiểm tra và xác nhận sau khi tạo Subscription.

---

### 3. Kiểm tra trạng thái CloudWatch Alarm

Sau khi hoàn tất cấu hình, truy cập:

**CloudWatch → Alarms**

Kiểm tra trạng thái của Alarm.

Alarm có thể có các trạng thái:

- **OK:** Metric hiện tại chưa vượt quá ngưỡng cảnh báo.
- **In alarm:** Điều kiện cảnh báo đã được đáp ứng.
- **Insufficient data:** CloudWatch chưa có đủ dữ liệu để đánh giá trạng thái.

Trong điều kiện hệ thống hoạt động bình thường, Alarm CPU dự kiến sẽ ở trạng thái **OK**.

> **Hình 5.4.4. Trạng thái CloudWatch Alarm của Amazon EC2.**

> ![Hình 5.4.4](/images/5.4.4.png)

---

### 4. Tạo cảnh báo chi phí bằng AWS Budgets

Ngoài việc theo dõi hiệu năng máy chủ, cần kiểm soát chi phí sử dụng AWS để tránh phát sinh chi phí ngoài dự kiến.

Truy cập dịch vụ **AWS Budgets** và tiến hành tạo một Budget mới.

Các bước thực hiện:

1. Truy cập **AWS Management Console**.
2. Tìm kiếm và mở **AWS Budgets**.
3. Chọn **Create budget**.
4. Lựa chọn loại Budget phù hợp.

Có thể sử dụng:

- **Zero spend budget** để nhận cảnh báo khi tài khoản bắt đầu phát sinh chi phí.
- **Custom budget** để thiết lập một mức ngân sách cụ thể, ví dụ:

```text
Budget amount: $10/month
```

5. Cấu hình Email nhận thông báo.
6. Thiết lập ngưỡng cảnh báo chi phí.
7. Kiểm tra lại cấu hình.
8. Chọn **Create budget** để hoàn tất.

Budget giúp theo dõi mức sử dụng và chi phí AWS, từ đó chủ động phát hiện khi chi phí bắt đầu phát sinh hoặc tiến gần đến mức ngân sách đã đặt.

> **Hình 5.4.5. Cấu hình AWS Budget và ngưỡng cảnh báo chi phí.**

> ![Hình 5.4.5](/images/5.4.5.png)

---

## Kết quả

Sau khi hoàn thành bước này, hệ thống đã được thiết lập các cơ chế **Alerting** nhằm hỗ trợ giám sát cả hiệu năng và chi phí.

Cụ thể:

- **CloudWatch Alarm** theo dõi mức sử dụng CPU của Amazon EC2.
- **Amazon SNS** được sử dụng để gửi thông báo qua Email khi Alarm được kích hoạt.
- **AWS Budgets** được cấu hình để theo dõi chi phí sử dụng AWS.
- Các cảnh báo giúp người quản trị chủ động phát hiện các vấn đề về tài nguyên và chi phí.

Việc kết hợp **Monitoring** và **Alerting** giúp nâng cao khả năng quản lý và vận hành **AI Learning Assistant Platform** trên AWS.