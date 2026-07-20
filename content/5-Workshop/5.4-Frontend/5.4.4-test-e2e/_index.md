---
title: "End-to-end test"
date: 2026-07-14
weight: 4
chapter: false
pre: " 5.4.4. "
---

#### Browser scenario I ran

1. Open the website endpoint:  
   `http://url-shortener-frontend-forward.s3-website-ap-southeast-1.amazonaws.com`
2. Paste a long URL (AWS console / `https://www.google.com`).
3. (Optional) enter a **custom code** (e.g. `awss`, 3–20 letters/digits/`-`/`_`) or leave blank for auto-generation.
4. Click **Create short link** → UI shows a `shortUrl` as Function URL + `shortCode`.
5. Open `shortUrl` → browser redirects to the original URL.
6. Click **View stats** → UI shows `clickCount`, created time, and last click.

![Shorten Link UI on S3 website](/images/5-Workshop/5.4-Frontend/frontend-ui.png)

![Short link result (custom code awss)](/images/5-Workshop/5.4-Frontend/test-result.png)

![View stats — clickCount and timestamps](/images/5-Workshop/5.4-Frontend/test-e2e.png)

#### CORS check in DevTools

Because the S3 website origin **differs** from the Lambda Function URL origin, the browser requires preflight:

- `OPTIONS` (preflight) → 200
- `POST`/`fetch` create → 200 + JSON body

In the **Network** tab (**Preserve log**), Function URL traffic showed successful preflight and fetch — CORS on Function URL and Lambda response headers matched.

![cors network](/images/5-Workshop/5.4-Frontend/cors-network.png)

#### Why this test matters

This is the first full **S3 → Lambda → DynamoDB → redirect → stats** path on a real browser, not only curl against the backend. Skipping the UI would miss CORS failures — a common issue when pairing a static frontend with Function URL.
