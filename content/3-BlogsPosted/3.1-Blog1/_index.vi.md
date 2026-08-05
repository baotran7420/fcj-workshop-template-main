---
title: "Blog 1"
date: 2026-07-16
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#  Mình đã mất 47,77 USD AWS Credits chỉ vì một Amazon RDS "bị bỏ quên"

Trong quá trình học AWS và thực hiện các bài lab, mình đã gặp một trải nghiệm mà có lẽ rất nhiều người mới làm quen với Cloud cũng từng gặp phải.

Ban đầu, mình nhận được **100 USD AWS Credits** để học tập và thực hành trên AWS. Sau khi hoàn thành **5 bài task**, mình tiếp tục được AWS cấp thêm **100 USD AWS Credits**, nâng tổng số lên **200 USD**. Mình tin rằng số credits này sẽ đủ để hoàn thành toàn bộ quá trình học mà không cần quá lo lắng về chi phí.

Thế nhưng, sau khi hoàn thành các bài lab và kiểm tra **AWS Billing**, mình bất ngờ phát hiện tài khoản đã bị trừ **27 USD**. Nghĩ rằng mình chỉ quên xóa một vài tài nguyên, mình bắt đầu kiểm tra lại **Amazon EC2**, **AWS Lambda**, **Amazon VPC**, **Amazon S3** và nhiều dịch vụ khác. Tuy nhiên, sự thật phía sau còn khiến mình bất ngờ hơn...

Tuy nhiên, sang ngày hôm sau, chi phí tiếp tục tăng và tổng số Credits mình mất lên tới **47,77 USD**.

Sau khi kiểm tra kỹ trong **AWS Billing** và **AWS Cost Explorer**, mình mới phát hiện nguyên nhân là **một Amazon RDS Instance vẫn đang ở trạng thái Running**, mặc dù không còn bất kỳ ứng dụng nào sử dụng.

Qua trải nghiệm này, mình nhận ra một bài học quan trọng:

> **Trên Cloud, tài nguyên vẫn tiếp tục phát sinh chi phí miễn là nó còn tồn tại và đang hoạt động, dù không có ai sử dụng.**

---

## Vấn đề mình gặp phải

Hình dưới đây minh họa tình huống mà mình gặp phải: Amazon RDS vẫn hoạt động liên tục sau khi hoàn thành bài thực hành, dẫn đến chi phí phát sinh ngoài mong muốn.

### Hình 1. Amazon RDS chạy liên tục gây phát sinh chi phí

![Hình 1](/images/hinh1.png)

---

## Điều mình học được từ AWS Enterprise Strategy Blog

Sau sự cố này, mình đã tìm đọc bài viết **"Money Matters: Four Methods to Unlock Investment Capacity in IT"** trên **AWS Enterprise Strategy Blog**.

Điều khiến mình tâm đắc nhất là thông điệp:

> **Cost Optimization không chỉ là cắt giảm chi phí, mà là loại bỏ những khoản chi không còn tạo ra giá trị.**

Nhìn lại hệ thống của mình, Amazon RDS:

- Không còn ứng dụng kết nối.
- Không có request.
- Không tạo ra giá trị cho hệ thống.

Nhưng Database vẫn tiếp tục hoạt động và tiêu tốn AWS Credits mỗi ngày.

Đây chính là một ví dụ điển hình của **Cloud Waste** (lãng phí tài nguyên trên Cloud).

---

## Giải pháp

Để tránh lặp lại sai lầm này, mình quyết định áp dụng giải pháp AWS khuyến nghị dành cho môi trường Development và Testing.

Kiến trúc giải pháp bao gồm:

- **Amazon EventBridge** dùng để lập lịch tự động.
- **AWS Lambda** thực hiện Start hoặc Stop Amazon RDS.
- **IAM Role** cấp quyền cho Lambda truy cập Amazon RDS.
- **Amazon CloudWatch Logs** theo dõi và ghi lại toàn bộ quá trình thực thi.

Nhờ đó, Database chỉ hoạt động trong khoảng thời gian cần thiết thay vì chạy liên tục 24/7.

### Hình 2. Kiến trúc tự động Start/Stop Amazon RDS

![Hình 2](/images/hinh2.png)

---

## Quy trình hoạt động

Hằng ngày, hệ thống sẽ hoạt động theo quy trình sau:

- **08:00:** Amazon EventBridge kích hoạt AWS Lambda để khởi động Amazon RDS.
- **18:00:** Amazon EventBridge tiếp tục kích hoạt AWS Lambda để dừng Amazon RDS.

Toàn bộ quá trình diễn ra hoàn toàn tự động, không cần thao tác thủ công.

### Hình 3. Quy trình tự động Start/Stop Amazon RDS

![Hình 3](/images/hinh3.png)

---

## Lịch hoạt động của Amazon RDS

Hình dưới đây mô tả chu kỳ hoạt động của Database trong một ngày.

Amazon RDS chỉ chạy trong giờ làm việc và tự động dừng sau khi kết thúc, giúp giảm đáng kể chi phí cho môi trường Development và Testing.

### Hình 4. Lịch hoạt động hằng ngày của Amazon RDS

![Hình 4](/images/hinh4.png)

---

## Lợi ích đạt được

Sau khi áp dụng giải pháp này, mình nhận thấy nhiều lợi ích rõ rệt:

- Giảm đáng kể chi phí cho môi trường Development và Testing.
- Không còn quên tắt Amazon RDS sau khi hoàn thành bài thực hành.
- Loại bỏ các thao tác Start/Stop thủ công mỗi ngày.
- Có thể theo dõi toàn bộ lịch sử thực thi thông qua Amazon CloudWatch Logs.
- Áp dụng đúng các nguyên tắc **Cost Optimization** mà AWS khuyến nghị.

---

## Bài học rút ra

Trải nghiệm mất **47,77 USD AWS Credits** đã giúp mình thay đổi hoàn toàn cách sử dụng AWS.

Trước đây, mình chỉ tập trung vào việc triển khai dịch vụ.

Hiện tại, mình hiểu rằng:

> **Quản lý vòng đời của tài nguyên cũng quan trọng không kém việc triển khai tài nguyên.**

Một Amazon RDS bị "bỏ quên" có thể âm thầm phát sinh chi phí trong nhiều ngày nếu không được theo dõi hoặc tự động quản lý.

Việc kết hợp **Amazon EventBridge**, **AWS Lambda** và **Amazon RDS** không chỉ giúp tự động hóa quy trình vận hành mà còn góp phần tối ưu chi phí, giảm thao tác thủ công và tuân thủ các thực hành tốt nhất của AWS.

Quan trọng hơn, mình nhận ra rằng **Cost Optimization nên được xem là một phần của quá trình thiết kế và vận hành hệ thống, thay vì chỉ kiểm tra khi nhận hóa đơn cuối tháng.**

---

## Tham khảo

 **Link bài viết gốc và tài liệu mình tham khảo:**

- **Money Matters: Four Methods to Unlock Investment Capacity in IT**  
  AWS Enterprise Strategy Blog  
  https://aws.amazon.com/blogs/enterprise-strategy/it-money-matters-four-methods-to-unlock-investment-capacity/

- **Schedule Amazon RDS Stop and Start Using AWS Lambda**  
  AWS Database Blog  
  https://aws.amazon.com/vi/blogs/database/schedule-amazon-rds-stop-and-start-using-aws-lambda/

- **AWS Well-Architected Framework – Cost Optimization Pillar**  
  https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html

  ## Link bài viết:
https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2215517809213179&notif_id=1784349094559062&notif_t=feedback_reaction_generic&ref=notif