---
title: "Proposed future solutions"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.2.2 </b> "
---

1. **CloudFront + ACM** in front of S3 (and optionally Function URL) for HTTPS, custom domain, and static caching.
2. **Tighten S3 access**: move toward OAC with CloudFront; reduce reliance on public Bucket Policies.
3. **Tighten the API**: consider IAM / JWT / API key auth; WAF rate-based rules; narrow CORS to the real frontend domain.
4. **Strengthen short codes**: existence checks before Put, longer alphabet, optional nicer custom-domain paths.
5. **DynamoDB upgrades**: TTL for expired links; GSIs for owner/date queries when multi-user appears.
6. **Observability**: CloudWatch dashboards (latency, errors, throttles); multi-metric alarms; log retention lifecycle.
7. **IaC + CI**: SAM/CDK/Terraform for Lambda, DynamoDB, S3/CloudFront; branch-based deploy pipelines.
8. **Cost guardrails**: AWS Budgets, cost alarms, tear down demo resources after evaluation.

Solutions can ship independently by phase — no forced big-bang rewrite.
