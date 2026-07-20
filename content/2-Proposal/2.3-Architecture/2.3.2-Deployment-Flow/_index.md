---
title: "Deployment flow after expansion"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.3.2 </b> "
---

1. User opens `https://short.example.com` (CloudFront).
2. Static assets (`index.html`, JS, images) come from S3 via OAC.
3. Browser calls the API on the same domain or a WAF-protected API domain.
4. Lambda still creates / redirects / returns stats on DynamoDB (with collision checks / TTL).
5. Metrics and logs go to CloudWatch; alarms / Budgets / SNS cover ops and cost.

Core business flow (create → redirect → stats) **stays the same**; changes focus on edge, security, and operations.
