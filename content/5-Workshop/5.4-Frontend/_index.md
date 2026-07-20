---
title: "Deploy Frontend"
date: 2026-07-14
weight: 4
chapter: false
pre: " 5.4. "
---

#### Goal

Host the shortener UI on S3 Static Website Hosting, point `config.js` at the real Function URL, then verify the full browser flow (including CORS).

#### What I did

1. Created bucket `url-shortener-frontend-forward` and enabled Static website hosting.
2. Applied a public-read Bucket Policy (`GetObject` only).
3. Uploaded `index.html`, `config.js`, and the background image.
4. Tested create / redirect / Network tab behavior.

Details:

- [Create S3 bucket & Static website hosting](5.4.1-tao-bucket/)
- [Public-read Bucket Policy](5.4.2-bucket-policy/)
- [Upload frontend & Function URL](5.4.3-upload-frontend/)
- [End-to-end test](5.4.4-test-e2e/)
