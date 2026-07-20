---
title: "Tóm tắt điều hành"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.1. </b> "
---

#### Hiện trạng dự án

Dự án Serverless URL Shortener đã chứng minh khả năng triển khai end-to-end một ứng dụng rút gọn link trên AWS theo mô hình serverless: frontend tĩnh trên S3 Static Website Hosting, backend một hàm Lambda expose qua Function URL (tạo mã, redirect 302, stats), lưu mapping `shortCode` ↔ `originalUrl` và `clickCount` trên DynamoDB on-demand, kèm metric filter / CloudWatch Alarm / SNS khi log có `[ERROR]`.

![Kiến trúc hiện tại đã triển khai](/images/2-Proposal/current-architecture.png)

#### Vấn đề cần giải quyết

Khi chuyển từ môi trường lab sang hướng vận hành bền vững hơn, hệ thống còn thiếu các năng lực: HTTPS trên biên frontend, kiểm soát truy cập API (không để Auth `NONE` lâu dài), bảo vệ biên (WAF / rate limit), chiến lược short code chắc chắn hơn, quan sát vận hành sâu hơn (latency, dashboards), tự động hóa triển khai (IaC / CI), và quản trị chi phí chủ động.

#### Định hướng đề xuất

| Nhóm đề xuất | Mục tiêu | Giá trị đạt được |
| --- | --- | --- |
| HTTPS và biên phân phối | CloudFront + ACM trước S3 / Function URL | TLS, custom domain, cache tĩnh |
| Bảo mật truy cập | Hạn chế public bucket thuần; auth / signed URL / IAM cho API; WAF | Giảm rủi ro endpoint công khai |
| Nâng cấp API & dữ liệu | Kiểm tra collision short code; TTL; (tuỳ chọn) API Gateway khi cần | Độ tin cậy nghiệp vụ cao hơn |
| Observability | Dashboard latency/error, alarm đa chỉ số, log retention | Phát hiện sự cố nhanh hơn |
| Tự động hóa | SAM/CDK/Terraform + pipeline deploy | Tái dựng môi trường và giảm sai sót tay |
| Kiểm soát chi phí | Budgets/alerts, lifecycle log/object, tắt tài nguyên demo | Tránh overrun trên account lab |

#### Thứ tự ưu tiên

Ưu tiên **ổn định và bảo mật biên** trước, mở rộng nghiệp vụ sau: CloudFront/HTTPS → siết truy cập S3/API → củng cố short code & dữ liệu → nâng observability → IaC/CI → tối ưu chi phí dài hạn. Cách sắp xếp này phù hợp thời gian còn lại / phạm vi báo cáo và ngân sách cá nhân.
