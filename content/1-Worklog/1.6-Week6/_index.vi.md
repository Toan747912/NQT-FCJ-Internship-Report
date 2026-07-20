---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Thời gian:** 25/05/2026 – 31/05/2026

### Mục tiêu của tuần 6:

* Phát triển ứng dụng serverless bằng Lambda, API Gateway và Step Functions.
* Nắm được kiến trúc event-driven cùng mô hình tính phí theo mỗi lượt gọi.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Lab 1: Viết hàm Lambda bằng Python để xóa các EC2 snapshot cũ hơn 30 ngày, kích hoạt bởi EventBridge vào 2:00 AM mỗi ngày. | 25/05/2026 | 25/05/2026 | <https://000022.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |
| 3 | Lab 2: Dựng REST API cho Book Store, kết hợp API Gateway, Lambda và DynamoDB (CRUD, trả JSON status code phù hợp). | 26/05/2026 | 27/05/2026 | <https://000078.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |
| 4 | Hoàn thiện thêm backend Book Store; tích hợp thêm S3 khi cần; rà soát lại response của API. | 28/05/2026 | 28/05/2026 | <https://000078.awsstudygroup.com/><br><https://000079.awsstudygroup.com/> |
| 5 | Lab 3: Dựng workflow bằng Step Functions — ValidateOrder → ProcessPayment → UpdateInventory → SendNotification. | 29/05/2026 | 29/05/2026 | <https://000047.awsstudygroup.com/> |
| 6 | Thử nghiệm cơ chế error handling / retry; chỉnh Lambda timeout từ 3s lên 30s và tối ưu để rút ngắn cold start. | 30/05/2026 | 30/05/2026 | <https://000047.awsstudygroup.com/><br><https://000077.awsstudygroup.com/> |

### Những gì đã hoàn thành trong tuần 6:

* Nắm được kiến trúc event-driven và lý do serverless mang lại lợi ích.
* Hoàn thiện REST API Book Store bằng API Gateway, Lambda và DynamoDB.
* Dựng được workflow nhiều bước bằng Step Functions, có xử lý lỗi và retry.

### Khó khăn và cách giải quyết:

* Lambda liên tục timeout với giới hạn mặc định 3 giây → nâng timeout lên 30 giây và tinh gọn code để giảm cold start.

### Kế hoạch cho tuần kế tiếp:

* Tìm hiểu Infrastructure as Code qua CloudFormation, CDK, cùng các CI/CD pipeline.
