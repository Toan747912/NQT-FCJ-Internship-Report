---
title: "Hạng mục phát sinh chi phí"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.6.1 </b> "
---

| Hạng mục | Ghi chú |
| --- | --- |
| CloudFront | Request + data transfer ra; HTTPS certificate qua ACM thường không tính phí công khai |
| S3 | Lưu trữ nhỏ + GET; public website request |
| Lambda | Request + duration (thường rất thấp ở lab) |
| DynamoDB on-demand | Trả theo RRU/WRU thực tế |
| CloudWatch Logs / Alarms | Ingestion + lưu trữ log; metric alarm |
| SNS | Email notification (free tier có hạn mức) |
| WAF (nếu bật) | Phí rule / request — cân nhắc chỉ bật khi cần |

Ước tính chi tiết nên đối chiếu [AWS Pricing Calculator](https://calculator.aws/) theo region `ap-southeast-1` trước khi mở rộng lâu dài.
