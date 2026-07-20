---
title: "Khuyến nghị kiểm soát chi phí"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.6.3 </b> "
---

- Tạo **AWS Budget** (ví dụ ngưỡng $5 / $10) + email SNS.
- Đặt **retention** CloudWatch Logs ngắn cho lab (7–14 ngày).
- Sau demo: xoá / disable CloudFront, empty S3, xoá bảng DynamoDB nếu không cần.
- Tránh WAF / multi-region / retention dài khi chưa cần bằng chứng trong báo cáo.
- Theo dõi Cost Explorer theo service hàng tuần trong giai đoạn mở rộng.
