---
title: "CloudWatch Lambda errors"
date: 2026-07-14
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | How to get notified on specific Lambda function error patterns using CloudWatch |
| Nguồn | [AWS Cloud Operations Blog](https://aws.amazon.com/blogs/mt/get-notified-specific-lambda-function-error-patterns-using-cloudwatch/) |
| Chủ đề | CloudWatch Logs filter / subscription, Lambda Errors metric, SNS notification |
| Liên hệ workshop | Mục 5.3.3 — metric filter `"[ERROR]"` + alarm + SNS |

#### 2. Tóm tắt nội dung

Bài viết chỉ ra hạn chế thực dụng của CloudWatch Alarm gắn metric **Errors** của Lambda: biết *có lỗi*, nhưng **không kèm nội dung log** cụ thể. Để nhận thông báo mang chi tiết hơn, AWS đề xuất kết hợp **CloudWatch Logs filter pattern** (ví dụ `ERROR`, `CRITICAL`, pattern tùy chỉnh) với subscription: khi dòng log khớp, kích hoạt Lambda xử lý lỗi → publish **SNS** → email/SMS. Cách này vừa cảnh báo vừa mang context để xử lý nhanh, đồng thời có thể làm blueprint cho phản ứng tự động khi phát hiện pattern nguy hiểm.

#### 3. Nội dung chính

##### 3.1. Metric Errors versus filter trên log

- **Errors metric**: tín hiệu tổng hợp theo phút, phù hợp “có/không có lỗi ở mức function”.
- **Log filter**: bắt đúng chuỗi trong CloudWatch Logs (ví dụ `"[ERROR]"` do code tự ghi). Phù hợp khi muốn lọc lỗi nghiệp vụ cụ thể, không chỉ exception runtime.

##### 3.2. Luồng kiến trúc trong bài

Nhiều Lambda nghiệp vụ ghi log → CloudWatch Logs → filter pattern khớp → Lambda “error processing” → SNS topic → subscriber (email). Đây là mẫu event-driven cho quan sát lỗi.

##### 3.3. Xây filter và kiểm thử

Chọn log group `/aws/lambda/<function-name>`, đặt filter pattern, gắn destination. Kiểm thử bằng cách cố tình sinh log khớp pattern và xác nhận SNS nhận được message. Filter quá rộng sẽ tốn invoke/chi phí; quá hẹp sẽ bỏ sót.

##### 3.4. Mở rộng

Có thể dùng mô hình này làm nền cho reactive automation (ticket, remediator) chứ không chỉ email.

#### 4. Nhận xét

Ở mục 5.3.3 mình triển khai biến thể cùng mục tiêu “log lỗi → cảnh báo”:

1. Metric filter trên `/aws/lambda/url-shortener-backend` với pattern `"[ERROR]"`.
2. Metric `URLShortenerErrorCount` + Alarm `url-shortener-error-alarm`.
3. SNS subscribe email.

![CloudWatch Alarm trong workshop](/images/3-BlogsTranslated/3.5-Blog5/cloudwatch-alarm.png)

Khác biệt so với bài: bài dùng subscription → Lambda trung gian để đính **nội dung log** vào SNS; mình dùng metric filter → alarm → SNS theo **số lần khớp**. Cùng vòng **quan sát → cảnh báo**. Trạng thái **Insufficient data** khi chưa có `[ERROR]` là bình thường — đọc bài AWS giúp giải thích đúng hiện tượng này trong báo cáo thay vì nghĩ alarm cấu hình sai.
