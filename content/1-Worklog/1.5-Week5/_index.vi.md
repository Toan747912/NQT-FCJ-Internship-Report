---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Thời gian:** 18/05/2026 – 20/05/2026

### Mục tiêu của tuần 5:

* Thực hành các dịch vụ lưu trữ đám mây: S3, RDS, DynamoDB, ElastiCache.
* Biết cách lựa chọn giải pháp lưu trữ phù hợp dựa trên use case, chi phí và hiệu năng.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Lab 1: Lưu trữ website tĩnh bằng S3 — tải lên file HTML/CSS/JS, bật tính năng hosting, áp dụng Bucket Policy cho phép public read. Lab 2: Dựng RDS MySQL trong Private Subnet, bật Multi-AZ; kết nối từ EC2 và thực hiện CRUD. | 18/05/2026 | 18/05/2026 | <https://000057.awsstudygroup.com/><br><https://000005.awsstudygroup.com/> |
| 3 | Lab 3: Dựng bảng DynamoDB (Partition/Sort Key); thao tác PutItem, GetItem, Query, Scan; đối chiếu với GSI. | 19/05/2026 | 19/05/2026 | <https://000060.awsstudygroup.com/><br><https://000039.awsstudygroup.com/> |
| 4 | Lab 4: Dựng ElastiCache Redis để cache kết quả truy vấn RDS (độ trễ giảm từ ~50ms xuống ~2ms). Tổng kết ưu nhược điểm giữa S3 / RDS / DynamoDB / ElastiCache; rà soát Security Group RDS ← EC2. | 20/05/2026 | 20/05/2026 | <https://000061.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |

### Những gì đã hoàn thành trong tuần 5:

* Đưa thành công website tĩnh lên S3.
* Dựng RDS Multi-AZ và thực hành truy vấn DynamoDB với GSI.
* Giảm khoảng 25 lần độ trễ truy vấn nhờ áp dụng ElastiCache Redis.

### Khó khăn và cách giải quyết:

* EC2 không thể kết nối tới RDS vì Security Group của RDS chặn inbound từ SG của EC2 → đã chỉnh lại inbound rule.

### Kế hoạch cho tuần kế tiếp:

* Nghiên cứu kiến trúc Serverless với AWS Lambda và API Gateway.
