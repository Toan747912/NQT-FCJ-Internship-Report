---
title: "Workshop"
date: 2026-07-14
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

#### Overview

Section 5 records how I deployed a **URL Shortener** in a fully **serverless** model on AWS. The goal was not only a working demo, but a clear understanding of how the pieces fit together: static frontend, business API, and low-latency key-value storage.

The architecture uses **Amazon S3** (Static Website Hosting) + **AWS Lambda Function URL** + **Amazon DynamoDB** in **ap-southeast-1 (Singapore)**. No EC2 and no API Gateway — Function URL is the public HTTPS API endpoint. Error monitoring uses **CloudWatch + SNS**.

![Serverless URL Shortener architecture](/images/5-Workshop/5.1-Tong-quan/architecture.png)

#### Project demo

**Demo video:** [Serverless URL Shortener — end-to-end walkthrough](https://drive.google.com/file/d/1az6EVbShi64-Lg72U0uZnOoewGKCVeXn/view?usp=drive_link)

#### Problem and approach

The app needs three core operations:

1. Accept a long URL → generate `shortCode` → store the mapping and return `shortUrl`.
2. When a user opens `shortUrl` → look up `originalUrl` → **HTTP 302** redirect, while incrementing `clickCount`.
3. Allow stats (`/stats/{shortCode}`) without increasing clicks.

For this lab, Function URL + on-demand DynamoDB is enough: fast to deploy, low pay-per-request cost, and a complete serverless path.

#### What was deployed

| Layer | Resource | Role |
| --- | ---------- | ------- |
| Frontend | S3 bucket `url-shortener-frontend-forward` | Serves UI (`index.html`, `config.js`) |
| Backend | Lambda `url-shortener-backend` + Function URL | Create, redirect, stats |
| Data | DynamoDB `url-shortener-links` (+ TTL `expiresAt`) | Stores `shortCode` ↔ `originalUrl`, `clickCount` |
| IAM | Role + DynamoDB policy | Least privilege for Lambda |
| Monitoring | CloudWatch metric filter + Alarm + SNS | Alerts on `[ERROR]` logs |

#### Section 5 structure

1. [Architecture overview](5.1-Tong-quan/) — request flow and service choices.
2. [Prerequisites](5.2-Chuan-bi/) — DynamoDB table and IAM role/policy.
3. [Deploy Backend](5.3-Backend/) — Lambda, Function URL, API tests, CloudWatch/SNS monitoring.
4. [Deploy Frontend](5.4-Frontend/) — S3 hosting, Bucket Policy, upload, e2e.
5. [Clean up](5.5-Don-dep/) — tear down resources after the demo.
