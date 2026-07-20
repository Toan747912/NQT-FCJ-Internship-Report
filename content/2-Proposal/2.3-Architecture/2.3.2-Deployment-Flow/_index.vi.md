---
title: "Luồng triển khai sau khi mở rộng"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.3.2 </b> "
---

1. Người dùng mở `https://short.example.com` (CloudFront).
2. Asset tĩnh (`index.html`, JS, ảnh) lấy từ S3 qua OAC.
3. Browser gọi API qua cùng domain hoặc domain API được WAF bảo vệ.
4. Lambda tạo / redirect / stats trên DynamoDB như hiện tại (có collision check / TTL).
5. Metric & log chảy vào CloudWatch; alarm / Budgets / SNS cảnh báo vận hành và chi phí.

Luồng nghiệp vụ cốt lõi (create → redirect → stats) **không đổi**; thay đổi chủ yếu ở biên, bảo mật và vận hành.
