---
title: "Remaining limitations"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.2.1 </b> "
---

| Group | Current limitation | Impact |
| --- | --- | --- |
| Frontend / edge | Default S3 website endpoint is **HTTP**; no CloudFront / custom domain | No TLS; browser “Not secure”; hard to attach a real domain |
| API | Function URL Auth **`NONE`**, CORS `*` | Anyone who knows the URL can call create APIs |
| Frontend storage | Public bucket `GetObject` | Static objects are fully public; hard to enforce production least privilege |
| Data | Short random codes; no TTL / item lifecycle | Collision risk at scale; demo data can linger unnecessarily |
| Observability | Mostly `[ERROR]` filter + one alarm | Weak latency / 4xx–5xx visibility and ops dashboards |
| Deployment | Many console steps | Hard to reproduce, easy environment drift, hard to review changes |
| Cost | No mandatory Budgets / log lifecycle | Log groups and demo resources may incur quiet cost |

These limits **do not erase** the completed lab value; they define the gaps the proposal should close toward production.
