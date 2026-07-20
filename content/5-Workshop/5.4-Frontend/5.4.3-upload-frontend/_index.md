---
title: "Upload frontend & configure Function URL"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.4.3. "
---

#### Objects uploaded

On the **Objects** tab of `url-shortener-frontend-forward`, I uploaded 3 files (Upload succeeded, ~3.1 MB total):

| File | Type | Role |
| ---- | ---- | ------- |
| `index.html` | `text/html` | UI to paste long URLs, call the API, show `shortUrl` |
| `config.js` | `text/javascript` | Declares `LAMBDA_URL` / the real Lambda Function URL |
| `forest-anime-bg.png` | `image/png` | UI background image |

![Upload succeeded — index.html, config.js, forest-anime-bg.png](/images/5-Workshop/5.4-Frontend/upload-files.png)

#### Role of `config.js`

Instead of hard-coding the Function URL in HTML, I split config into `config.js` so I can change the Lambda endpoint without rewriting UI logic, and keep the config visible for the report on S3.

`config.js` points to the Function URL copied in section 5.3.1:

```javascript
window.APP_CONFIG = {
  LAMBDA_URL: "https://xxxx.lambda-url.ap-southeast-1.on.aws"
};
```

![config.js pointing to Lambda Function URL](/images/5-Workshop/5.4-Frontend/config-js.png)

(`index.html` uses `window.APP_CONFIG.LAMBDA_URL` for `fetch` `POST /`.)

#### Content-Type

Console Upload usually sets `text/html`, `application/javascript`, and `image/png` correctly. Wrong Content-Type via CLI can break JS execution — I used console Upload for the lab and did not hit that issue.
