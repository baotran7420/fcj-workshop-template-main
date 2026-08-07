---
title: "Tổng quan và kiến trúc"
weight: 1
chapter: false
pre: "<b>5.1.</b>"
---



## Giới thiệu

Trong workshop này, chúng ta sẽ triển khai **AI Learning Assistant Platform** trên nền tảng **Amazon Web Services (AWS)**. Mục tiêu của workshop là hướng dẫn toàn bộ quy trình triển khai một hệ thống AI thực tế trên môi trường Cloud, từ việc chuẩn bị hạ tầng, cấu hình máy chủ, triển khai ứng dụng bằng Docker, thiết lập quy trình CI/CD cho đến giám sát và kiểm thử hệ thống sau khi triển khai.

AI Learning Assistant Platform là nền tảng học tập thông minh được xây dựng dựa trên **FastGPT (Customized)** kết hợp với kiến trúc **Retrieval-Augmented Generation (RAG)**. Hệ thống cho phép người dùng tải tài liệu học tập lên, xây dựng **Knowledge Base** và sử dụng trí tuệ nhân tạo để trả lời các câu hỏi dựa trên nội dung của tài liệu. Việc triển khai trên AWS giúp hệ thống dễ dàng quản lý, mở rộng, giám sát và đáp ứng các yêu cầu vận hành trong môi trường thực tế.

---

## Problem & Goal

Trong quá trình học tập và nghiên cứu, sinh viên và giảng viên thường phải làm việc với nhiều nguồn tài liệu như giáo trình, slide bài giảng, tài liệu tham khảo và các bài báo khoa học. Việc tìm kiếm thông tin theo phương pháp truyền thống tốn nhiều thời gian và khó khai thác hiệu quả khi số lượng tài liệu ngày càng lớn.

Mặc dù các mô hình **Large Language Model (LLM)** có khả năng xử lý ngôn ngữ tự nhiên rất mạnh, chúng vẫn gặp hạn chế khi trả lời các câu hỏi liên quan đến dữ liệu nội bộ hoặc tài liệu riêng của người dùng. Điều này có thể dẫn đến hiện tượng **hallucination**, khi mô hình tạo ra câu trả lời không chính xác hoặc không dựa trên dữ liệu thực tế.

Để giải quyết bài toán trên, AI Learning Assistant Platform được xây dựng dựa trên công nghệ **Retrieval-Augmented Generation (RAG)**. Hệ thống cho phép người dùng tải tài liệu học tập lên, xây dựng **Knowledge Base** và đặt câu hỏi trực tiếp dựa trên chính nội dung của tài liệu, giúp nâng cao độ chính xác của câu trả lời và hỗ trợ học tập hiệu quả hơn.

Workshop hướng đến việc triển khai hoàn chỉnh AI Learning Assistant Platform trên nền tảng AWS với các mục tiêu sau:

- Triển khai toàn bộ hệ thống trên Amazon EC2.
- Đóng gói và quản lý ứng dụng bằng Docker Compose.
- Thiết lập quy trình CI/CD thông qua GitHub Actions và Amazon ECR.
- Thiết lập cơ chế sao lưu dữ liệu bằng Amazon S3.
- Giám sát hệ thống bằng Amazon CloudWatch.
- Thiết lập cảnh báo tự động bằng CloudWatch Alarm và Amazon SNS.
- Xây dựng môi trường triển khai ổn định, an toàn và sẵn sàng mở rộng trong tương lai.

---

## Architecture Diagram

AI Learning Assistant Platform được thiết kế theo mô hình **Client–Server** kết hợp với kiến trúc **Retrieval-Augmented Generation (RAG)**. Hệ thống bao gồm các thành phần giao diện người dùng, máy chủ xử lý, cơ sở dữ liệu và các thành phần AI phối hợp với nhau để tiếp nhận yêu cầu, xử lý dữ liệu và tạo câu trả lời dựa trên nội dung tài liệu.

> **Hình 5.1. Kiến trúc tổng thể của AI Learning Assistant Platform.**

![Hình 5.1](/images/3.1.d.x.png)

Người dùng truy cập hệ thống thông qua trình duyệt Web bằng giao thức HTTP hoặc HTTPS. Các yêu cầu được gửi đến **Frontend**, sau đó chuyển tiếp đến **Backend** để xử lý nghiệp vụ. Backend chịu trách nhiệm quản lý người dùng, Knowledge Base, xử lý tài liệu, thực hiện quy trình Retrieval-Augmented Generation (RAG) và giao tiếp với các thành phần lưu trữ dữ liệu.

Trong hệ thống, **MongoDB** được sử dụng để lưu trữ dữ liệu người dùng, hội thoại và cấu hình hệ thống. **PostgreSQL** kết hợp với **pgvector** lưu trữ Vector Embedding phục vụ quá trình tìm kiếm ngữ nghĩa, trong khi **MinIO** lưu trữ các tài liệu được người dùng tải lên để xây dựng Knowledge Base.

