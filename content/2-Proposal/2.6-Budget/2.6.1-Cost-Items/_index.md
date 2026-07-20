---
title: "Items that may add cost"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.6.1 </b> "
---

| Item | Notes |
| --- | --- |
| CloudFront | Requests + egress; public ACM certs are typically no charge |
| S3 | Small storage + GETs; website requests |
| Lambda | Requests + duration (usually tiny in a lab) |
| DynamoDB on-demand | Pay for actual RRU/WRU |
| CloudWatch Logs / Alarms | Ingestion + retention; metric alarms |
| SNS | Email notifications (Free Tier limits apply) |
| WAF (if enabled) | Rule / request fees — enable only when needed |

Detailed estimates should use the [AWS Pricing Calculator](https://calculator.aws/) for `ap-southeast-1` before long-running expansion.
