---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Thời gian:** 27/04/2026 – 29/04/2026

### Mục tiêu tuần 2:

* Kiểm soát danh tính người dùng và quyền truy cập thông qua AWS IAM.
* Đưa Least Privilege, MFA và IAM Role vào thực tế cho EC2.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Nghiên cứu mô hình IAM (User, Group, Role, Policy), nguyên tắc Least Privilege, MFA. Lab 1: Khởi tạo IAM Users, Groups (Dev, Ops), gắn Managed Policies, xác nhận bằng Policy Simulator. | 27/04/2026 | 27/04/2026 | <https://000002.awsstudygroup.com/> |
| 3 | Nghiên cứu IAM Permission Boundaries và cơ chế giới hạn quyền cho người dùng. | 28/04/2026 | 28/04/2026 | <https://000030.awsstudygroup.com/> |
| 4 | Lab 2: Dựng IAM Role cho EC2 (Instance Profile) để truy cập S3 mà không cần lưu Access Key; gắn Role vào instance, kiểm tra quyền truy cập; ôn tập IAM Role & Condition. | 29/04/2026 | 29/04/2026 | <https://000048.awsstudygroup.com/><br><https://000044.awsstudygroup.com/> |

### Kết quả đạt được tuần 2:

* Nắm vững User, Group, Role, Policy và tinh thần của nguyên tắc Least Privilege.
* Khởi tạo được IAM Users/Groups và xác nhận quyền hoạt động đúng qua Policy Simulator.
* Thiết lập xong IAM Role giúp EC2 truy cập S3 mà không cần đến Access Key.

### Khó khăn và cách giải quyết:

* Thường xuyên mắc lỗi cú pháp khi soạn IAM Policy dạng JSON → nhờ đến IAM Policy Editor trên Console và tra cứu tài liệu AWS.

### Kế hoạch tuần tiếp theo:

* Tìm hiểu sâu hơn về Amazon VPC — dựng hạ tầng mạng riêng ảo trên nền tảng AWS.
