---
title: "Bản đề xuất "
date: 2026-08-04
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# AI Learning Assistant Platform

## Nền tảng trợ lý học tập thông minh dựa trên tài liệu triển khai trên AWS

# Phần 1. Giới thiệu dự án

## 1.1 Bối cảnh

Sự phát triển mạnh mẽ của **Trí tuệ nhân tạo (Artificial Intelligence - AI)**, đặc biệt là các **Mô hình ngôn ngữ lớn (Large Language Models - LLMs)**, đang tạo ra nhiều thay đổi trong lĩnh vực giáo dục. Các hệ thống AI có khả năng hỗ trợ người học tìm kiếm thông tin, giải thích kiến thức và tương tác với tài liệu bằng ngôn ngữ tự nhiên, góp phần nâng cao hiệu quả học tập.

Tuy nhiên, hầu hết các chatbot AI hiện nay chỉ dựa trên dữ liệu đã được huấn luyện trước nên chưa thể trả lời chính xác các câu hỏi liên quan đến tài liệu học tập riêng của từng người dùng. Khi thiếu ngữ cảnh phù hợp, AI có thể đưa ra thông tin không chính xác hoặc không phản ánh đúng nội dung của tài liệu.

Trong thực tế, sinh viên thường phải sử dụng nhiều loại tài liệu như giáo trình, slide bài giảng, tài liệu tham khảo và hướng dẫn thực hành. Việc tìm kiếm thông tin trong khối lượng lớn tài liệu này mất nhiều thời gian và ảnh hưởng đến quá trình học tập.

Xuất phát từ nhu cầu đó, dự án **AI Learning Assistant Platform** được đề xuất nhằm xây dựng một nền tảng trợ lý học tập thông minh, cho phép người dùng khai thác hiệu quả tài liệu học tập thông qua công nghệ **Retrieval-Augmented Generation (RAG)**. Hệ thống được phát triển dựa trên nền tảng **FastGPT** và triển khai trên **Amazon Web Services (AWS)** nhằm đảm bảo khả năng mở rộng, tính sẵn sàng và bảo mật.

---

## 1.2 Mục tiêu

Dự án hướng đến việc xây dựng một nền tảng trợ lý học tập thông minh giúp người học tiếp cận và khai thác kiến thức từ tài liệu một cách nhanh chóng và hiệu quả.

Các mục tiêu chính của dự án bao gồm:

- Xây dựng hệ thống AI Learning Assistant ứng dụng công nghệ **Retrieval-Augmented Generation (RAG)**.
- Cho phép người dùng tải lên và quản lý tài liệu học tập.
- Xây dựng **Knowledge Base** phục vụ truy xuất thông tin theo ngữ nghĩa.
- Hỗ trợ AI trả lời câu hỏi dựa trên nội dung tài liệu của người dùng.
- Tích hợp các chức năng hỗ trợ học tập như tóm tắt bài học, tạo câu hỏi trắc nghiệm và Flashcard.
- Triển khai hệ thống trên nền tảng **Amazon Web Services (AWS)** theo mô hình điện toán đám mây.

---

## 1.3 Tổng quan giải pháp

AI Learning Assistant Platform là nền tảng học tập thông minh cho phép người dùng tải lên các tài liệu học tập và tương tác với AI bằng ngôn ngữ tự nhiên.

Sau khi tài liệu được tải lên, hệ thống sẽ tự động xử lý nội dung, chia nhỏ tài liệu, tạo **Embedding** và xây dựng **Knowledge Base**. Khi người dùng đặt câu hỏi, hệ thống sử dụng cơ chế **Retrieval-Augmented Generation (RAG)** để truy xuất các đoạn tài liệu liên quan, sau đó cung cấp ngữ cảnh cho mô hình AI nhằm tạo ra câu trả lời chính xác và bám sát nội dung tài liệu.

Ngoài chức năng hỏi đáp, hệ thống còn hỗ trợ quản lý tài liệu, tóm tắt bài học, tạo câu hỏi trắc nghiệm, Flashcard và lưu lịch sử học tập. Toàn bộ ứng dụng được triển khai trên AWS bằng Docker Compose và tự động hóa quy trình triển khai thông qua GitHub Actions kết hợp với Amazon ECR, tạo nền tảng thuận lợi cho việc mở rộng và phát triển trong tương lai.

