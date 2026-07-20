---
title: "Cấu hình Bucket Policy cho phép đọc công khai"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.4.2. "
---

#### Vì sao cần Bucket Policy

Static Website Hosting chỉ “bật công tắc phục vụ website”. Để trình duyệt tải được `index.html` / `config.js` / ảnh nền qua website endpoint, object vẫn phải **được phép đọc công khai**. Mình gắn policy chỉ với action `s3:GetObject` trên prefix object của bucket — không cấp `ListBucket` hay quyền ghi công khai.

#### Policy đã áp dụng

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

Thao tác: S3 → bucket → **Permissions** → tắt **Block all public access** (Off) → **Bucket policy** → Edit → Save. Sau khi lưu, console báo *Successfully edited bucket policy*.

![Bucket policy PublicReadGetObject trên url-shortener-frontend-forward](/images/5-Workshop/5.4-Frontend/bucket-policy.png)

#### Ý nghĩa bảo mật trong phạm vi lab

- Người dùng Internet chỉ **đọc** object đã upload; không được list toàn bucket hay upload/xóa qua policy này.
- Nội dung nhạy cảm không nên để trên bucket public kiểu này. Function URL và dữ liệu mapping nằm ở Lambda/DynamoDB, không nằm trong HTML tĩnh ngoài `config.js` (chỉ chứa endpoint API).
