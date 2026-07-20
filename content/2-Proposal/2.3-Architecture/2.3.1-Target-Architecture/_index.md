---
title: "Target architecture direction"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.3.1 </b> "
---

```text
[ User ]
   │  HTTPS
   ▼
[ Route 53 + ACM ] (optional custom domain)
   │
   ▼
[ CloudFront + WAF ]
   │                │
   │ static         │ /api/*  (behavior)
   ▼                ▼
[ S3 origin         [ Lambda Function URL
  (OAC) ]             or API Gateway → Lambda ]
                        │
                        ▼
                   [ DynamoDB ]
                        │
              [ CloudWatch + SNS (+ Budgets) ]
```

**Principle:** stay serverless; push TLS and edge protection to CloudFront/WAF; shrink public S3; avoid long-term Auth `NONE` if truly public on the Internet.