### Thông tin tổng quan

| Tiêu chí | Giá trị |
|----------|----------|
| Tên dự án | AI Learning Assistant Platform |
| Loại dự án | Nền tảng trợ lý học tập thông minh |
| Đối tượng sử dụng | Sinh viên, giảng viên |
| Nền tảng phát triển | FastGPT (Customized) |
| Công nghệ AI | RAG, Knowledge Base, Embedding |
| Cloud Platform | Amazon Web Services (AWS) |
| Dịch vụ AWS | Amazon EC2, Amazon S3, Amazon CloudWatch |
| Cơ sở dữ liệu | MongoDB, PostgreSQL |
| Phương thức triển khai | Docker Compose |

# Phần 2. Phân tích bài toán và giải pháp

## 2.1 Bài toán

Trong môi trường học tập hiện nay, sinh viên thường phải sử dụng nhiều nguồn tài liệu như giáo trình, slide bài giảng, tài liệu tham khảo và hướng dẫn thực hành. Khi số lượng tài liệu ngày càng lớn, việc tìm kiếm một nội dung cụ thể trở nên mất nhiều thời gian và ảnh hưởng đến hiệu quả học tập.

Mặc dù các chatbot AI hiện nay có khả năng trả lời nhiều câu hỏi bằng ngôn ngữ tự nhiên, nhưng phần lớn chỉ dựa trên kiến thức đã được huấn luyện trước. Điều này khiến AI không thể khai thác chính xác nội dung từ tài liệu riêng của người dùng, đồng thời có thể tạo ra những câu trả lời không đúng với ngữ cảnh hoặc không có trong tài liệu.

Do đó, cần có một giải pháp cho phép AI hiểu và khai thác trực tiếp dữ liệu từ tài liệu học tập, giúp người dùng tìm kiếm thông tin nhanh chóng và nhận được câu trả lời chính xác hơn.

--- 

## 2.2 Giải pháp đề xuất

Để giải quyết các vấn đề trên, dự án đề xuất xây dựng **AI Learning Assistant Platform** dựa trên công nghệ **Retrieval-Augmented Generation (RAG)**.

Khác với chatbot AI truyền thống, hệ thống cho phép người dùng tải lên các tài liệu học tập để xây dựng **Knowledge Base**. Khi người dùng đặt câu hỏi, hệ thống sẽ truy xuất những đoạn nội dung liên quan từ Knowledge Base trước khi gửi đến mô hình AI để tạo câu trả lời.

Nhờ đó, AI có thể:

- Trả lời dựa trên nội dung tài liệu của người dùng.
- Giảm hiện tượng AI tạo thông tin không có căn cứ (Hallucination).
- Hiển thị nguồn tham khảo của câu trả lời.
- Nâng cao độ chính xác và tính tin cậy của kết quả.

Ngoài chức năng hỏi đáp, hệ thống còn hỗ trợ các tính năng như:

- Quản lý tài liệu học tập.
- Tóm tắt nội dung bài học.
- Tạo câu hỏi trắc nghiệm.
- Tạo Flashcard hỗ trợ ôn tập.
- Lưu lịch sử học tập và hội thoại.

---

## 2.3 Quy trình hoạt động

Quy trình hoạt động của hệ thống gồm các bước sau:

1. Người dùng tải tài liệu học tập lên hệ thống.
2. Hệ thống trích xuất nội dung và xử lý tài liệu.
3. Nội dung được chia thành các đoạn nhỏ (Chunking).
4. Hệ thống tạo Embedding và lưu vào Vector Database.
5. Người dùng đặt câu hỏi bằng ngôn ngữ tự nhiên.
6. Hệ thống truy xuất các đoạn tài liệu phù hợp từ Knowledge Base.
7. Mô hình AI sử dụng các đoạn tài liệu làm ngữ cảnh để sinh câu trả lời.
8. Kết quả cùng nguồn tham khảo được hiển thị cho người dùng.

