---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Thời gian:** 04/05/2026 – 06/05/2026

### Mục tiêu tuần 3:

* Thiết kế và dựng hạ tầng mạng dựa trên Amazon VPC.
* Thiết lập Public/Private Subnet cùng IGW, NAT Gateway, Security Groups và NACL.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Nghiên cứu kiến trúc VPC (CIDR, Subnet, Route Table, IGW). Lab 1: Dựng VPC 10.0.0.0/16, khởi tạo Public & Private Subnet, thiết lập Internet Gateway. | 04/05/2026 | 04/05/2026 | <https://000003.awsstudygroup.com/> |
| 3 | Thiết lập NAT Gateway cho Private Subnet; so sánh Security Group (stateful) với NACL (stateless). | 05/05/2026 | 05/05/2026 | <https://000003.awsstudygroup.com/> |
| 4 | Lab 2: Networking Workshop — mô hình multi-tier (web ở public, DB ở private); tìm lỗi Route Table / NAT; xác nhận private subnet kết nối ra internet được qua NAT Gateway. | 06/05/2026 | 06/05/2026 | <https://000092.awsstudygroup.com/><br><https://000003.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

* Dựng thành công VPC gồm public/private subnet, IGW và NAT Gateway.
* Hiểu được cách traffic di chuyển qua Route Table.
* Phân biệt rõ giữa Security Group và Network ACL.

### Khó khăn và cách giải quyết:

* NAT Gateway bị lỗi vì thiếu route trong Route Table của private subnet → tự tìm và sửa lỗi Route Table dựa theo tài liệu lab.

### Kế hoạch tuần tiếp theo:

* Nghiên cứu Amazon EC2 — cách khởi chạy máy chủ ảo và thiết lập Auto Scaling.
