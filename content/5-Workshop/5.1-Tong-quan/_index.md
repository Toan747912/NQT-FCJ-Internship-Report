---
title: "Architecture overview"
date: 2026-07-14
weight: 1
chapter: false
pre: " 5.1. "
---

#### Goal

Present the architecture I actually deployed: AWS components, how they call each other, and each Function URL API.

#### System architecture diagram

Deployed in **ap-southeast-1**: S3 (Static Website) + Lambda Function URL (Node.js) + DynamoDB (`url-shortener-links`, TTL) + IAM least privilege, plus CloudWatch / SNS error alerts.

![Serverless URL Shortener architecture](/images/5-Workshop/5.1-Tong-quan/architecture.png)

**Main flow on the diagram:**

1. User loads the static page from **S3 Static Website Hosting** (HTML/CSS/JS).
2. Browser calls the **Lambda Function URL** directly (`POST /`, `GET /{code}`, `GET /stats/{code}`).
3. Lambda reads/writes DynamoDB (`PutItem` / `UpdateItem` / `GetItem`) via a least-privilege IAM role.
4. DynamoDB returns data; Lambda prepares short URL, **302 redirect**, or stats.
5. Response back to the browser.
6–7. Logs/metrics → **CloudWatch** (metric filter `[ERROR]`, alarm) → **SNS** → admin email when thresholds are crossed.

When opening a short link, the browser calls Function URL (`GET /{shortCode}`) directly; Lambda returns **302** with `Location: originalUrl`. The S3 frontend is not involved in redirect.

#### Designed API flow

| Method & path | Purpose | DynamoDB write | Affects clicks |
| ------------- | -------- | ------------ | --------------- |
| `POST /` | Create short link | `PutItem` (+ `expiresAt` TTL) | No |
| `GET /{shortCode}` | Redirect to original URL | `UpdateItem` (`clickCount`, `lastClickedAt`) | Yes |
| `GET /stats/{shortCode}` | View stats | read | No |

Create flow:

1. User opens the S3 website and pastes a long URL.
2. `index.html` reads Function URL from `config.js` and calls `POST /` with `{ "url": "..." }`.
3. Lambda generates a 6-character `shortCode`, stores the item in DynamoDB, returns `{ shortCode, shortUrl, originalUrl }`.

Short-link open flow:

1. Client calls `GET /{shortCode}` on the Function URL.
2. Lambda atomically updates `clickCount` if the code exists; otherwise **404**.
3. Returns **302** to `originalUrl`.

#### Why Function URL instead of API Gateway

- The lab only needs a simple HTTPS API; Auth `NONE` + CORS is enough.
- Fewer resources to configure and clean up (no API Gateway stages/methods/integrations).
- Lower cost and complexity for an internal demo / internship report.

Trade-off: Function URL has fewer governance features than API Gateway (advanced throttling, API keys, usage plans). Acceptable for this shortener lab.

#### Why DynamoDB

The core problem is **key lookup** `shortCode` → `originalUrl`. On-demand DynamoDB fits: no capacity planning, low latency, no RDS instance ops. TTL via `expiresAt` lets items expire after the lab/demo window.

#### Architecture outcome

With all layers in place, the path is closed: create on S3 UI → store in DynamoDB → open short URL via Lambda → redirect + click count → stats / console inspection, plus CloudWatch → SNS monitoring.