> **Hình 2.1. Quy trình hoạt động của AI Learning Assistant Platform sử dụng RAG.**

![Quy trình Retrieval-Augmented Generation](/images/h3bl3.png)

## 2.4 Lợi ích của giải pháp

Việc áp dụng công nghệ RAG vào AI Learning Assistant Platform mang lại nhiều lợi ích:

- Hỗ trợ tìm kiếm thông tin nhanh chóng trong tài liệu học tập.
- Nâng cao độ chính xác của câu trả lời nhờ sử dụng dữ liệu thực tế.
- Giảm hiện tượng Hallucination của mô hình AI.
- Tiết kiệm thời gian học tập và ôn tập.
- Tạo môi trường học tập thông minh, linh hoạt và dễ mở rộng trên nền tảng AWS.

Giải pháp không chỉ phù hợp với sinh viên và giảng viên mà còn có thể mở rộng cho các tổ chức đào tạo hoặc doanh nghiệp cần xây dựng hệ thống hỏi đáp dựa trên tài liệu nội bộ.

# Phần 3. Thiết kế và kiến trúc hệ thống

## 3.1 Kiến trúc tổng thể

AI Learning Assistant Platform được xây dựng theo mô hình **Client–Server** kết hợp với kiến trúc **Retrieval-Augmented Generation (RAG)** và được triển khai trên **Amazon Web Services (AWS)** nhằm xây dựng một nền tảng học tập thông minh có khả năng quản lý tài liệu, tìm kiếm ngữ nghĩa và hỗ trợ học tập bằng trí tuệ nhân tạo.

Kiến trúc hệ thống được chia thành năm lớp chính:

- **Client Layer:** Sinh viên và giảng viên truy cập hệ thống thông qua trình duyệt web bằng giao thức HTTP hoặc HTTPS.
- **Application Layer:** Toàn bộ ứng dụng được triển khai trên **Amazon EC2** dưới dạng các **Docker Container** được quản lý bởi **Docker Compose**, bao gồm Nginx, Frontend, Backend, MongoDB, PostgreSQL với pgvector và MinIO.
- **AI & Data Layer:** Backend xử lý AI Chat, Retrieval-Augmented Generation (RAG), Knowledge Base, Document Processing và Semantic Search. PostgreSQL với **pgvector** lưu trữ vector embedding, trong khi MongoDB quản lý dữ liệu người dùng, hội thoại và cấu hình hệ thống.
- **Infrastructure Layer:** Amazon EBS cung cấp vùng lưu trữ lâu dài cho Docker Volume và dữ liệu hệ thống. Amazon S3 được sử dụng để lưu trữ các bản sao lưu và tài liệu dự phòng.
- **DevOps & Monitoring Layer:** GitHub Actions và Amazon ECR hỗ trợ quy trình CI/CD, trong khi Amazon CloudWatch, CloudWatch Alarm và AWS Budgets giúp giám sát hệ thống, cảnh báo sự cố và kiểm soát chi phí vận hành.

Kiến trúc được thiết kế theo hướng **Production Lite**, phù hợp với quy mô MVP nhưng vẫn đáp ứng các yêu cầu cơ bản về triển khai, bảo mật, giám sát, sao lưu và tự động hóa trên nền tảng AWS.

> **Hình 3.1. Kiến trúc tổng thể của AI Learning Assistant Platform.**

![Hình 3.1](/images/3.1.d.x.png)

---

## 3.2 Kiến trúc triển khai trên AWS

AI Learning Assistant Platform được triển khai trên **Amazon Web Services (AWS)** tại Region **US East (N. Virginia) – us-east-1**.

Người dùng truy cập hệ thống thông qua **Elastic IP** hoặc tên miền của Amazon EC2 bằng giao thức HTTP hoặc HTTPS. Toàn bộ lưu lượng truy cập được kiểm soát bởi **Security Group** trước khi chuyển đến máy chủ EC2.

Bên trong Amazon EC2, Docker Compose quản lý các container của hệ thống gồm Nginx, Frontend, Backend, MongoDB, PostgreSQL với pgvector, MinIO. Amazon EBS được sử dụng để lưu trữ Docker Volume và dữ liệu lâu dài.

