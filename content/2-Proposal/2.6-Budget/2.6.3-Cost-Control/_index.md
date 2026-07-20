---
title: "Cost-control recommendations"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.6.3 </b> "
---

- Create an **AWS Budget** (e.g. $5 / $10 thresholds) with SNS email.
- Keep CloudWatch Logs **retention** short for labs (7–14 days).
- After demos: delete/disable CloudFront, empty S3, delete DynamoDB tables if unused.
- Avoid WAF / multi-region / long retention until the report needs that evidence.
- Review Cost Explorer by service weekly during expansion.
