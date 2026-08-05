---
title: "Blog 2"
date: 2026-08-03
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

#  Mọi Docker Container đều chạy, nhưng website vẫn không truy cập được! Đây là bài học đầu tiên của mình khi triển khai AI Learning Assistant lên AWS EC2

Xin chào mọi người! 

Trong quá trình phát triển dự án **AI Learning Assistant** của nhóm mình, mình đã tự triển khai hệ thống lên **Amazon EC2** bằng **Docker Compose**. Mình nghĩ rằng chỉ cần các container chạy thành công là website sẽ hoạt động. Nhưng thực tế lại không đơn giản như vậy.

---

## Kiến trúc triển khai của hệ thống

Dưới đây là kiến trúc triển khai dự án **AI Learning Assistant** của nhóm mình trên **Amazon EC2** bằng **Docker Compose**.

Hệ thống được triển khai theo mô hình **multi-container**, trong đó mỗi thành phần đảm nhiệm một vai trò riêng:

- **Nginx** đóng vai trò Reverse Proxy, tiếp nhận yêu cầu từ người dùng và chuyển tiếp đến các dịch vụ phía sau.
- **FastGPT Web** cung cấp giao diện cho người dùng.
- **FastGPT API** xử lý các yêu cầu và điều phối toàn bộ nghiệp vụ của hệ thống.
- **MongoDB** lưu trữ dữ liệu của ứng dụng.
- **PostgreSQL** quản lý dữ liệu quan hệ.
- **Redis** dùng để cache và lưu trữ session.
- **Sandbox** thực thi các đoạn mã do AI sinh ra trong môi trường cách ly.
- **AI Model (OpenAI/Gemini/Ollama...)** cung cấp khả năng xử lý ngôn ngữ tự nhiên cho hệ thống.

Toàn bộ các dịch vụ được triển khai bằng **Docker Compose** trên một máy chủ **Amazon EC2**.

### Hình 1. Kiến trúc triển khai AI Learning Assistant

![Hình 1](/images/docker1.png)

---

## Vấn đề mình gặp phải

Sau khi hoàn tất quá trình triển khai, mình kiểm tra thì tất cả container đều ở trạng thái **Running**, ứng dụng cũng phản hồi bình thường khi kiểm tra ngay trên máy chủ EC2.

Tuy nhiên, khi mở trình duyệt và truy cập bằng **Public IP** của EC2, website chỉ hiển thị thông báo:

> **"This site can't be reached"**

Lúc đầu mình nghĩ lỗi nằm ở Docker hoặc ứng dụng. Mình dành khá nhiều thời gian kiểm tra cấu hình Docker Compose, log của các container và cả mã nguồn nhưng vẫn không tìm ra nguyên nhân.

## Quá trình tìm nguyên nhân

Sau đó, mình quyết định kiểm tra từng lớp của hệ thống theo đúng trình tự thay vì thay đổi cấu hình một cách ngẫu nhiên.

Mình lần lượt kiểm tra:

-  Ứng dụng có đang chạy không?
-  Docker Container có hoạt động ổn định không?
-  Port Mapping đã cấu hình đúng chưa?

Sau khi ba bước trên đều không phát hiện lỗi, mình tiếp tục kiểm tra hạ tầng AWS.

Cuối cùng, mình phát hiện nguyên nhân không nằm ở Docker hay ứng dụng mà ở **Security Group của Amazon EC2**.


## Nguyên nhân

Security Group lúc đó chỉ cho phép kết nối qua:

- SSH (Port **22**)

Trong khi đó, hai cổng dùng để truy cập website là:

- HTTP (Port **80**)
- HTTPS (Port **443**)

lại chưa được mở.

Điều này đồng nghĩa với việc:

- Ứng dụng vẫn chạy bình thường.
- Docker không hề gặp lỗi.
- EC2 vẫn hoạt động ổn định.
- Nhưng AWS chặn toàn bộ lưu lượng HTTP và HTTPS từ Internet.

Chỉ sau khi bổ sung các quy tắc cho phép truy cập qua **HTTP (80)** và **HTTPS (443)**, website mới có thể truy cập bình thường từ bên ngoài.

## Bài học mình rút ra

Qua sự cố này, mình nhận ra rằng khi triển khai ứng dụng lên AWS, đừng chỉ tập trung vào Docker hoặc source code.

Hãy kiểm tra toàn bộ hệ thống theo từng lớp:

1. Ứng dụng có chạy không?
2. Docker Container có hoạt động không?
3. Port Mapping đã đúng chưa?
4. Security Group đã mở đúng cổng chưa?
5. Reverse Proxy (Nginx) đã cấu hình chính xác chưa?
6. Domain và DNS đã trỏ đúng chưa?

Việc kiểm tra theo trình tự này giúp mình xác định nguyên nhân nhanh hơn rất nhiều thay vì thay đổi cấu hình một cách ngẫu nhiên.

Qua trải nghiệm này, mình hiểu rằng:

> **Một ứng dụng hoạt động bên trong EC2 không đồng nghĩa với việc người dùng bên ngoài có thể truy cập được. Khi triển khai trên AWS, cần kiểm tra cả ứng dụng, Docker và hạ tầng mạng để đảm bảo hệ thống hoạt động đúng như mong muốn.**

---

## Tham khảo

 **Tài liệu AWS mình tham khảo:**

- **Amazon EC2 Security Groups**  
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html

- **Amazon EC2 Networking and Security**  
  https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html

## Link bài viết

https://www.facebook.com/groups/awsstudygroupfcj/?multi_permalinks=2233426700755623&notif_id=1785770202368739&notif_t=feedback_reaction_generic&ref=notif