Để đảm bảo khả năng phục hồi dữ liệu, MongoDB, PostgreSQL và MinIO được sao lưu định kỳ lên **Amazon S3**. Amazon CloudWatch kết hợp với CloudWatch Alarm được sử dụng để theo dõi hiệu năng hệ thống và gửi cảnh báo khi xảy ra sự cố.

Quy trình triển khai được tự động hóa bằng **GitHub Actions** và **Amazon ECR**. Khi mã nguồn được cập nhật lên GitHub Repository, GitHub Actions sẽ tự động xây dựng Docker Image, đẩy Image lên Amazon ECR và triển khai phiên bản mới lên Amazon EC2.

### Các dịch vụ AWS được sử dụng

| Dịch vụ AWS | Vai trò |
|-------------|----------|
| Amazon EC2 | Chạy toàn bộ hệ thống AI Learning Assistant |
| Amazon EBS | Lưu Docker Volume và dữ liệu lâu dài |
| Amazon S3 | Sao lưu MongoDB, PostgreSQL và tài liệu học tập |
| Amazon ECR | Quản lý Docker Image |
| Amazon CloudWatch | Giám sát Metrics và Logs |
| CloudWatch Alarm | Cảnh báo CPU, Memory, Disk và trạng thái dịch vụ |
| Amazon SNS | Gửi Email Notification khi xảy ra cảnh báo |
| AWS IAM | Quản lý quyền truy cập tài nguyên AWS |
| Security Group | Kiểm soát truy cập mạng vào EC2 |
| AWS Budgets | Theo dõi và cảnh báo chi phí AWS |

Kiến trúc hiện tại được tối ưu cho môi trường thực tập và giai đoạn MVP. Việc triển khai trên một Amazon EC2 giúp giảm chi phí vận hành, đồng thời vẫn đảm bảo khả năng mở rộng trong tương lai thông qua CI/CD, Docker Container và các dịch vụ quản trị của AWS.

> **Hình 3.2. Kiến trúc triển khai hệ thống trên AWS.**

![Hình 3.2](/images/3.2.d.s.png)

---

## 3.3 Thiết kế cơ sở dữ liệu

Hệ thống sử dụng nhiều thành phần lưu trữ nhằm đáp ứng yêu cầu quản lý dữ liệu, truy xuất ngữ nghĩa và lưu trữ tài liệu học tập.

| Thành phần | Vai trò |
|------------|----------|
| MongoDB | Lưu trữ thông tin người dùng, hội thoại, Knowledge Base và cấu hình hệ thống |
| PostgreSQL + pgvector | Lưu trữ Vector Embedding phục vụ Semantic Search và Retrieval-Augmented Generation |
| MinIO | Lưu trữ tài liệu học tập do người dùng tải lên |
| Amazon S3 | Sao lưu MongoDB, PostgreSQL và tài liệu học tập |
| Amazon EBS | Lưu Docker Volume và dữ liệu lâu dài của hệ thống |

MongoDB, PostgreSQL và MinIO hoạt động trong mạng nội bộ Docker và không được mở trực tiếp ra Internet nhằm tăng cường bảo mật cho hệ thống.

> **Hình 3.3. Sơ đồ cơ sở dữ liệu của hệ thống.**

![Hình 3.3](/images/3.3.pr.drawio.png)

---

## 3.4 Quy trình hoạt động

Sau khi người dùng tải tài liệu lên hệ thống, AI Learning Assistant Platform thực hiện quy trình Retrieval-Augmented Generation (RAG) theo các bước sau:

1. Người dùng tải tài liệu học tập lên hệ thống.
2. Backend trích xuất nội dung từ tài liệu.
3. Tài liệu được chia thành các đoạn nhỏ (Chunking).
4. Hệ thống tạo Vector Embedding cho từng đoạn.
5. Embedding được lưu trong PostgreSQL với pgvector, trong khi Metadata được lưu trong MongoDB.
6. Người dùng gửi câu hỏi từ giao diện AI Chat.
7. Backend tạo Embedding cho câu hỏi và thực hiện Semantic Search trong Vector Database.
8. Các đoạn tài liệu liên quan được truy xuất và kết hợp với câu hỏi để tạo Prompt.
9. Prompt được gửi đến Large Language Model (LLM).
10. AI tạo câu trả lời dựa trên ngữ cảnh của tài liệu và trả kết quả kèm nguồn tham khảo cho người dùng.

