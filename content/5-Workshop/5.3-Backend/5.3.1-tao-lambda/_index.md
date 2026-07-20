---
title: "Create Lambda function & Function URL"
date: 2026-07-14
weight: 1
chapter: false
pre: " 5.3.1. "
---

#### Function configuration

| Property | Value |
| ---------- | ------- |
| Name | `url-shortener-backend` |
| Runtime | Node.js 20.x |
| Handler file | `index.mjs` |
| Region | `ap-southeast-1` |
| Env | `TABLE_NAME=url-shortener-links` |
| Function URL Auth | `NONE` |
| CORS | Allow origin `*`, methods `GET, POST` (plus OPTIONS preflight) |

I chose Node.js 20 because the Lambda runtime already includes AWS SDK v3 (`@aws-sdk/client-dynamodb`, `@aws-sdk/lib-dynamodb`) — paste code in the console and run, with no `node_modules` packaging for this lab.

Function **`url-shortener-backend`** uses handler file `index.mjs`. In the code editor I wired the DynamoDB Document Client, `generateShortCode()` (~6 characters), and `isValidUrl()` (only `http`/`https`), then **Deploy** to update the function.

![Lambda url-shortener-backend code (index.mjs)](/images/5-Workshop/5.3-Backend/create-lambda.png)

#### Core handler logic

**1) Create — `POST /`**

- Parse JSON body for `url` and validate with `isValidUrl`.
- Generate a ~6-character random `shortCode` via `generateShortCode`.
- `PutCommand` into `TABLE_NAME` with `shortCode`, `originalUrl`, `clickCount: 0`, `createdAt`.
- Return `{ shortCode, shortUrl, originalUrl }` where `shortUrl = functionUrl + "/" + shortCode`.

**2) Redirect — `GET /{shortCode}`**

- `UpdateCommand` increments `clickCount` atomically.
- `ConditionExpression: attribute_exists(shortCode)` → missing code → **404**.
- Success → **302** with `Location: originalUrl`.

**3) Stats — `GET /stats/{shortCode}`**

- Return `{ shortCode, originalUrl, clickCount, createdAt }` **without** incrementing.

**4) CORS**

- JSON/redirect responses need `Access-Control-Allow-Origin: *` because the S3 website origin differs from the Function URL origin.
- `OPTIONS` preflight must return CORS headers — otherwise the browser blocks `POST` even if Lambda runs.

#### Function URL

After enabling Function URL (Auth type **NONE**, Invoke mode **BUFFERED**), I set CORS Allow origin `*`, Allow headers `content-type`, Allow methods `GET` / `POST`, then copied an endpoint like:

`https://xxxx.lambda-url.ap-southeast-1.on.aws/`

![Function URL + CORS for url-shortener-backend](/images/5-Workshop/5.3-Backend/function-url.png)

That value goes into frontend `config.js` (section 5.4). Auth `NONE` fits a public lab shortener; production should add auth, rate limits, or CloudFront in front.

#### Configuration pitfalls

- Wrong `TABLE_NAME`/region → Put/Update failures (visible in CloudWatch Logs).
- Role missing `dynamodb:UpdateItem` → create may work, redirect click increment fails.
- Enabling CORS only on Function URL is not enough if the handler omits CORS headers on real responses.
