---
title: "Tạo S3 bucket & bật Static website hosting"
date: 2026-07-14
weight: 1
chapter: false
pre: " 5.4.1. "
---

#### Việc đã thực hiện

Mình tạo bucket **`url-shortener-frontend-forward`** tại **Asia Pacific (Singapore) `ap-southeast-1`**. Sau khi tạo, console báo *Successfully created bucket* và tab Objects còn trống (0 objects) — sẵn sàng upload frontend.

![Bucket url-shortener-frontend-forward đã tạo thành công](/images/5-Workshop/5.4-Frontend/create-bucket.png)

Tiếp theo mình bật **Static website hosting** (Bucket hosting) với document mặc định `index.html`. Website endpoint dùng để truy cập UI:

`http://url-shortener-frontend-forward.s3-website-ap-southeast-1.amazonaws.com`

#### Vì sao dùng S3 website endpoint

- Phù hợp frontend tĩnh (HTML/JS/CSS/ảnh), không cần web server.
- Endpoint website tách biệt với endpoint REST API của S3; đây là URL người dùng mở trên trình duyệt.
- Lưu ý: S3 website endpoint mặc định là **HTTP** (không HTTPS). Với lab/demo chấp nhận được; production thường đặt **CloudFront + ACM** phía trước để có HTTPS và custom domain.

#### Điểm cấu hình quan trọng

- Region bucket nên cùng khu vực với Lambda/DynamoDB để đơn giản vận hành (dù website hosting không bắt buộc cùng region với API).
- Sau khi Enable hosting, cần Bucket Policy public read (mục 5.4.2) và chỉnh Block Public Access — nếu không, mở endpoint sẽ bị Access Denied / 403.