Kiến trúc này được thiết kế theo mô hình **Production Lite**, phù hợp với giai đoạn phát triển MVP (Minimum Viable Product), đồng thời vẫn đáp ứng các yêu cầu cơ bản về khả năng mở rộng, quản lý dữ liệu và triển khai trên nền tảng Cloud.


Sau khi hoàn thiện kiến trúc ứng dụng, toàn bộ hệ thống được triển khai trên nền tảng Amazon Web Services (AWS) như Hình 5.2.

> **Hình 5.2. Kiến trúc triển khai AI Learning Assistant Platform trên AWS.**

![Hình 5.2](/images/5.1.ws.png)

Người dùng truy cập hệ thống thông qua **Elastic IP** hoặc tên miền của máy chủ **Amazon EC2** bằng giao thức HTTP hoặc HTTPS. Toàn bộ lưu lượng truy cập được kiểm soát bởi **Security Group** trước khi chuyển đến máy chủ EC2.

Bên trong Amazon EC2, **Docker Compose** quản lý các Docker Container của hệ thống, bao gồm **Nginx**, **Frontend**, **Backend**, **MongoDB**, **PostgreSQL với pgvector** và **MinIO**. Dữ liệu của các container được lưu trữ trên **Amazon EBS** nhằm đảm bảo tính bền vững trong quá trình vận hành.

Quá trình triển khai được tự động hóa thông qua **GitHub Actions** và **Amazon ECR**. Khi mã nguồn được cập nhật trên GitHub Repository, GitHub Actions sẽ tự động xây dựng Docker Image, đẩy Image lên Amazon ECR và triển khai phiên bản mới lên Amazon EC2.

Để đảm bảo hệ thống hoạt động ổn định, **Amazon CloudWatch** được sử dụng để thu thập Logs và Metrics, **CloudWatch Alarm** theo dõi các chỉ số quan trọng như CPU và bộ nhớ, trong khi **Amazon SNS** gửi Email cảnh báo khi hệ thống phát sinh sự cố. Ngoài ra, **Amazon S3** được sử dụng để lưu trữ dữ liệu sao lưu, góp phần đảm bảo an toàn dữ liệu và hỗ trợ khôi phục khi cần thiết.

Hai sơ đồ trên cung cấp cái nhìn tổng quan về kiến trúc của AI Learning Assistant Platform và là cơ sở để thực hiện các bước triển khai chi tiết trong các mục tiếp theo của workshop.

---

## Lý do lựa chọn dịch vụ?

Để đáp ứng yêu cầu triển khai, vận hành và quản lý AI Learning Assistant Platform, workshop sử dụng các dịch vụ AWS phù hợp với từng thành phần của hệ thống.

| Dịch vụ AWS | Lý do lựa chọn |
|--------------|----------------|
| **Amazon EC2** | Triển khai toàn bộ ứng dụng trên một máy chủ duy nhất, thuận tiện cho việc quản lý Docker Compose và phù hợp với mô hình MVP. |
| **Amazon EBS** | Lưu trữ Docker Volumes và dữ liệu của hệ thống, đảm bảo dữ liệu không bị mất khi EC2 khởi động lại. |
| **Amazon ECR** | Lưu trữ Docker Images và tích hợp với GitHub Actions để tự động hóa quy trình CI/CD. |
| **Amazon S3** | Lưu trữ dữ liệu sao lưu với chi phí thấp, độ bền cao và khả năng mở rộng linh hoạt. |
| **Amazon CloudWatch** | Thu thập Logs, Metrics và giám sát trạng thái hoạt động của hệ thống theo thời gian thực. |
| **CloudWatch Alarm** | Theo dõi CPU, Memory và Disk, đồng thời gửi cảnh báo khi vượt ngưỡng cấu hình. |
| **Amazon SNS** | Gửi Email thông báo khi CloudWatch Alarm phát hiện sự cố. |
| **AWS IAM** | Quản lý người dùng và phân quyền truy cập theo nguyên tắc Least Privilege. |
| **Security Group** | Kiểm soát lưu lượng mạng, chỉ cho phép các cổng cần thiết như SSH (22), HTTP (80) và HTTPS (443). |
| **Elastic IP** | Cung cấp địa chỉ IP tĩnh giúp truy cập hệ thống ổn định sau mỗi lần khởi động lại EC2. |

Việc kết hợp các dịch vụ AWS trên giúp xây dựng một quy trình triển khai hoàn chỉnh từ triển khai ứng dụng, tự động hóa CI/CD, lưu trữ dữ liệu, giám sát hệ thống đến quản lý bảo mật. Đây cũng là nền tảng để thực hiện các bước triển khai chi tiết trong các mục tiếp theo của workshop.