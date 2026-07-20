---
title: "Worklog Tuần 10"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Thời gian:** 22/06/2026 – 28/06/2026

### Mục tiêu tuần 10:

* Triển khai một data lake trên nền AWS gồm S3, Glue, Athena và QuickSight.
* Có thể truy vấn dữ liệu dung lượng lớn trên S3 mà không cần đến một database server thông thường.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Tìm hiểu kiến trúc data lake gồm: S3 để lưu trữ, Glue để ETL, Athena để truy vấn và QuickSight để làm BI. | 22/06/2026 | 22/06/2026 | <https://000070.awsstudygroup.com/><br><https://000035.awsstudygroup.com/> |
| 3 | Lab 1: Đưa một file CSV khoảng 100.000 dòng lên S3, sau đó tạo bảng Athena và chạy truy vấn SQL trực tiếp trên đó. | 23/06/2026 | 24/06/2026 | <https://000106.awsstudygroup.com/><br><https://000040.awsstudygroup.com/> |
| 4 | Luyện tập với AWS Glue Crawler / ETL; khắc phục lỗi liên quan API DynamicFrame bằng cách convert sang Spark DataFrame qua `toDF()`. | 25/06/2026 | 25/06/2026 | <https://000040.awsstudygroup.com/><br><https://000105.awsstudygroup.com/> |
| 5 | Giảm chi phí Athena nhờ định dạng Parquet kết hợp partition theo ngày, đồng thời dựng biểu đồ trực quan bằng QuickSight. | 26/06/2026 | 26/06/2026 | <https://000073.awsstudygroup.com/><br><https://000106.awsstudygroup.com/> |
| 6 | Đúc kết toàn bộ pipeline S3 → Glue → Athena → QuickSight cùng các best practice để tiết kiệm chi phí. | 27/06/2026 | 27/06/2026 | <https://000070.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 10:

* Truy vấn được dữ liệu lớn trên S3 bằng Athena mà không cần dựng DB server.
* Nắm được cách dùng Glue cho ETL và tối ưu chi phí Athena nhờ Parquet kết hợp partition.
* Dựng được các biểu đồ trực quan hóa dữ liệu bằng QuickSight.

### Khó khăn và cách giải quyết:

* Glue Job bị lỗi do dùng sai API DynamicFrame → khắc phục bằng cách tham khảo Glue Developer Guide rồi convert dữ liệu sang Spark DataFrame thông qua `toDF()`.

### Kế hoạch tuần tiếp theo:

* Tìm hiểu các dịch vụ AI/ML gồm SageMaker, Rekognition và Amazon Bedrock.
