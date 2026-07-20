---
title: "Configure Bucket Policy for public read"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.4.2. "
---

#### Why a Bucket Policy is required

Static Website Hosting only turns on website serving. For the browser to load `index.html` / `config.js` / the background image via the website endpoint, objects still need **public read**. I attached a policy with only `s3:GetObject` on the bucket’s object ARN — no public `ListBucket` or write.

#### Policy applied

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::url-shortener-frontend-forward/*"
    }
  ]
}
```

Path: S3 → bucket → **Permissions** → turn **Block all public access** Off → **Bucket policy** → Edit → Save. Console then shows *Successfully edited bucket policy*.

![Bucket policy PublicReadGetObject on url-shortener-frontend-forward](/images/5-Workshop/5.4-Frontend/bucket-policy.png)

#### Security meaning in this lab

- Internet clients can **read** uploaded objects only; they cannot list the whole bucket or upload/delete via this policy.
- Sensitive data should not live on a public bucket like this. Mapping data stays in Lambda/DynamoDB; static HTML only exposes the API endpoint via `config.js`.
