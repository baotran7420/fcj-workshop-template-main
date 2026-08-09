---
title: "Hướng tối ưu trong tương lai"
date: 2026-08-07
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---



Nếu dự án được nâng cấp từ phiên bản **MVP** lên môi trường **Enterprise Production**, kiến trúc hiện tại sử dụng một máy chủ **Amazon EC2** đơn lẻ nên được tái cấu trúc nhằm nâng cao khả năng mở rộng, tính sẵn sàng và khả năng quản lý hệ thống.

### 1. Di chuyển sang Amazon ECS / EKS

Thay vì chạy toàn bộ Docker Container trực tiếp trên một EC2 Instance, hệ thống có thể được triển khai trên một Cluster sử dụng **Amazon ECS** hoặc **Amazon EKS**.

Đặc biệt, **Amazon ECS với AWS Fargate** cho phép chạy Docker Container mà không cần tự quản lý máy chủ EC2.

Việc chuyển sang mô hình này giúp hệ thống:

- Tự động mở rộng tài nguyên khi lưu lượng tăng.
- Phân phối workload giữa nhiều Container.
- Tăng khả năng sẵn sàng của hệ thống.
- Giảm công việc quản lý máy chủ thủ công.

### 2. Tách rời Database

Trong kiến trúc hiện tại, các Database được triển khai cùng với hệ thống thông qua Docker Compose.

Trong tương lai, Database có thể được chuyển sang các dịch vụ **Managed Services** của AWS như:

- **Amazon RDS for PostgreSQL** cho PostgreSQL.
- **Amazon DocumentDB** cho các workload tương thích với MongoDB.

Việc sử dụng Managed Services giúp giảm công việc quản trị Database và hỗ trợ các cơ chế như **Backup, Monitoring và High Availability (Multi-AZ)** tùy theo cấu hình.

### 3. Sử dụng Application Load Balancer

Có thể triển khai **Application Load Balancer (ALB)** ở phía trước hệ thống để phân phối lưu lượng truy cập giữa các Application Server hoặc Container.

ALB có thể kết hợp với **AWS Certificate Manager (ACM)** để quản lý chứng chỉ và triển khai kết nối **SSL/TLS (HTTPS)**.

Kiến trúc này phù hợp hơn khi hệ thống được mở rộng thành nhiều Instance hoặc nhiều Application Container.

---

## Định hướng phát triển

Các cải tiến trên sẽ giúp **AI Learning Assistant Platform** chuyển từ mô hình triển khai đơn giản trên một EC2 Instance sang kiến trúc có khả năng mở rộng và vận hành phù hợp hơn với môi trường Production.

Các hướng phát triển tập trung vào ba yếu tố chính:

- **Scalability:** Có khả năng mở rộng khi số lượng người dùng tăng.
- **High Availability:** Hạn chế thời gian hệ thống bị gián đoạn.
- **Manageability:** Giảm công việc quản trị thủ công và tăng khả năng tự động hóa.