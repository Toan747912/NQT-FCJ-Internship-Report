---
title: "Triển khai Backend"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.3. "
---

#### Mục tiêu

Triển khai lớp xử lý nghiệp vụ: Lambda nhận HTTPS request qua Function URL, đọc/ghi DynamoDB, trả JSON hoặc redirect 302 — kèm giám sát lỗi cơ bản qua CloudWatch / SNS.

#### Việc đã làm

1. Tạo function `url-shortener-backend` (Node.js 20.x), gắn execution role có quyền DynamoDB.
2. Triển khai logic handler: `POST /`, `GET /{shortCode}`, `GET /stats/{shortCode}`, xử lý CORS/OPTIONS (kèm tăng `clickCount` atomic).
3. Bật Function URL (Auth `NONE` + CORS).
4. Kiểm thử bằng curl/PowerShell và đối chiếu dữ liệu trên DynamoDB.
5. Bổ sung metric filter + alarm + SNS khi log có `[ERROR]`.

Chi tiết từng bước:

- [Tạo Lambda function & Function URL](5.3.1-tao-lambda/)
- [Test API](5.3.2-test-lambda/)
- [Giám sát CloudWatch + SNS](5.3.3-giam-sat/)
