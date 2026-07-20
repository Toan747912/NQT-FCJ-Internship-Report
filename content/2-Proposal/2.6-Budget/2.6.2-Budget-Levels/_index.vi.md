---
title: "Ngân sách theo mức mở rộng"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2.6.2 </b> "
---

| Mức | Phạm vi | Kỳ vọng chi phí / tháng (lab) |
| --- | --- | --- |
| M0 – Hiện tại | S3 + Lambda URL + DynamoDB + Alarm cơ bản | ~$0–2 (thường Free Tier) |
| M1 – HTTPS edge | + CloudFront + ACM | ~$1–5 tuỳ traffic |
| M2 – Bảo mật biên | + WAF rule tối thiểu | Cộng thêm vài USD nếu có request |
| M3 – Quan sát + IaC | Dashboard, log retention vừa phải | Chủ yếu phụ thuộc log volume |

Các con số mang tính định hướng cho báo cáo; cần cập nhật bằng Pricing Calculator / Cost Explorer khi thực thi.
