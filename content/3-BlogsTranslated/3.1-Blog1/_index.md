---
title: "Serverless URL Shortener"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Build a Serverless, Private URL Shortener |
| Source | [AWS Compute Blog](https://aws.amazon.com/blogs/compute/build-a-serverless-private-url-shortener/) |
| Topics | Serverless URL shortener, Lambda, API Gateway, S3 website redirect, CloudFront |
| Workshop link | Section 5 — compare the AWS sample design with my Function URL + DynamoDB architecture |

#### 2. Summary

The article starts from a practical Solutions Architect need: pre-signed URLs are long and hard to share, so the author wants a **private**, self-controlled URL shortener without managing servers. The proposed design uses managed services: **S3**, **API Gateway**, **Lambda**, optionally **CloudFront**, packaged with **CloudFormation**.

The key technical idea is **S3 website redirects**: each short link is an (often empty) object with `WebsiteRedirectLocation` metadata pointing to the long URL. Opening the short URL on the website endpoint makes S3 return an HTTP redirect **without Lambda running at redirect time**.

Creating short links uses a static HTML admin page on S3. Shorten → POST to API Gateway → Lambda validates → random short id → PutObject with redirect metadata → return the short URL.

#### 3. Main content

##### 3.1. S3 as a redirection engine

After enabling Static Website Hosting, each short code maps to an object key with website-redirect metadata. Requests to the website endpoint become redirects. This minimizes compute on the read path: no Lambda cold starts when many users only click short links.

![AWS sample architecture: S3 redirect](/images/3-BlogsTranslated/3.1-Blog1/aws-sample-architecture.png)

##### 3.2. Creating short links via API Gateway + Lambda

The admin UI is static. Creation logic lives in Lambda behind API Gateway. Lambda generates a short random key, writes the S3 object, and returns a URL reachable via the website/CloudFront.

##### 3.3. CloudFront and infrastructure packaging

CloudFront can unify the entry point and support custom domains. CloudFormation packages S3, Lambda, API Gateway, and helper custom resources.

##### 3.4. What “private” means here

“Private” leans toward **self-hosted / self-controlled** rather than strictly VPC-private. Public website endpoint and bucket policy implications still matter.

#### 4. Reflection

Useful because it matches the shortener problem while showing a different architectural trade-off than my workshop.

| Item | AWS Compute Blog | My workshop |
| --- | --- | --- |
| Mapping store | S3 object + redirect metadata | DynamoDB `url-shortener-links` |
| Redirect | S3 website redirect | Lambda **HTTP 302** |
| Ingress API | API Gateway | **Lambda Function URL** |
| Clicks / stats | Not the focus | Atomic `clickCount` + `/stats/{code}` |
| Frontend | Admin HTML on S3 | Shortener UI on S3 + `config.js` |

![Deployed workshop architecture: S3 + Function URL + DynamoDB + CloudWatch/SNS](/images/3-BlogsTranslated/3.1-Blog1/my-workshop-architecture.png)

S3 redirects are lean for “shorten + redirect only.” When you need clicks, stats, conditional 404s, and centralized handler logging, Function URL + DynamoDB is more flexible. In the workshop I verified **302** with PowerShell and stored mappings in DynamoDB:

![Verified 302 redirect in the workshop](/images/3-BlogsTranslated/3.1-Blog1/redirect-302.png)

Takeaway: multiple valid serverless shortener designs exist; choice depends on extensibility needs.
