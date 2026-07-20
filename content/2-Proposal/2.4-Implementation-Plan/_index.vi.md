---
title: "Kế hoạch triển khai"
date: 2026-07-14
weight: 4
chapter: false
pre: " <b> 2.4. </b> "
---

#### Giai đoạn ưu tiên

| Giai đoạn | Việc chính | Kết quả kiểm chứng |
| --- | --- | --- |
| P0 | CloudFront + ACM cho frontend S3 | Mở được site bằng HTTPS |
| P1 | OAC + thu hẹp public bucket; siết CORS | Không còn phụ thuộc public GetObject rộng nếu có thể |
| P2 | Auth API / WAF rate limit | Giảm Abuse tạo short link |
| P3 | Collision check + TTL DynamoDB | Short code chắc hơn; data demo tự hết hạn |
| P4 | Dashboard + alarm đa chỉ số + Budgets | Quan sát và cảnh báo chi phí |
| P5 | IaC (SAM/CDK) + pipeline tối thiểu | Deploy tái lập được |

#### Nguyên tắc triển khai

- Không phá vỡ demo đang chạy: triển khai song song / gradual cutover.
- Mỗi giai đoạn có checklist kiểm thử (HTTPS, create link, redirect, stats, alarm).
- Ưu tiên thay đổi cấu hình biên trước khi viết lại handler lớn.
- Giữ Free Tier / chi phí thấp: tắt CloudFront distribution demo khi không dùng; lifecycle log.