Quy trình này giúp AI hạn chế hiện tượng Hallucination, nâng cao độ chính xác của câu trả lời và tận dụng hiệu quả nguồn tài liệu học tập của người dùng.

> **Hình 3.4. Quy trình hoạt động của AI Learning Assistant Platform sử dụng RAG.**

![Hình 3.4](/images/3.4.p.r.png)

---

## 3.5 Công nghệ sử dụng

| Thành phần | Công nghệ |
|------------|-----------|
| Frontend | Next.js, React, TypeScript |
| Backend | FastGPT (Customized) |
| AI | Large Language Models (LLMs) |
| AI Framework | Retrieval-Augmented Generation (RAG) |
| Database | MongoDB, PostgreSQL + pgvector |
| Object Storage | MinIO |
| Containerization | Docker, Docker Compose |
| Version Control | GitHub |
| CI/CD | GitHub Actions |
| Container Registry | Amazon ECR |
| Cloud Platform | Amazon Web Services (AWS) |
| Monitoring | Amazon CloudWatch, CloudWatch Alarm |
| Backup Storage | Amazon S3 |
| Persistent Storage | Amazon EBS |
| Cost Management | AWS Budgets |
# Phần 4. Triển khai và kiểm thử

## 4.1 Môi trường triển khai

AI Learning Assistant Platform được triển khai trên **Amazon Web Services (AWS)** tại Region **US East (N. Virginia) – us-east-1**.

Toàn bộ hệ thống được triển khai trên một **Amazon EC2** bằng **Docker Compose**, bao gồm **Nginx**, **Frontend (Next.js/React)**, **Backend (FastGPT Customized)**, **MongoDB**, **PostgreSQL với pgvector** và **MinIO**.

Hệ thống sử dụng **Amazon EBS** để lưu trữ dữ liệu lâu dài, **Amazon S3** để sao lưu dữ liệu, **Amazon ECR** để quản lý Docker Image, **GitHub Actions** để tự động hóa quy trình CI/CD, **Amazon CloudWatch** để giám sát hệ thống, cùng **AWS IAM**, **Security Group** và **AWS Budgets** để quản lý bảo mật và chi phí.

### Cấu hình môi trường

| Thành phần | Công nghệ / Dịch vụ |
|------------|---------------------|
| Cloud Platform | Amazon Web Services (AWS) |
| Region | us-east-1 |
| Compute | Amazon EC2 |
| Persistent Storage | Amazon EBS |
| Container | Docker, Docker Compose |
| Reverse Proxy | Nginx |
| Frontend | Next.js, React |
| Backend | FastGPT (Customized) |
| Database | MongoDB, PostgreSQL + pgvector |
| Object Storage | MinIO |
| Container Registry | Amazon ECR |
| CI/CD | GitHub Actions |
| Monitoring | Amazon CloudWatch |
| Backup Storage | Amazon S3 |
| Security | AWS IAM, Security Group |
| Cost Monitoring | AWS Budgets |

> **Hình 4.1. Môi trường triển khai AI Learning Assistant Platform trên AWS.**

![Hình 4.1](/images/4.1.d.x.png)

---

## 4.2 Quy trình triển khai hệ thống

Quy trình triển khai hệ thống được thực hiện theo các bước sau:

1. Khởi tạo và cấu hình **Amazon EC2**, **Security Group** và **Elastic IP**.
2. Cài đặt **Docker** và **Docker Compose** trên Amazon EC2.
3. Đẩy mã nguồn lên **GitHub Repository**.
4. **GitHub Actions** tự động xây dựng Docker Image và đẩy lên **Amazon ECR**.
5. Amazon EC2 tải Docker Image mới và khởi động các container bằng **Docker Compose**.
6. **Amazon CloudWatch** giám sát trạng thái hoạt động của hệ thống.
7. Dữ liệu MongoDB, PostgreSQL và MinIO được sao lưu định kỳ lên **Amazon S3**.

