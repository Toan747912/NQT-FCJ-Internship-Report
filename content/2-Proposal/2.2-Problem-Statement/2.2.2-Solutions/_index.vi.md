---
title: "Đề xuất giải pháp phát triển"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.2.2 </b> "
---

1. **CloudFront + ACM** trước S3 (và tuỳ chọn trước Function URL) để có HTTPS, custom domain, cache asset tĩnh.
2. **Siết truy cập S3**: chuyển dần sang OAC với CloudFront; giảm phụ thuộc Bucket Policy public.
3. **Siết API**: cân nhắc Auth IAM / JWT / API key; WAF rate-based rule; thu hẹp CORS theo domain frontend thật.
4. **Củng cố short code**: kiểm tra tồn tại trước khi Put, tăng độ dài / alphabet, (tuỳ chọn) custom domain path đẹp hơn.
5. **DynamoDB nâng cao**: TTL cho link hết hạn; GSIs nếu cần tra cứu theo owner/ngày (khi có multi-user).
6. **Observability**: dashboard CloudWatch (latency, errors, throttle); alarm đa chỉ số; retention log có lifecycle.
7. **IaC + CI**: SAM/CDK/Terraform mô tả Lambda, DynamoDB, S3/CloudFront; pipeline deploy theo nhánh.
8. **Cost guardrails**: AWS Budgets, alarm chi phí, tắt/xoá tài nguyên demo sau đánh giá.

Các giải pháp có thể triển khai độc lập theo giai đoạn, không buộc “big bang” viết lại toàn bộ hệ thống.
