---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Thời gian:** 11/05/2026 – 17/05/2026

### Mục tiêu của tuần 4:

* Triển khai và vận hành Amazon EC2.
* Thiết lập Auto Scaling kết hợp giám sát bằng CloudWatch.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Lab 1: Dựng một instance EC2 (Amazon Linux 2), cài đặt Apache, mở port 80/443, và truy cập qua Public IP. | 11/05/2026 | 11/05/2026 | <https://000004.awsstudygroup.com/> |
| 3 | Ôn lại AMI, Key Pair, Elastic IP; siết chặt Security Group SSH chỉ cho phép IP cá nhân. | 12/05/2026 | 12/05/2026 | <https://000004.awsstudygroup.com/> |
| 4 | Lab 2: Thiết lập Launch Template cùng Auto Scaling Group (min=1, max=3) dựa trên mức sử dụng CPU. | 13/05/2026 | 13/05/2026 | <https://000006.awsstudygroup.com/> |
| 5 | Lab 3: Dựng CloudWatch Dashboard (CPU, Network, StatusCheck) và kích hoạt Alarm + thông báo SNS khi CPU vượt 70%. | 14/05/2026 | 14/05/2026 | <https://000036.awsstudygroup.com/><br><https://000008.awsstudygroup.com/> |
| 6 | Xác nhận Auto Scaling hoạt động đúng khi có tải; xem lại toàn bộ vòng đời EC2 (launch/stop/start/terminate). | 15/05/2026 | 15/05/2026 | <https://000006.awsstudygroup.com/><br><https://000004.awsstudygroup.com/> |

### Những gì đã hoàn thành trong tuần 4:

* Nắm vững vòng đời EC2 và đưa được web server vào hoạt động trên cloud.
* Vận hành thành công Auto Scaling dựa trên CPU.
* Xây dựng cơ chế giám sát chủ động kết hợp CloudWatch và SNS.

### Khó khăn và cách giải quyết:

* SSH thất bại vì port 22 chưa được mở → khắc phục bằng cách chỉ cho phép inbound SSH từ IP cá nhân (thay vì 0.0.0.0/0).

### Kế hoạch cho tuần kế tiếp:

* Tìm hiểu các dịch vụ lưu trữ: Amazon S3, RDS và DynamoDB.
