---
title: "S3 Static Website"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Tutorial: Configuring a static website on Amazon S3 |
| Source | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html) |
| Topics | Static Website Hosting, Block Public Access, Bucket Policy, website endpoint |
| Workshop link | Section 5.4 — frontend `url-shortener-frontend-forward` |

#### 2. Summary

The official tutorial turns an S3 bucket into a static website serving HTML/JS/CSS/images: create the bucket, enable **Static website hosting** with an index document (`index.html`), adjust **Block Public Access**, attach a public **`s3:GetObject` Bucket Policy**, upload content, then test via the **website endpoint**.

AWS stresses the default endpoint is **HTTP** (not HTTPS). Keeping all Block Public Access settings on usually means serving through **CloudFront** with Origin Access Control instead of a fully public bucket.

#### 3. Main content

##### 3.1. Enable Static website hosting

In Properties, enable bucket website hosting and set Index document to match the uploaded filename exactly (case-sensitive). After Save, the console shows the **Bucket website endpoint**.

![Static website hosting enabled on the workshop bucket](/images/3-BlogsTranslated/3.3-Blog3/s3-website.png)

##### 3.2. Block Public Access and Bucket Policy

Hosting alone is not enough. Objects must be publicly readable (or readable by CloudFront). A minimal lab policy is `Principal: "*"`, `Action: s3:GetObject`, `Resource: arn:aws:s3:::bucket-name/*` — no public list/write.

##### 3.3. Upload content and test the endpoint

Upload `index.html` and assets. Open the website endpoint — missing policy / remaining public blocks yield 403. Distinguish the website endpoint from the S3 REST endpoint.

![Uploaded frontend objects](/images/3-BlogsTranslated/3.3-Blog3/s3-objects.png)

##### 3.4. Limits and production direction

HTTP-only without CDN/TLS is acceptable for a lab. Production should use CloudFront + ACM and optionally a custom domain.

#### 4. Reflection

This doc is essentially the checklist I followed in the workshop: bucket `url-shortener-frontend-forward`, enable hosting, `GetObject` policy, upload `index.html`/`config.js`/background, e2e test on the Singapore website endpoint. Extra reporting value: explain why the lab is still HTTP and document CloudFront as the hardening path.