> **Hình 4.2. Quy trình triển khai AI Learning Assistant Platform trên AWS.**

![Hình 4.2](/images/4.2.d.x.png)

---

## 4.3 Kiểm thử hệ thống

Sau khi triển khai thành công, hệ thống được kiểm thử nhằm đánh giá tính ổn định và khả năng hoạt động của các chức năng chính.

| Chức năng | Kết quả |
|-----------|----------|
| Đăng nhập và xác thực người dùng | Thành công |
| Quản lý môn học | Thành công |
| Upload tài liệu học tập | Thành công |
| Xây dựng Knowledge Base | Thành công |
| AI Chat (RAG) | Thành công |
| Tóm tắt bài học | Thành công |
| Tạo Quiz | Thành công |
| Tạo Flashcard | Thành công |
| Triển khai CI/CD | Thành công |

Kết quả kiểm thử cho thấy hệ thống hoạt động ổn định, các Docker Container vận hành bình thường và các chức năng chính đáp ứng yêu cầu của nền tảng.

---

## 4.4 Giám sát và vận hành

Trong quá trình vận hành, **Amazon CloudWatch** được sử dụng để giám sát hiệu năng và trạng thái hoạt động của hệ thống.

Các chỉ số được theo dõi bao gồm:

- CPU Utilization
- Memory Usage
- Disk Usage
- Network Traffic
- Docker Container Logs

Ngoài ra, dữ liệu của MongoDB, PostgreSQL và các tài liệu học tập được sao lưu định kỳ lên **Amazon S3** nhằm đảm bảo khả năng phục hồi dữ liệu khi xảy ra sự cố. **AWS Budgets** được sử dụng để theo dõi chi phí và cảnh báo khi mức sử dụng vượt quá ngân sách đã thiết lập.
# Phần 5. Bảo mật và tối ưu chi phí

## 5.1 Bảo mật hệ thống

AI Learning Assistant Platform lưu trữ tài khoản người dùng, tài liệu học tập và lịch sử hội thoại. Do đó, hệ thống áp dụng nhiều biện pháp nhằm đảm bảo an toàn dữ liệu khi triển khai trên Amazon Web Services (AWS).

Các biện pháp bảo mật chính bao gồm:

- Sử dụng **AWS IAM** để quản lý quyền truy cập theo nguyên tắc **Least Privilege**.
- Sử dụng **Security Group** để kiểm soát các cổng truy cập vào Amazon EC2.
- Sử dụng **HTTPS** để mã hóa dữ liệu truyền giữa người dùng và hệ thống.
- Lưu trữ thông tin cấu hình và API Key bằng **Environment Variables**, không lưu trực tiếp trong mã nguồn.
- Giới hạn quyền truy cập vào **Amazon S3** đối với dữ liệu sao lưu.
- MongoDB, PostgreSQL và MinIO chỉ hoạt động trong mạng nội bộ Docker và không được truy cập trực tiếp từ Internet.
- Sử dụng **Amazon CloudWatch** để giám sát trạng thái hoạt động và phát hiện các sự cố của hệ thống.

---

## 5.2 Chi phí triển khai dự kiến

Hệ thống được triển khai theo mô hình **Production Lite** nhằm tối ưu chi phí nhưng vẫn đáp ứng các yêu cầu về hiệu năng, bảo mật và khả năng mở rộng.

### Bảng 5.1. Chi phí triển khai dự kiến

| Dịch vụ AWS | Mục đích | Chi phí ước tính (USD/Tháng) |
|--------------|---------|---------------------------:|
| Amazon EC2 (t3.large) | Application Hosting | 60 |
| Amazon EBS (50 GB) | Persistent Storage | 4 |
| Amazon S3 | Backup Storage | 2 |
| Amazon ECR | Docker Image Registry | 1 |
| Amazon CloudWatch | Monitoring | 3 |
| Data Transfer | Internet Traffic | 8 |
| Google Gemini / OpenAI API | AI Processing | 15–50 |

| | **Tổng ước tính chi phí** | **93–128 USD/Tháng** |

