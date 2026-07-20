---
title: "Implementation plan"
date: 2026-07-14
weight: 4
chapter: false
pre: " <b> 2.4. </b> "
---

#### Priority phases

| Phase | Main work | Verification |
| --- | --- | --- |
| P0 | CloudFront + ACM for S3 frontend | Site opens over HTTPS |
| P1 | OAC + shrink public bucket; tighten CORS | Less reliance on broad public GetObject |
| P2 | API auth / WAF rate limit | Less short-link creation abuse |
| P3 | Collision checks + DynamoDB TTL | Stronger codes; demo data can expire |
| P4 | Dashboards + multi-metric alarms + Budgets | Ops and cost visibility |
| P5 | IaC (SAM/CDK) + minimal pipeline | Reproducible deploys |

#### Delivery principles

- Do not break the working demo: parallel deploy / gradual cutover.
- Each phase has a test checklist (HTTPS, create, redirect, stats, alarms).
- Prefer edge/config changes before large handler rewrites.
- Stay Free Tier / low cost: disable unused CloudFront demos; apply log lifecycles.
