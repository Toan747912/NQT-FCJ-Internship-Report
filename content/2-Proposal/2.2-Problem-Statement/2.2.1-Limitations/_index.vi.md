---
title: "Hạn chế còn tồn tại"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 2.2.1 </b> "
---

| Nhóm | Hạn chế hiện tại | Ảnh hưởng |
| --- | --- | --- |
| Frontend / biên | S3 website endpoint mặc định **HTTP**, chưa CloudFront / custom domain | Thiếu TLS; trình duyệt cảnh báo “Not secure”; khó gắn domain thật |
| API | Function URL Auth **`NONE`**, CORS `*` | Bất kỳ ai cũng gọi được API tạo link nếu biết URL |
| Lưu trữ frontend | Bucket public `GetObject` | Object tĩnh lộ công khai; khó siết theo least privilege production |
| Dữ liệu | Short code ngẫu nhiên ngắn; chưa TTL / lifecycle item | Nguy cơ collision khi scale; dữ liệu demo tồn lâu không cần thiết |
| Observability | Chủ yếu filter `[ERROR]` + 1 alarm | Thiếu nhìn latency, tỷ lệ 4xx/5xx, dashboard vận hành |
| Triển khai | Cấu hình nhiều bước trên console | Khó tái dựng, dễ lệch môi trường, khó review thay đổi |
| Chi phí | Chưa Budgets / lifecycle log bắt buộc | Log group và tài nguyên demo có thể phát sinh phí âm thầm |

Các hạn chế trên **không phủ nhận** giá trị lab đã hoàn thành; chúng xác định đúng khoảng trống cần đề xuất để tiến gần production.