### Tối ưu chi phí

Nền tảng áp dụng các chiến lược tối ưu chi phí sau:

- Triển khai toàn bộ hệ thống trên một **Amazon EC2 Instance** trong giai đoạn phát triển MVP.
- Theo dõi và kiểm soát chi phí sử dụng AWS bằng **AWS Budgets**.
- Lưu trữ dữ liệu sao lưu trên **Amazon S3** thay vì duy trì nhiều bản sao trên EC2.
- Xóa các tài nguyên AWS không còn sử dụng sau khi hoàn thành quá trình kiểm thử.
- Tối ưu số lượng và tần suất các yêu cầu (request) gửi đến dịch vụ AI nhằm giảm chi phí sử dụng API.
- Chỉ mở rộng hệ thống sang **Application Load Balancer (ALB)** và **Amazon ECS** khi số lượng người dùng hoặc lưu lượng truy cập tăng cao.

---

# Phần 6. Đánh giá và hướng phát triển

## 6.1 Đánh giá theo AWS Well-Architected Framework

AI Learning Assistant Platform được đánh giá dựa trên các nguyên tắc của **AWS Well-Architected Framework**.

### Bảng 6.1. Đánh giá hệ thống

| Pillar | Implementation |
|---------|----------------|
| Operational Excellence | Docker Compose, GitHub Actions, Amazon CloudWatch |
| Security | AWS IAM, Security Group, HTTPS, Environment Variables |
| Reliability | Amazon S3 Backup, Docker Restart Policy, Amazon CloudWatch |
| Performance Efficiency | PostgreSQL + pgvector, Retrieval-Augmented Generation (RAG) |
| Cost Optimization | Amazon EC2, AWS Budgets, Amazon CloudWatch |
| Sustainability | Architecture can be extended to Amazon ECS and Application Load Balancer |

Hệ thống hiện tại đáp ứng các nguyên tắc cốt lõi của AWS Well-Architected Framework đối với một ứng dụng AI được triển khai trên nền tảng AWS. Kiến trúc này phù hợp để phát triển phiên bản Minimum Viable Product (MVP), đồng thời vẫn đảm bảo khả năng mở rộng và nâng cấp trong tương lai khi quy mô hệ thống và số lượng người dùng tăng lên.

> **Hình 6.1. Đánh giá AI Learning Assistant Platform theo AWS Well-Architected Framework.**

![Hình 6.1](/images/6.1.p.r.png)

---

## 6.2 Hướng phát triển

Trong tương lai, hệ thống có thể được mở rộng theo các hướng sau:

- Triển khai **Amazon ECS** để tăng khả năng mở rộng.
- Sử dụng **Application Load Balancer** để phân phối lưu lượng truy cập.
- Mở rộng Knowledge Base cho nhiều môn học và người dùng.
- Tích hợp thêm các mô hình AI như **Amazon Bedrock**, **Google Gemini** hoặc **OpenAI**.
- Bổ sung các tính năng AI như AI Tutor, Mindmap, Speech-to-Text và Text-to-Speech.
- Hoàn thiện hệ thống Monitoring, Alerting và Backup để nâng cao độ tin cậy.

Với kiến trúc hiện tại, AI Learning Assistant Platform có thể đáp ứng tốt nhu cầu triển khai trong giai đoạn MVP và sẵn sàng mở rộng khi số lượng người dùng tăng trong tương lai.
# Phần 7. Kết luận

## 7.1 Kết quả đạt được

AI Learning Assistant Platform được xây dựng nhằm hỗ trợ người học khai thác tài liệu học tập thông qua trí tuệ nhân tạo kết hợp với công nghệ Retrieval-Augmented Generation (RAG). Hệ thống cho phép người dùng tải lên tài liệu, xây dựng Knowledge Base và tương tác với AI bằng ngôn ngữ tự nhiên, từ đó nâng cao độ chính xác của câu trả lời so với các chatbot AI truyền thống.

