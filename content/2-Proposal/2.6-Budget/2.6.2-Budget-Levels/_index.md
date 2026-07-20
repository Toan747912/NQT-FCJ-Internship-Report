---
title: "Budget by expansion level"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.6.2 </b> "
---

| Level | Scope | Expected monthly cost (lab) |
| --- | --- | --- |
| M0 – Current | S3 + Lambda URL + DynamoDB + basic alarm | ~$0–2 (often Free Tier) |
| M1 – HTTPS edge | + CloudFront + ACM | ~$1–5 depending on traffic |
| M2 – Edge security | + minimal WAF rule | A few more USD if requests exist |
| M3 – Observability + IaC | Dashboards, moderate log retention | Mostly driven by log volume |

Numbers are directional for the report; refresh with Pricing Calculator / Cost Explorer when executing.
