---
title: "Những khó khăn gặp phải"
date: 2026-08-07
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---


Trong quá trình triển khai **AI Learning Assistant Platform**, nhóm gặp một số vấn đề liên quan đến tài nguyên máy chủ và cấu hình quyền truy cập AWS.

### 1. Cạn kiệt bộ nhớ 

Ở giai đoạn đầu, nhóm thử triển khai toàn bộ hệ thống, bao gồm **Application, MongoDB và PostgreSQL + pgvector**, trên các máy chủ có cấu hình thấp như **t2.micro** hoặc **t3.small**.

Tuy nhiên, do kiến trúc **RAG** và **Vector Database** yêu cầu nhiều tài nguyên bộ nhớ, máy chủ thường xuyên xảy ra tình trạng **Out of Memory (OOM)** và bị Crash.

Sau khi xác định nguyên nhân, nhóm đã nâng cấp cấu hình EC2 lên **t3.large** để cung cấp thêm CPU và RAM, giúp hệ thống hoạt động ổn định hơn.

Qua vấn đề này, nhóm nhận ra rằng việc lựa chọn **Instance Type** cần dựa trên yêu cầu tài nguyên thực tế của ứng dụng thay vì chỉ tập trung vào việc sử dụng cấu hình thấp để tiết kiệm chi phí.

### 2. Lỗi phân quyền IAM

Trong quá trình thiết lập **GitHub Actions**, nhóm gặp lỗi **Access Denied** khi Workflow thực hiện các thao tác với **Amazon ECR**.

Sau khi kiểm tra lại cấu hình IAM, nhóm nhận ra IAM User chưa được cấp đầy đủ quyền cần thiết cho các thao tác với ECR.

Nhóm đã bổ sung quyền phù hợp và áp dụng nguyên tắc **Least Privilege**, chỉ cấp những quyền cần thiết cho quá trình triển khai.

Sau khi cập nhật quyền, GitHub Actions có thể thực hiện các thao tác với ECR và tiếp tục quy trình CI/CD.

Qua vấn đề này, nhóm hiểu rõ hơn về tầm quan trọng của **IAM Permissions** và nguyên tắc **Least Privilege** trong việc bảo mật tài nguyên AWS.