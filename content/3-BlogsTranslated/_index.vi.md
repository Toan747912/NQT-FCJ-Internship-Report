---
title: "Các bài blogs đã dịch"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Phần này trình bày bản dịch và tóm tắt nội dung các bài viết kỹ thuật chính thức từ AWS (Compute Blog, News Blog, Documentation, Database Blog, Cloud Operations Blog). Mỗi mục nêu rõ nguồn gốc bài viết, nội dung chính và các điểm kỹ thuật đáng chú ý — được chọn vì khớp với kiến trúc **URL Shortener serverless** mình triển khai ở mục Workshop (**S3 + Lambda Function URL + DynamoDB + CloudWatch**).

### [Blog 1 – Build a Serverless, Private URL Shortener](3.1-Blog1/)

Tóm tắt hướng dẫn xây URL shortener serverless của AWS (Lambda + S3 + API Gateway, dùng S3 làm redirection engine) và so sánh với thiết kế Lambda Function URL + DynamoDB trong workshop.

### [Blog 2 – Announcing AWS Lambda Function URLs](3.2-Blog2/)

Tóm tắt Function URL — endpoint HTTPS gắn sẵn cho một hàm Lambda — cơ chế backend mình dùng thay cho API Gateway, kèm CORS và giới hạn so với API Gateway.

### [Blog 3 – Tutorial: Configuring a static website on Amazon S3](3.3-Blog3/)

Tóm tắt tài liệu chính thức cấu hình Static Website Hosting, Block Public Access và Bucket Policy — khớp phần frontend mục 5.4.

### [Blog 4 – Implement resource counters with Amazon DynamoDB](3.4-Blog4/)

Tóm tắt các pattern đếm tài nguyên trên DynamoDB (atomic counter, ConditionExpression, giới hạn độ chính xác) — khớp `clickCount` khi redirect.

### [Blog 5 – How to get notified on specific Lambda function error patterns using CloudWatch](3.5-Blog5/)

Tóm tắt cách nhận cảnh báo theo pattern lỗi trong log Lambda qua CloudWatch / SNS — liên hệ metric filter + alarm ở mục 5.3.3.
