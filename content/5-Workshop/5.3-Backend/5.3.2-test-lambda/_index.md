---
title: "Test API"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.3.2. "
---

#### Test goals

Verify the backend works without the frontend for create, 302 redirect, and stats — then cross-check DynamoDB items.

#### 1) Create short link (`POST /`)

```bash
curl -X POST https://<function-url>/ \
  -H "Content-Type: application/json" \
  -d '{"url":"https://www.google.com"}'
```

Sample success response:

```json
{
  "shortCode": "aZ3kT9",
  "shortUrl": "https://<function-url>/aZ3kT9",
  "originalUrl": "https://www.google.com"
}
```

After the frontend was wired, the UI produced the same Function URL + short-code shape (optional custom code, e.g. `awss`):

![Short link result in the UI](/images/5-Workshop/5.3-Backend/frontend-shorten-result.png)

#### 2) Redirect (`GET /{shortCode}`)

Opening the short URL in a browser should land on the original URL. To **observe HTTP 302** without auto-follow, I used PowerShell:

```powershell
Invoke-WebRequest -Uri "https://<function-url>/<shortCode>" -MaximumRedirection 0
```

Observed: `StatusCode = 302`, `StatusDescription = Found` — proof of a real redirect response.

![Test redirect HTTP 302](/images/5-Workshop/5.3-Backend/test-redirect-302.png)

#### 3) Stats (`GET /stats/{shortCode}`)

```bash
curl https://<function-url>/stats/<shortCode>
```

```json
{
  "shortCode": "aZ3kT9",
  "originalUrl": "https://www.google.com",
  "clickCount": 1,
  "createdAt": "..."
}
```

Successful redirects increase `clickCount`; `/stats/...` only reads.

#### 4) DynamoDB cross-check

In **Explore table items** for `url-shortener-links`, items showed `shortCode`, `originalUrl`, `clickCount`, `createdAt` matching the codes created during tests.

![dynamodb items](/images/5-Workshop/5.3-Backend/dynamodb-items.png)

#### Backend test conclusion

The backend covers the shortener lifecycle: write mapping → redirect with counting → read stats. Common failures during testing (CORS, IAM 403, ConditionalCheckFailed for bad codes) were diagnosable from the function’s CloudWatch Logs.
