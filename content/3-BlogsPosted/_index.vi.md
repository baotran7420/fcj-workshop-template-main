
---
title: "Các bài blog đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---



Trong quá trình thực tập, mình đã nghiên cứu các bài viết từ **AWS Blog**, kết hợp với trải nghiệm thực tế và quá trình học tập để viết các bài chia sẻ kỹ thuật. Mỗi bài blog đều tập trung vào một chủ đề cụ thể, giúp tổng hợp kiến thức, chia sẻ kinh nghiệm cũng như giới thiệu các giải pháp và thực hành tốt nhất (Best Practices) trên AWS.

Các bài viết đã đăng trên **AWS Study Group**:

---

### [Blog 1 - Tôi đã mất 47,77 USD AWS Credits chỉ vì một Amazon RDS "bị bỏ quên"](3.1-Blog1/)

Bài viết này chia sẻ trải nghiệm thực tế của mình khi mất **47,77 USD AWS Credits** do một **Amazon RDS Instance** bị bỏ quên và vẫn tiếp tục hoạt động sau khi hoàn thành các bài thực hành trên AWS. Bài viết phân tích cách các tài nguyên đám mây không được quản lý có thể trở thành **Cloud Waste** (lãng phí tài nguyên), đồng thời giới thiệu giải pháp tự động tối ưu chi phí bằng **Amazon EventBridge**, **AWS Lambda**, **Amazon RDS** và **Amazon CloudWatch** để lập lịch khởi động và dừng cơ sở dữ liệu. Qua đó, bài viết cũng nhấn mạnh tầm quan trọng của việc đưa **Cost Optimization** vào ngay từ giai đoạn thiết kế và vận hành kiến trúc Cloud theo các thực hành tốt nhất của **AWS Well-Architected Framework**.
###  [Blog 2 -  Mọi Docker Container đều chạy, nhưng website vẫn không truy cập được! Đây là bài học đầu tiên của mình khi triển khai AI Learning Assistant lên AWS EC2](3.2-Blog2/)
Bài viết chia sẻ sự cố khi triển khai AI Learning Assistant lên Amazon EC2 bằng Docker Compose. Mặc dù tất cả container đều hoạt động bình thường, website vẫn không thể truy cập từ Internet vì Security Group chưa mở cổng HTTP 80 và HTTPS 443. Qua đó, bài viết nhấn mạnh tầm quan trọng của việc kiểm tra lần lượt ứng dụng, Docker, Port Mapping, Security Group, Nginx và DNS khi xử lý lỗi triển khai.

###  [Blog 3 -  Upload tài liệu thành công nhưng AI vẫn trả lời sai – Bài học về RAG và Knowledge Base khi xây dựng AI Learning Assistant](3.3-Blog3/)
Bài viết trình bày vấn đề AI trả lời không chính xác dù tài liệu đã được tải thành công vào Knowledge Base. Nguyên nhân liên quan đến quy trình RAG, bao gồm trích xuất nội dung, chunking, embedding, lưu trữ vector, retrieval và cấu hình prompt. Sau khi kiểm tra quá trình lập chỉ mục, tối ưu truy xuất và yêu cầu AI chỉ trả lời dựa trên tài liệu, chất lượng câu trả lời được cải thiện và hiện tượng hallucination giảm đáng kể.

