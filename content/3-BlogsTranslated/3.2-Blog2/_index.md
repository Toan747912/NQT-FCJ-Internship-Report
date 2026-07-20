---
title: "Lambda Function URLs"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Announcing AWS Lambda Function URLs: Built-in HTTPS Endpoints for Single-Function Microservices |
| Source | [AWS News Blog](https://aws.amazon.com/blogs/aws/announcing-aws-lambda-function-urls-built-in-https-endpoints-for-single-function-microservices/) |
| Topics | Lambda Function URL, HTTPS endpoint, CORS, IAM Auth / NONE, vs API Gateway |
| Workshop link | Section 5.3 — `url-shortener-backend` via Function URL |

#### 2. Summary

AWS announced **Lambda Function URLs**: built-in HTTPS endpoints for a single Lambda function, optional CORS, **without requiring** API Gateway or an ALB. Endpoints attach to an alias or `$LATEST` and can be created via console, SDKs, CloudFormation, SAM, or CDK.

Default protection uses **AWS IAM**. Auth type **`NONE`** enables a public endpoint (with resource-based policy updates). No separate fee beyond normal Lambda invoke cost. The feature targets **single-function** microservices that need public HTTP without full API Gateway platform features.

#### 3. Main content

##### 3.1. Why Function URLs exist

Previously, HTTPS access to Lambda usually meant API Gateway or ALB. For simple webhooks, form handlers, or fast prototypes, that middle layer can outweigh the business logic. Function URLs shorten the path: Lambda gets a stable HTTPS endpoint.

##### 3.2. When to use Function URLs

Best when one function serves one microservice endpoint and you do not need advanced validation, usage plans, API keys, custom authorizers, complex custom domains, or API Gateway caching — including lab/R&D scenarios.

##### 3.3. When to prefer API Gateway

When you need platform-level API management: varied route policies, fine throttling, custom authorizers, controlled stages, or richer WAF/usage-plan integrations.

##### 3.4. CORS and public access

Native CORS matters when the frontend origin differs (S3 website → API). Auth `NONE` fits intentionally public APIs; production should reconsider auth, rate limits, or CloudFront in front.

#### 4. Reflection

This article explains the **exact backend mechanism** in my shortener. `url-shortener-backend` exposes a Function URL with Auth `NONE` and CORS so the S3 frontend can call `POST /` and `GET /{shortCode}`.

![Lambda Function URL in the workshop](/images/3-BlogsTranslated/3.2-Blog2/function-url.png)

Compared with the Compute Blog shortener (API Gateway), Function URL reduced lab resources while keeping HTTPS. Accepted trade-off: no custom domain or advanced throttling yet — enough for the internship; real products may move to CloudFront / API Gateway as the article’s use-case split suggests.
