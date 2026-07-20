---
title: "Các thành phần nên bổ sung"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.3.3 </b> "
---

| Thành phần | Vai trò |
| --- | --- |
| Amazon CloudFront | HTTPS edge, cache tĩnh, gom entry point |
| ACM | Chứng chỉ TLS |
| Route 53 (tuỳ chọn) | Custom domain DNS |
| AWS WAF | Rate limit / rule bảo vệ API |
| CloudFront OAC | Truy cập S3 không cần public bucket rộng |
| AWS Budgets | Cảnh báo ngân sách |
| SAM / CDK / Terraform | IaC tái dựng môi trường |
| (Tuỳ chọn) API Gateway | Khi cần usage plan, authorizer, stage chặt hơn Function URL |

Giữ nguyên DynamoDB và phần lớn logic handler; thay đổi cấu hình triển khai và lớp biên trước khi đổi sâu application code.
