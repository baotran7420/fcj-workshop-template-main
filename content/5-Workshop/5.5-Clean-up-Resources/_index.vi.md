---
title: "Dọn dẹp tài nguyên"
date: 2026-08-07
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---


> Việc dọn dẹp tài nguyên sau khi hoàn thành quá trình thực hành là cần thiết để tránh phát sinh chi phí ngoài ý muốn trên tài khoản AWS.

## Mục tiêu

Sau khi hoàn thành quá trình triển khai và kiểm thử **AI Learning Assistant Platform**, tiến hành dọn dẹp các tài nguyên AWS không còn sử dụng.

Việc này giúp giải phóng tài nguyên, hạn chế phát sinh chi phí và đảm bảo tài khoản AWS không duy trì các dịch vụ không cần thiết.

---

## Nội dung thực hiện

### 1. Xóa Amazon EC2 Instance

Sau khi hoàn tất quá trình kiểm thử, tiến hành Terminate EC2 Instance đang sử dụng để triển khai hệ thống.

Các bước thực hiện:

1. Truy cập **Amazon EC2 Console**.
2. Chọn **Instances**.
3. Chọn Instance **ai-learning-assistant**.
4. Chọn **Instance state**.
5. Chọn **Terminate instance**.
6. Xác nhận thao tác Terminate.

Sau khi thực hiện, kiểm tra trạng thái của Instance. Instance sẽ chuyển sang trạng thái **Shutting-down** và sau đó là **Terminated**.

> **Hình 5.5.1. Thực hiện Terminate Amazon EC2 Instance sau khi hoàn thành triển khai.**

> ![Hình 5.5.1](/images/5.5.1.png)

---

### 2. Giải phóng Elastic IP

Elastic IP không còn sử dụng nên được giải phóng để tránh phát sinh chi phí khi địa chỉ IP không được gắn với tài nguyên cần thiết.

Các bước thực hiện:

1. Truy cập **Amazon EC2 Console**.
2. Chọn **Elastic IPs**.
3. Chọn Elastic IP đã sử dụng cho EC2 Instance.
4. Chọn **Actions**.
5. Nếu IP vẫn đang được Associate, thực hiện **Disassociate Elastic IP address** trước.
6. Chọn **Actions → Release Elastic IP address**.
7. Xác nhận thao tác Release.

Sau khi hoàn tất, Elastic IP sẽ được trả về Amazon và không còn nằm trong danh sách các địa chỉ IP được cấp phát cho tài khoản.

> **Hình 5.5.2. Thực hiện Release Elastic IP address sau khi hoàn thành triển khai.**

> ![Hình 5.5.2](/images/5.5.2.png)

---

### 3. Xóa Amazon ECR Repository

Nếu Amazon ECR Repository không còn được sử dụng, tiến hành xóa Repository và các Docker Image liên quan.

Các bước thực hiện:

1. Truy cập **Amazon Elastic Container Registry (Amazon ECR)**.
2. Chọn **Repositories**.
3. Chọn Repository **ai-learning-assistant**.
4. Chọn **Delete**.
5. Xác nhận thao tác xóa Repository.

> **Lưu ý:** Việc xóa Repository sẽ xóa các Docker Images được lưu trữ bên trong Repository. Chỉ thực hiện bước này khi các Images không còn cần thiết.

> **Hình 5.5.3. Xóa Amazon ECR Repository của AI Learning Assistant Platform.**

> ![Hình 5.5.3](/images/5.5.3.png)

---

### 4. Xóa dữ liệu trên Amazon S3

Nếu hệ thống có sử dụng **Amazon S3** để lưu trữ dữ liệu backup hoặc các dữ liệu tạm thời, tiến hành làm trống Bucket trước khi xóa.

Các bước thực hiện:

1. Truy cập **Amazon S3**.
2. Chọn Bucket chứa dữ liệu backup của hệ thống.
3. Chọn **Empty**.
4. Xác nhận thao tác xóa toàn bộ dữ liệu trong Bucket.
5. Sau khi Bucket đã được làm trống, chọn **Delete**.
6. Nhập tên Bucket để xác nhận thao tác xóa.

> **Lưu ý:** Kiểm tra kỹ dữ liệu trong Bucket trước khi xóa để tránh mất các dữ liệu cần thiết.

> **Hình 5.5.4. Xóa Amazon S3 Bucket sau khi hoàn thành triển khai.**

> ![Hình 5.5.4](/images/5.5.4.png)

---

## Kiểm tra sau khi dọn dẹp

Sau khi hoàn thành các bước Clean-up, kiểm tra lại các dịch vụ AWS để đảm bảo các tài nguyên không còn sử dụng đã được xóa hoặc giải phóng.

Có thể kiểm tra:

- **Amazon EC2:** Instance đã chuyển sang trạng thái **Terminated**.
- **Elastic IP:** Địa chỉ IP không còn được Allocate.
- **Amazon ECR:** Repository **ai-learning-aassistant** đã được xóa nếu không còn sử dụng.
- **Amazon S3:** Bucket không còn dữ liệu hoặc đã được xóa nếu không cần thiết.

---

## Kết quả

Sau khi hoàn thành quá trình **Clean-up**, các tài nguyên AWS không còn cần thiết cho **AI Learning Assistant Platform** đã được xóa hoặc giải phóng.

Việc dọn dẹp tài nguyên giúp:

- Hạn chế phát sinh chi phí AWS ngoài dự kiến.
- Giải phóng các tài nguyên không còn sử dụng.
- Đảm bảo tài khoản AWS được quản lý hiệu quả.
- Hoàn tất chu trình triển khai, kiểm thử và vận hành dự án trên AWS.

> **Lưu ý:** Nếu dự án vẫn cần tiếp tục sử dụng EC2, ECR hoặc S3 cho quá trình phát triển và demo, không cần xóa các tài nguyên tương ứng. Chỉ thực hiện Clean-up đối với những tài nguyên không còn cần thiết.