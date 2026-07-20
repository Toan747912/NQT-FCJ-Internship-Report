---
title: "Đánh giá rủi ro"
date: 2026-07-14
weight: 7
chapter: false
pre: " <b> 2.7. </b> "
---

| Rủi ro | Mức ảnh hưởng | Khả năng | Giảm thiểu |
| --- | --- | --- | --- |
| Abuse API Auth NONE | Cao | Trung bình | WAF rate limit, auth, monitoring |
| Lộ dữ liệu qua bucket public | Trung bình | Trung bình | OAC, bỏ public GetObject rộng |
| Collision short code | Trung bình | Thấp→TB khi scale | Existence check, tăng độ dài |
| Chi phí CloudFront/WAF tăng | Trung bình | Trung bình | Budgets, tắt khi không demo |
| Phức tạp IaC làm trễ báo cáo | Trung bình | Trung bình | Phạm vi IaC tối thiểu, ưu tiên biên HTTPS trước |
| Mất demo đang chạy khi cutover | Cao | Thấp | Deploy song song, rollback DNS/CloudFront |

**Kế hoạch dự phòng:** giữ stack lab hiện tại như fallback; đảo traffic bằng DNS/CloudFront behavior thay vì xoá tay tài nguyên đang hoạt động.
