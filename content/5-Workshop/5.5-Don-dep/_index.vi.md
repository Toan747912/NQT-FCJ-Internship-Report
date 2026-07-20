---
title: "Dọn dẹp tài nguyên"
date: 2026-07-14
weight: 5
chapter: false
pre: " 5.5. "
---

#### Tổng kết những gì đã hoàn thành

Qua workshop này, mình đã dựng end-to-end một URL Shortener serverless:

- **S3** phục vụ UI và nối tới backend qua `config.js`.
- **Lambda Function URL** xử lý tạo mã, redirect 302, stats và CORS.
- **DynamoDB** lưu mapping `shortCode` ↔ `originalUrl` và `clickCount`.
- **CloudWatch + SNS** theo dõi lỗi qua metric filter / alarm.

Kiến trúc đủ để minh họa serverless trên báo cáo thực tập; đồng thời lộ rõ giới hạn lab (HTTP website endpoint, Auth `NONE`, chưa có custom domain / WAF / CI-CD).

#### Hạn chế và hướng cải thiện

| Hạn chế hiện tại | Hướng cải thiện |
| ---------------- | --------------- |
| S3 website endpoint HTTP | CloudFront + ACM (HTTPS, custom domain) |
| Function URL Auth `NONE` | IAM/JWT, API key, hoặc WAF rate limit |
| Short code ngẫu nhiên ngắn | kiểm tra collision, tăng độ dài, hoặc nanoid có kiểm tra tồn tại |
| Monitor mới ở mức ERROR count | dashboard latency/error rate, alarm đa chỉ số |
| Deploy tay trên console | infra as code (SAM/CDK/Terraform) + pipeline |

#### Danh sách tài nguyên cần thu hồi sau demo

Để tránh phát sinh chi phí / để lại endpoint public không cần thiết, các tài nguyên liên quan cần xóa:

1. Lambda `url-shortener-backend` (kèm Function URL).
2. DynamoDB table `url-shortener-links`.
3. Empty + delete bucket `url-shortener-frontend-forward`.
4. IAM role gắn Lambda (ví dụ role đã xoá dạng `url-shortener-backend-role-...`) và policy DynamoDB kèm theo.
5. CloudWatch Alarm `URLShortener-Errors` (và Throttles/Duration nếu có), metric filter, log group `/aws/lambda/url-shortener-backend` (nếu không còn cần).
6. SNS topic `url-shortener-alerts` / subscription email dùng cho alarm.

![cleanup](/images/5-Workshop/5.5-Don-dep/cleanup.png)

Ảnh trên ghi nhận bước xoá IAM role sau khi thu hồi function — một phần của quy trình dọn dẹp thực tế trên account.
