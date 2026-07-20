---
title: "Định hướng kiến trúc mục tiêu"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.3.1 </b> "
---

```text
[ User ]
   │  HTTPS
   ▼
[ Route 53 + ACM ] (tuỳ chọn custom domain)
   │
   ▼
[ CloudFront + WAF ]
   │                │
   │ static         │ /api/*  (behavior)
   ▼                ▼
[ S3 origin         [ Lambda Function URL
  (OAC) ]             hoặc API Gateway → Lambda ]
                        │
                        ▼
                   [ DynamoDB ]
                        │
              [ CloudWatch + SNS (+ Budgets) ]
```

**Nguyên tắc:** giữ serverless; đẩy TLS và bảo vệ biên ra CloudFront/WAF; thu hẹp public S3; API không còn Auth `NONE` mặc định nếu public Internet thật.
