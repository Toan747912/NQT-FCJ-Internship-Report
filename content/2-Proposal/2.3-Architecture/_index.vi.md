---
title: "Kiến trúc giải pháp đề xuất"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.3. </b> "
---

Mục này mô tả kiến trúc mục tiêu sau khi mở rộng, vẫn giữ lõi S3 + Lambda + DynamoDB đã triển khai trong workshop.

#### Kiến trúc hiện tại (baseline)

![Kiến trúc hiện tại Serverless URL Shortener](/images/2-Proposal/current-architecture.png)

Baseline đã có: S3 Static Website → Lambda Function URL → DynamoDB, IAM least privilege, CloudWatch + SNS cảnh báo lỗi. Các đề xuất ở mục con bổ sung lớp biên HTTPS (CloudFront/WAF) và siết bảo mật, không thay thế lõi trên.

#### Nội dung

- [Định hướng kiến trúc mục tiêu](2.3.1-Target-Architecture/)
- [Luồng triển khai sau khi mở rộng](2.3.2-Deployment-Flow/)
- [Các thành phần nên bổ sung](2.3.3-Components-to-Add/)
