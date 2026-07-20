---
title: "Bản đề xuất"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

#### Bối cảnh và mục đích

Trong phạm vi thực tập, dự án **Serverless URL Shortener** đã hoàn thành giai đoạn xây dựng nền tảng: giao diện tĩnh trên **Amazon S3**, backend **AWS Lambda Function URL**, lưu trữ mapping trên **Amazon DynamoDB**, kèm giám sát lỗi cơ bản bằng **CloudWatch** (metric filter / alarm) và **SNS**.

Bản đề xuất này trình bày định hướng phát triển tiếp theo, nhằm nâng cấp dự án từ mô hình lab/demo serverless sang mô hình vận hành gần production hơn — vẫn kiểm soát được chi phí, phạm vi và độ phức tạp kỹ thuật — phù hợp tài khoản cá nhân và mục tiêu đánh giá của báo cáo thực tập.

#### Cấu trúc nội dung

| Mục | Nội dung chính |
| --- | --- |
| [2.1 Tóm tắt điều hành](2.1-Executive-Summary/) | Hiện trạng, nhóm đề xuất và thứ tự ưu tiên |
| [2.2 Tuyên bố vấn đề](2.2-Problem-Statement/) | Hạn chế, giải pháp và lợi ích kỳ vọng |
| [2.3 Kiến trúc giải pháp đề xuất](2.3-Architecture/) | Kiến trúc mục tiêu, luồng triển khai và thành phần bổ sung |
| [2.4 Kế hoạch triển khai](2.4-Implementation-Plan/) | Giai đoạn ưu tiên và nguyên tắc thực hiện |
| [2.5 Lộ trình phát triển](2.5-Roadmap/) | Khung thời gian và kết quả từng giai đoạn |
| [2.6 Ước tính ngân sách](2.6-Budget/) | Hạng mục chi phí, mức ngân sách và kiểm soát |
| [2.7 Đánh giá rủi ro](2.7-Risks/) | Rủi ro kỹ thuật / vận hành và biện pháp giảm thiểu |
| [2.8 Kết quả kỳ vọng](2.8-Expected-Outcomes/) | Tiêu chí đánh giá sau khi triển khai đề xuất |

#### Phạm vi áp dụng

Các đề xuất **không thay thế** kiến trúc S3 + Lambda Function URL + DynamoDB hiện có, mà bổ sung lớp năng lực về HTTPS biên, bảo mật truy cập, quan sát hệ thống, chất lượng short code, tự động hóa triển khai và quản trị chi phí. Mỗi hạng mục có thể làm theo giai đoạn, kèm bằng chứng kỹ thuật phục vụ đánh giá và báo cáo.
