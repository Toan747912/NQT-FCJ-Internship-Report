---
title: "Clean up resources"
date: 2026-07-14
weight: 5
chapter: false
pre: " 5.5. "
---

#### Summary of what was completed

In this workshop I built an end-to-end serverless URL Shortener:

- **S3** serves the UI and connects to the backend via `config.js`.
- **Lambda Function URL** handles create, 302 redirect, stats, and CORS.
- **DynamoDB** stores `shortCode` ↔ `originalUrl` and `clickCount`.
- **CloudWatch + SNS** watch errors via metric filter / alarm.

The architecture is enough to demonstrate serverless in an internship report, while also exposing lab limits (HTTP website endpoint, Auth `NONE`, no custom domain / WAF / CI-CD yet).

#### Limits and next improvements

| Current limit | Improvement direction |
| ---------------- | ---------------- |
| S3 website endpoint over HTTP | CloudFront + ACM (HTTPS, custom domain) |
| Function URL Auth `NONE` | IAM/JWT, API keys, or WAF rate limits |
| Short random codes | collision checks, longer codes, or nanoid with existence checks |
| Monitoring mostly ERROR count | latency/error dashboards, multi-metric alarms |
| Manual console deploy | IaC (SAM/CDK/Terraform) + pipeline |

#### Resources to tear down after the demo

To avoid cost and leftover public endpoints, related resources should be removed:

1. Lambda `url-shortener-backend` (including Function URL).
2. DynamoDB table `url-shortener-links`.
3. Empty + delete bucket `url-shortener-frontend-forward`.
4. IAM role attached to Lambda (for example deleted role `url-shortener-backend-role-...`) and its DynamoDB policy.
5. CloudWatch Alarm `URLShortener-Errors` (and Throttles/Duration if present), metric filter, log group `/aws/lambda/url-shortener-backend` (if no longer needed).
6. SNS topic `url-shortener-alerts` / email subscription used for the alarm.

![cleanup](/images/5-Workshop/5.5-Don-dep/cleanup.png)

The screenshot records deleting the IAM role after removing the function — part of the real cleanup on the account.
