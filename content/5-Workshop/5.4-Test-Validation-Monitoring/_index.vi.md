---
title: "Kiểm thử, Xác thực và Giám sát"
date: 2026-08-07
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Mục tiêu

Sau khi hoàn thành quá trình triển khai **AI Learning Assistant Platform** trên **Amazon Web Services (AWS)**, cần tiến hành kiểm thử và giám sát hệ thống để đảm bảo ứng dụng hoạt động đúng và các tài nguyên AWS được theo dõi trong quá trình vận hành.

Trong phần này, hệ thống sẽ được kiểm tra thông qua **Functional Testing**, theo dõi bằng **Amazon CloudWatch** và thiết lập **Alerting** để phát hiện các vấn đề có thể xảy ra trong quá trình vận hành.

---

## Nội dung

Workshop này bao gồm các nội dung kiểm thử và giám sát sau:

### [1. Kiểm thử chức năng](./5.4.1-functional-testing)

- Kiểm tra các chức năng chính của **AI Learning Assistant Platform** sau khi được triển khai trên Amazon EC2.

---

### [2. Giám sát](./5.4.2-monitoring)

- Sử dụng **Amazon CloudWatch** để theo dõi tình trạng hoạt động và các Metrics của tài nguyên AWS được sử dụng trong hệ thống.

---

### [3. Cảnh báo](./5.4.3-alerting)

- Thiết lập cảnh báo bằng **Amazon CloudWatch Alarm** nhằm phát hiện các tình trạng bất thường của hệ thống và tài nguyên AWS.

---

