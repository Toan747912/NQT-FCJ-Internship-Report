---
title: "Risk assessment"
date: 2026-07-14
weight: 7
chapter: false
pre: " <b> 2.7. </b> "
---

| Risk | Impact | Likelihood | Mitigation |
| --- | --- | --- | --- |
| Abuse of Auth NONE API | High | Medium | WAF rate limit, auth, monitoring |
| Data exposure via public bucket | Medium | Medium | OAC, remove broad public GetObject |
| Short-code collision | Medium | Low→Med at scale | Existence checks, longer codes |
| CloudFront/WAF cost growth | Medium | Medium | Budgets; disable when not demoing |
| IaC complexity delays the report | Medium | Medium | Minimal IaC scope; HTTPS edge first |
| Break working demo during cutover | High | Low | Parallel deploy; DNS/CloudFront rollback |

**Contingency:** keep the current lab stack as fallback; shift traffic with DNS/CloudFront behaviors instead of deleting live resources by hand.
