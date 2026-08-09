---
title: "Cấu hình IAM"
date: 2026-08-07
weight: 3
chapter: false
pre: " <b> 5.2.3. </b> "
---

## Mục tiêu

Thiết lập quyền truy cập AWS nhằm hỗ trợ quá trình triển khai và quản lý tài nguyên của **AI Learning Assistant Platform**, đồng thời tuân thủ các khuyến nghị về bảo mật của AWS.

---

## Nội dung thực hiện

AWS khuyến nghị không sử dụng **Root Account** cho các hoạt động triển khai và vận hành hệ thống hằng ngày. Thay vào đó, mỗi thành viên trong nhóm được cấp một **IAM User** riêng để thực hiện các thao tác trên các dịch vụ AWS.

Trong workshop này, nhóm sử dụng hai IAM User tương ứng với hai thành viên tham gia triển khai. Ngoài ra, một IAM User riêng được sử dụng cho quy trình **GitHub Actions** nhằm phục vụ tự động hóa CI/CD.

Để đơn giản hóa quá trình thực hành và đảm bảo quá trình triển khai diễn ra thuận lợi, các IAM User được cấp chính sách **AdministratorAccess**. Trong môi trường triển khai thực tế (Production), nên áp dụng nguyên tắc **Least Privilege**, chỉ cấp các quyền cần thiết cho từng người dùng hoặc từng tác vụ.

Ngoài ra, cần tuân thủ các nguyên tắc bảo mật sau:

- Không sử dụng Root Account cho các thao tác triển khai hằng ngày.
- Không lưu trữ **Access Key ID** và **Secret Access Key** trực tiếp trong mã nguồn.
- Không đưa thông tin xác thực lên GitHub Repository.
- Lưu trữ các thông tin xác thực cần thiết bằng **GitHub Secrets** khi cấu hình quy trình CI/CD.

---

## Quy trình cấu hình IAM

Quy trình cấu hình IAM được thực hiện như sau:

1. Đăng nhập vào **AWS Management Console**.
2. Truy cập dịch vụ **AWS Identity and Access Management (IAM)**.
3. Chọn **Users** và tạo IAM User cho từng thành viên.
4. Gán chính sách **AdministratorAccess** cho các IAM User phục vụ triển khai workshop.
5. Kiểm tra danh sách IAM Users và các quyền được cấp sau khi hoàn tất cấu hình.

---

## Kết quả

Sau khi hoàn thành bước này, các IAM User đã được tạo và cấu hình thành công, sẵn sàng sử dụng để triển khai và quản lý các tài nguyên AWS của AI Learning Assistant Platform.

> **Hình 5.2.3. Danh sách IAM Users được sử dụng trong workshop.**
> ![Hình 5.2.3](/images/5.2.3.png)

> **Hình 5.2.4. Quyền được gán cho IAM User.**
> ![Hình 5.2.4](/images/5.2.4.png)