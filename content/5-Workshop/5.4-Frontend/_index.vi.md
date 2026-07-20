---
title: "Triển khai Frontend"
date: 2026-07-14
weight: 4
chapter: false
pre: " 5.4. "
---

#### Mục tiêu

Đưa giao diện rút gọn link lên S3 Static Website Hosting, nối `config.js` với Function URL thật, rồi kiểm thử toàn luồng trên trình duyệt (kèm CORS).

#### Việc đã làm

1. Tạo bucket `url-shortener-frontend-forward`, bật Static website hosting.
2. Gắn Bucket Policy public `GetObject` để website endpoint đọc được object.
3. Upload `index.html`, `config.js`, ảnh nền.
4. Test tạo link / redirect / quan sát Network.

Chi tiết:

- [Tạo S3 bucket & Static website hosting](5.4.1-tao-bucket/)
- [Bucket Policy public read](5.4.2-bucket-policy/)
- [Upload frontend & Function URL](5.4.3-upload-frontend/)
- [Test end-to-end](5.4.4-test-e2e/)
