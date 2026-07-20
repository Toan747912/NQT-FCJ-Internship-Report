---
title: "Translated Blogs"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

This section presents translated summaries of official AWS technical articles (Compute Blog, News Blog, Documentation, Database Blog, Cloud Operations Blog). Each entry lists the source, main content, and notable technical points — chosen because they map to the **serverless URL Shortener** architecture in the Workshop section (**S3 + Lambda Function URL + DynamoDB + CloudWatch**).

### [Blog 1 – Build a Serverless, Private URL Shortener](3.1-Blog1/)

Summary of AWS’s serverless URL shortener guide (Lambda + S3 + API Gateway, S3 as a redirection engine) compared with the Function URL + DynamoDB design in my workshop.

### [Blog 2 – Announcing AWS Lambda Function URLs](3.2-Blog2/)

Summary of Function URLs — built-in HTTPS endpoints for a single Lambda function — the backend mechanism I used instead of API Gateway, including CORS and limits versus API Gateway.

### [Blog 3 – Tutorial: Configuring a static website on Amazon S3](3.3-Blog3/)

Summary of the official Static Website Hosting tutorial (Block Public Access and Bucket Policy) — matching frontend work in section 5.4.

### [Blog 4 – Implement resource counters with Amazon DynamoDB](3.4-Blog4/)

Summary of DynamoDB resource-counter patterns (atomic counters, ConditionExpression, accuracy limits) — matching `clickCount` on redirect.

### [Blog 5 – How to get notified on specific Lambda function error patterns using CloudWatch](3.5-Blog5/)

Summary of alerting on Lambda log error patterns via CloudWatch / SNS — related to the metric filter + alarm in section 5.3.3.
