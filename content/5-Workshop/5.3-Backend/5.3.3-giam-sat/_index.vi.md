---
title: "Giám sát CloudWatch + SNS"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.3.3. "
---

#### Mục tiêu

Sau khi create / redirect / stats chạy ổn, mình bổ sung vòng **quan sát → cảnh báo** quanh Lambda: bắt pattern lỗi trên log, dựng alarm và gửi email qua SNS. (Đếm click atomic `UpdateItem` đã nằm trong handler mục 5.3.1.)

#### 1) Metric filter trên CloudWatch Logs

Trên log group `/aws/lambda/url-shortener-backend`, mình tạo metric filter **`URLShortenerErrorFilter`** với pattern `"[ERROR]"` (metric `ErrorCount`, namespace `URLShortenerApp`).

![Metric filter URLShortenerErrorFilter](/images/5-Workshop/5.3-Backend/metric-filter.png)

#### 2) SNS topic + subscription email

Mình tạo topic **`url-shortener-alerts`**, rồi tạo subscription protocol **EMAIL** (xác nhận subscription trước khi nhận mail cảnh báo thật).

![SNS topic url-shortener-alerts](/images/5-Workshop/5.3-Backend/sns-topic.png)

![SNS email subscription (Pending confirmation)](/images/5-Workshop/5.3-Backend/sns-subscription.png)

#### 3) CloudWatch Alarms

Mình tạo các alarm gắn với stack URL Shortener, trong đó alarm chính theo dõi lỗi:

| Alarm | Điều kiện (tóm tắt) |
| --- | --- |
| `URLShortener-Errors` | `ErrorCount >= 1` trong cửa sổ ~5 phút |
| `URLShortener-Throttles` | `Throttles >= 1` / 5 phút |
| `URLShortener-Duration` | theo dõi thời gian chạy / ngưỡng liên quan |

![Danh sách CloudWatch alarms (URLShortener-Errors đã tạo)](/images/5-Workshop/5.3-Backend/alarm.png)

#### 4) Email khi alarm vào trạng thái ALARM

Khi metric lỗi vượt ngưỡng, CloudWatch đổi state (ví dụ `INSUFFICIENT_DATA` → `ALARM`) và SNS gửi mail AWS Notifications.

![Email cảnh báo từ SNS khi alarm ALARM](/images/5-Workshop/5.3-Backend/alarm-email.png)

#### Giải thích trạng thái Insufficient data

Trên console alarm thường thấy **Insufficient data** khi chưa có datapoint (chưa có log khớp `"[ERROR]"` trong cửa sổ đánh giá). Điều này **không có nghĩa alarm hỏng** — chỉ là hệ thống chưa nhận tín hiệu lỗi. Khi Lambda log `[ERROR]` đủ điều kiện, metric tăng và alarm có thể chuyển **In alarm** rồi gửi SNS.

#### Liên hệ kiến trúc

Trên sơ đồ mục 5.1, đây là nhánh Step 6–7: CloudWatch (Logs / Metrics / Metric filter / Alarms) → SNS Topic → Email admin.
