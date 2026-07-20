---
title: "Create S3 bucket & enable Static website hosting"
date: 2026-07-14
weight: 1
chapter: false
pre: " 5.4.1. "
---

#### What I configured

I created bucket **`url-shortener-frontend-forward`** in **Asia Pacific (Singapore) `ap-southeast-1`**. After creation, the console shows *Successfully created bucket* and the Objects tab is empty (0 objects) — ready for frontend upload.

![url-shortener-frontend-forward bucket created successfully](/images/5-Workshop/5.4-Frontend/create-bucket.png)

Then I enabled **Static website hosting** (Bucket hosting) with default document `index.html`. Website endpoint used for the UI:

`http://url-shortener-frontend-forward.s3-website-ap-southeast-1.amazonaws.com`

#### Why the S3 website endpoint

- Fits a static frontend (HTML/JS/CSS/images) with no web server.
- Separate from the S3 REST API endpoint; this is the URL users open in a browser.
- Note: the default S3 website endpoint is **HTTP** (not HTTPS). Acceptable for the lab; production usually adds **CloudFront + ACM** for HTTPS and a custom domain.

#### Important configuration notes

- Keeping the bucket near Lambda/DynamoDB simplifies operations.
- After enabling hosting, a public-read Bucket Policy (5.4.2) and adjusted Block Public Access are required — otherwise the endpoint returns Access Denied / 403.
