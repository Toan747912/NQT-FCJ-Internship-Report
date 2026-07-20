---
title: "Deploy Backend"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.3. "
---

#### Goal

Deploy the business layer: Lambda receives HTTPS via Function URL, reads/writes DynamoDB, returns JSON or 302 redirects — plus basic error monitoring with CloudWatch / SNS.

#### What I did

1. Created `url-shortener-backend` (Node.js 20.x) with a DynamoDB-capable execution role.
2. Implemented handler logic: `POST /`, `GET /{shortCode}`, `GET /stats/{shortCode}`, CORS/OPTIONS (including atomic `clickCount`).
3. Enabled Function URL (Auth `NONE` + CORS).
4. Tested with curl/PowerShell and verified DynamoDB items.
5. Added metric filter + alarm + SNS on `[ERROR]` logs.

Details:

- [Create Lambda function & Function URL](5.3.1-tao-lambda/)
- [Test API](5.3.2-test-lambda/)
- [CloudWatch + SNS monitoring](5.3.3-giam-sat/)
