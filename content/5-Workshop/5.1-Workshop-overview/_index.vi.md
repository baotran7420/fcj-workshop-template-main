---
title: " Tổng quan Workshop "
date: 2026-08-05
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---



## Giới thiệu

Trong Workshop này, chúng ta sẽ triển khai **AI Learning Assistant Platform** trên nền tảng **Amazon Web Services (AWS)**.

AI Learning Assistant Platform là một nền tảng học tập thông minh được phát triển dựa trên **FastGPT (Customized)** và kiến trúc **Retrieval-Augmented Generation (RAG)**. Hệ thống cho phép người dùng tải tài liệu học tập, xây dựng **Knowledge Base** và sử dụng trí tuệ nhân tạo để trả lời câu hỏi dựa trên nội dung của tài liệu.

Toàn bộ hệ thống được triển khai trên **Amazon EC2** bằng **Docker Compose**, kết hợp với **Amazon ECR**, **GitHub Actions**, **Amazon S3**, **Amazon CloudWatch**, **AWS IAM** và **Security Group** nhằm xây dựng một quy trình triển khai, giám sát và quản lý ứng dụng AI trên AWS.

> **Hình 5.1. Kiến trúc triển khai AI Learning Assistant Platform trên AWS**

![Hình 5.1](/images/5.1.ws.png)

---

## Kiến trúc triển khai

AI Learning Assistant Platform được triển khai theo mô hình **Client – Server** trên nền tảng Amazon Web Services (AWS).

Người dùng truy cập hệ thống thông qua trình duyệt Web. Các yêu cầu được chuyển đến **Nginx**, sau đó điều phối đến **Frontend** và **Backend**. Backend chịu trách nhiệm xử lý nghiệp vụ, quản lý Knowledge Base và thực hiện quy trình **Retrieval-Augmented Generation (RAG)**.

Toàn bộ ứng dụng được đóng gói dưới dạng các **Docker Container** và triển khai trên một **Amazon EC2**, kết hợp với các dịch vụ lưu trữ, giám sát, sao lưu và bảo mật của AWS.

### Thành phần hệ thống

| Thành phần | Vai trò |
|------------|----------|
| Amazon EC2 | Chạy toàn bộ AI Learning Assistant Platform |
| Docker Compose | Quản lý và điều phối các Docker Container |
| Nginx | Reverse Proxy |
| Frontend | Giao diện người dùng (Next.js / React) |
| Backend | FastGPT (Customized), AI Chat và RAG |
| MongoDB | Lưu trữ dữ liệu hệ thống |
| PostgreSQL + pgvector | Lưu trữ Vector Embedding phục vụ RAG |
| MinIO | Lưu trữ tài liệu học tập |
| Amazon S3 | Sao lưu dữ liệu |
| Amazon ECR | Quản lý Docker Image |
| GitHub Actions | Tự động hóa quy trình CI/CD |
| Amazon CloudWatch | Giám sát hiệu năng và trạng thái hệ thống |
| AWS IAM | Quản lý quyền truy cập |
| Security Group | Kiểm soát lưu lượng truy cập mạng |

---

## Quy trình hoạt động

Sau khi hệ thống được triển khai thành công, AI Learning Assistant Platform hoạt động theo quy trình sau:

1. Người dùng đăng nhập vào hệ thống.
2. Tải tài liệu học tập lên nền tảng.
3. Hệ thống xử lý tài liệu, thực hiện Chunking và tạo Vector Embedding.
4. Dữ liệu được lưu vào Knowledge Base.
5. Người dùng gửi câu hỏi bằng ngôn ngữ tự nhiên.
6. Backend thực hiện quy trình Retrieval-Augmented Generation (RAG) để truy xuất thông tin liên quan.
7. Mô hình AI tạo câu trả lời dựa trên dữ liệu được truy xuất.
8. Kết quả được trả về giao diện người dùng.

> **Hình 5.2. Quy trình hoạt động của AI Learning Assistant Platform**

![Hình 5.2](/images/h3bl3.png)

---

## Kết quả đạt được

Sau khi hoàn thành Workshop này, bạn sẽ có thể:

- Triển khai AI Learning Assistant Platform trên Amazon EC2 bằng Docker Compose.
- Triển khai và vận hành ứng dụng đa container trên AWS.
- Thiết lập quy trình CI/CD bằng GitHub Actions và Amazon ECR.
- Cấu hình Amazon S3 để sao lưu dữ liệu.
- Giám sát hệ thống bằng Amazon CloudWatch.
- Thiết lập AWS IAM và Security Group để bảo vệ hệ thống.
- Truy cập và kiểm thử toàn bộ chức năng của AI Learning Assistant Platform.

---
