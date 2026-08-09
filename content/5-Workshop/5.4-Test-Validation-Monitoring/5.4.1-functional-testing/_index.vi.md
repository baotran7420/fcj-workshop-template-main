---
title: "Kiểm thử chức năng"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

## Mục tiêu

Kiểm tra các chức năng chính của **AI Learning Assistant Platform** sau khi hệ thống được triển khai trên **Amazon EC2**, đặc biệt là khả năng tạo Knowledge Base, xử lý tài liệu và thực hiện truy vấn thông qua hệ thống **RAG**.

---

## Nội dung thực hiện

### 1. Truy cập ứng dụng

Truy cập **AI Learning Assistant Platform** thông qua địa chỉ Web của Amazon EC2:

```text
http://<ELASTIC_IP>:3000
```

Ví dụ:

```text
http://13.219.3.244:3000
```

Sau đó đăng nhập vào hệ thống bằng tài khoản **Quản trị viên (Root)**.

---

### 2. Kiểm tra Knowledge Base và RAG

Sau khi đăng nhập thành công, tạo một **Knowledge Base (Tập tri thức)** mới.

Tiến hành tải lên một tài liệu mẫu ở định dạng **PDF** hoặc **Word**.

Quá trình xử lý tài liệu sẽ sử dụng hệ thống cơ sở dữ liệu **PostgreSQL + pgvector** để lưu trữ và xử lý các **Vector Embeddings** phục vụ cho quá trình truy xuất thông tin.

---

### 3. Kiểm thử chức năng AI Chat

Mở giao diện **AI Chat** và đặt một câu hỏi liên quan trực tiếp đến nội dung của tài liệu vừa tải lên.

Ví dụ, nếu tài liệu chứa thông tin về AWS, có thể đặt câu hỏi liên quan đến nội dung được trình bày trong tài liệu.

Hệ thống sẽ thực hiện quá trình truy xuất thông tin từ Knowledge Base và sử dụng kết quả truy xuất để tạo câu trả lời.

---

### 4. Kiểm tra kết quả

Kết quả được đánh giá dựa trên các tiêu chí:

- Hệ thống nhận và xử lý thành công tài liệu được tải lên.
- Knowledge Base có thể sử dụng nội dung tài liệu để truy xuất thông tin.
- AI Chat trả lời câu hỏi liên quan đến nội dung tài liệu.
- Câu trả lời chứa thông tin phù hợp với nội dung nguồn.
- Hệ thống hiển thị phần **Citation (trích dẫn nguồn)** tương ứng với nội dung được sử dụng để trả lời.

> **Hình 5.4.1. Kết quả kiểm thử chức năng AI Chat và trích dẫn nguồn tài liệu.**

> ![Hình 5.4.1](/images/5.4.1.png)

---

## Kết quả

Qua quá trình kiểm thử, các chức năng chính của **AI Learning Assistant Platform** được kiểm tra từ khâu tải tài liệu lên **Knowledge Base** đến quá trình truy vấn thông tin thông qua **AI Chat**.

Kết quả kiểm thử được sử dụng để xác nhận khả năng hoạt động của quy trình **Retrieval-Augmented Generation (RAG)** và khả năng cung cấp câu trả lời dựa trên nội dung tài liệu nguồn.