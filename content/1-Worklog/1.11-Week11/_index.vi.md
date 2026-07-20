---
title: "Worklog Tuần 11"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Thời gian:** 29/06/2026 – 05/07/2026

### Mục tiêu tuần 11:

* Thực hành các dịch vụ AI/ML trên AWS gồm SageMaker, Rekognition, Comprehend và Bedrock.
* Nắm rõ sự khác biệt giữa AI Services có thể dùng ngay và ML Platform dùng để tự huấn luyện model.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | So sánh AI Services (Rekognition, Comprehend) với ML Platform (SageMaker); nắm tổng quan về Generative AI và Bedrock. | 29/06/2026 | 29/06/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| 3 | Lab 1: Khởi động một SageMaker Notebook Instance rồi huấn luyện model Image Classification. | 30/06/2026 | 01/07/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| 4 | Triển khai SageMaker Endpoint và gọi API inference, đạt độ chính xác khoảng 91% trên tập test. | 02/07/2026 | 02/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | Luyện tập tích hợp AI vào ứng dụng thông qua API; khám phá các Foundation Models trên Amazon Bedrock. | 03/07/2026 | 03/07/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| 6 | Viết hàm Lambda tự động gỡ SageMaker Endpoint sau khi test xong nhằm tránh phát sinh chi phí; tổng kết tuần. | 04/07/2026 | 04/07/2026 | <https://000022.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |

### Kết quả đạt được tuần 11:

* Nắm được điểm khác nhau giữa AI Services và ML Platform (SageMaker).
* Huấn luyện và triển khai thành công model phân loại ảnh trên SageMaker với độ chính xác khoảng 91%.
* Biết cách sử dụng Bedrock Foundation Models thông qua một API thống nhất.

### Khó khăn và cách giải quyết:

* Việc triển khai Endpoint mất khoảng 7 phút và nếu để chạy sẽ phát sinh chi phí → giải quyết bằng cách viết hàm Lambda tự động xóa endpoint ngay sau khi test xong.

### Kế hoạch tuần tiếp theo:

* Tổng kết toàn bộ chương trình, hoàn tất project cuối khóa và chuẩn bị nội dung báo cáo thực tập.