Bên cạnh chức năng hỏi đáp, hệ thống còn tích hợp các tính năng hỗ trợ học tập như quản lý tài liệu, tóm tắt bài học, tạo câu hỏi trắc nghiệm, Flashcard và lưu lịch sử hội thoại. Toàn bộ ứng dụng được triển khai trên nền tảng Amazon Web Services (AWS), đáp ứng các yêu cầu cơ bản về hiệu năng, bảo mật, khả năng mở rộng và quản lý hệ thống.

Thông qua quá trình thực hiện dự án, các mục tiêu chính đã đạt được gồm:

- Xây dựng nền tảng AI Learning Assistant dựa trên FastGPT.
- Ứng dụng Retrieval-Augmented Generation (RAG) để nâng cao chất lượng câu trả lời.
- Triển khai hệ thống trên Amazon EC2 bằng Docker Compose.
- Tích hợp MongoDB, PostgreSQL, MinIO và các dịch vụ AWS.
- Xây dựng kiến trúc có khả năng mở rộng và phù hợp với giai đoạn MVP.

---

## 7.2 Hạn chế

Mặc dù đã đáp ứng các mục tiêu đề ra, hệ thống vẫn còn một số hạn chế:

- Kiến trúc hiện tại sử dụng một Amazon EC2 nên chưa đáp ứng yêu cầu sẵn sàng cao (High Availability).
- Chưa triển khai Auto Scaling và Load Balancer.
- Chất lượng câu trả lời vẫn phụ thuộc vào nội dung và chất lượng của tài liệu được tải lên.
- Chưa hỗ trợ ứng dụng di động và làm việc ngoại tuyến.
- Một số tính năng AI nâng cao vẫn đang trong giai đoạn nghiên cứu và phát triển.

---

## 7.3 Hướng phát triển

Trong tương lai, AI Learning Assistant Platform sẽ được mở rộng theo các hướng sau:

- Triển khai Amazon ECS hoặc Amazon EKS để nâng cao khả năng mở rộng.
- Sử dụng Application Load Balancer và Auto Scaling nhằm hỗ trợ nhiều người dùng đồng thời.
- Tích hợp thêm các mô hình AI như Amazon Bedrock, Google Gemini hoặc OpenAI.
- Mở rộng các chức năng học tập như AI Tutor, Mindmap, Speech-to-Text và Text-to-Speech.
- Phát triển ứng dụng trên nền tảng Android và iOS.
- Tối ưu quy trình RAG để nâng cao tốc độ và độ chính xác của hệ thống.
- Hoàn thiện cơ chế giám sát, sao lưu và phục hồi dữ liệu nhằm tăng tính ổn định và an toàn trong quá trình vận hành.

Những định hướng trên sẽ giúp AI Learning Assistant Platform trở thành một nền tảng học tập thông minh có khả năng phục vụ nhiều đối tượng người dùng và đáp ứng tốt hơn các nhu cầu trong môi trường giáo dục hiện đại.

---

## 7.4 Kết luận

AI Learning Assistant Platform là một giải pháp hỗ trợ học tập ứng dụng trí tuệ nhân tạo, được xây dựng trên nền tảng FastGPT và triển khai trên Amazon Web Services (AWS). Việc kết hợp công nghệ Retrieval-Augmented Generation (RAG) với Knowledge Base giúp hệ thống cung cấp câu trả lời bám sát tài liệu học tập, góp phần nâng cao hiệu quả học tập và giảm hiện tượng AI tạo thông tin không có căn cứ.

Với kiến trúc được thiết kế theo hướng mở, hệ thống có thể tiếp tục mở rộng và tích hợp thêm nhiều dịch vụ AI cũng như các dịch vụ AWS trong tương lai. Dự án không chỉ đáp ứng mục tiêu xây dựng một trợ lý học tập thông minh mà còn tạo nền tảng cho việc nghiên cứu, phát triển và ứng dụng Generative AI trong lĩnh vực giáo dục.

Bên cạnh việc xây dựng nền tảng học tập thông minh, dự án còn minh họa cách triển khai một ứng dụng Generative AI trên Amazon Web Services thông qua Docker Compose, Amazon EC2, Amazon S3, Amazon CloudWatch và các dịch vụ bảo mật của AWS. Đây là nền tảng để tiếp tục mở rộng hệ thống trong tương lai.