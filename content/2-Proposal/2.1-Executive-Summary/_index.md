---
title: "Executive summary"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.1. </b> "
---

#### Current project state

The Serverless URL Shortener already demonstrates an end-to-end AWS serverless shortener: static frontend on S3 Static Website Hosting, a single Lambda backend via Function URL (create, 302 redirect, stats), DynamoDB on-demand storage for `shortCode` ↔ `originalUrl` and `clickCount`, plus metric filter / CloudWatch Alarm / SNS on `[ERROR]` logs.

![Current deployed architecture](/images/2-Proposal/current-architecture.png)

#### Problems to address

Moving from lab to more sustainable operations still requires: frontend edge HTTPS, tighter API access (not long-term Auth `NONE`), edge protection (WAF / rate limits), stronger short-code strategy, deeper ops visibility (latency, dashboards), deployment automation (IaC / CI), and proactive cost control.

#### Proposal direction

| Proposal group | Goal | Value |
| --- | --- | --- |
| HTTPS and distribution edge | CloudFront + ACM in front of S3 / Function URL | TLS, custom domain, static caching |
| Access security | Reduce pure public buckets; API auth / signed access / IAM; WAF | Lower risk from public endpoints |
| API & data upgrades | Collision checks; TTL; optional API Gateway when needed | Higher business reliability |
| Observability | Latency/error dashboards, multi-metric alarms, log retention | Faster incident detection |
| Automation | SAM/CDK/Terraform + deploy pipeline | Reproducible environments, fewer manual mistakes |
| Cost control | Budgets/alerts, log/object lifecycle, shut down demo resources | Avoid overruns on a lab account |

#### Priority order

Prioritize **edge stability and security** first, business expansion later: CloudFront/HTTPS → tighten S3/API access → strengthen short codes & data → observability → IaC/CI → long-term cost control. This fits remaining report scope and personal budget limits.
