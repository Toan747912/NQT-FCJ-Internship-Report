---
title: "Components to add"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.3.3 </b> "
---

| Component | Role |
| --- | --- |
| Amazon CloudFront | HTTPS edge, static cache, unified entry |
| ACM | TLS certificates |
| Route 53 (optional) | Custom domain DNS |
| AWS WAF | Rate limits / API protection rules |
| CloudFront OAC | S3 access without a broadly public bucket |
| AWS Budgets | Budget alerts |
| SAM / CDK / Terraform | IaC for reproducible environments |
| (Optional) API Gateway | When usage plans, authorizers, and stages outgrow Function URL |

Keep DynamoDB and most handler logic; change deployment wiring and the edge layer before deep application rewrites.
