---
title: "Lambda Function URLs"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Announcing AWS Lambda Function URLs: Built-in HTTPS Endpoints for Single-Function Microservices |
| Nguồn | [AWS News Blog](https://aws.amazon.com/blogs/aws/announcing-aws-lambda-function-urls-built-in-https-endpoints-for-single-function-microservices/) |
| Chủ đề | Lambda Function URL, HTTPS endpoint, CORS, IAM Auth / NONE, so sánh API Gateway |
| Liên hệ workshop | Mục 5.3 — backend `url-shortener-backend` qua Function URL |

#### 2. Tóm tắt nội dung

AWS công bố **Lambda Function URLs**: thêm endpoint HTTPS sẵn có cho một hàm Lambda, tuỳ chọn cấu hình CORS, **không bắt buộc** gắn API Gateway hay Application Load Balancer. Endpoint gắn với alias hoặc `$LATEST`, tạo được từ console, SDK, CloudFormation, SAM hoặc CDK.

Mặc định bảo vệ bằng **AWS IAM**. Có thể chọn Auth type **`NONE`** để tạo endpoint công khai (cần cập nhật resource-based policy phù hợp). Không phát sinh phí riêng ngoài chi phí invoke Lambda thông thường. Tính năng nhắm tới use case microservice **một hàm** cần HTTP công khai nhưng không cần đầy đủ tính năng nền tảng của API Gateway.

#### 3. Nội dung chính

##### 3.1. Vì sao có Function URL

Trước đây, muốn gọi Lambda bằng HTTPS thường phải dựng thêm API Gateway hoặc ALB. Với webhook đơn giản, form handler, hay prototype nhanh, phần “lớp API trung gian” trở thành độ phức tạp lớn hơn nghiệp vụ. Function URL rút gọn đường đi: Lambda tự có endpoint HTTPS ổn định.

##### 3.2. Khi nào nên dùng Function URL

Theo bài viết, phù hợp khi:

- Một function phục vụ một endpoint microservice.
- Không cần validation nâng cao, usage plan, API key, custom authorizer, custom domain phức tạp, caching API Gateway…
- Cần gọi nhanh trong R&D / lab / webhook nội bộ.

##### 3.3. Khi nào nên chọn API Gateway

Khi ứng dụng cần quản trị API ở mức nền tảng: nhiều route có policy khác nhau, throttle chi tiết, authorizer tùy biến, stage/deploy kiểm soát, tích hợp WAF/usage plan theo mô hình API Gateway. Function URL không thay thế mọi kịch bản.

##### 3.4. CORS và truy cập công khai

Function URL hỗ trợ cấu hình CORS native — quan trọng khi frontend nằm trên origin khác (ví dụ S3 website endpoint) gọi API. Auth `NONE` phù hợp API public có chủ đích; production cần cân nhắc auth, rate limit hoặc đặt CloudFront phía trước.

#### 4. Nhận xét

Đây là bài giải thích **đúng cơ chế** mình chọn cho backend URL Shortener. Function `url-shortener-backend` expose Function URL, Auth `NONE`, CORS cho phép frontend S3 gọi `POST /` tạo short link và `GET /{shortCode}` redirect.

![Lambda Function URL trong workshop](/images/3-BlogsTranslated/3.2-Blog2/function-url.png)

So với bài Compute Blog (shortener dùng API Gateway), Function URL giúp lab **giảm số tài nguyên** mà vẫn có HTTPS. Trade-off đã chấp nhận trong báo cáo: chưa custom domain, chưa throttling nâng cao — đủ cho phạm vi thực tập; nếu sản phẩm thật, có thể nâng lên CloudFront / API Gateway đúng như khuyến nghị phân tách use case trong bài này.
