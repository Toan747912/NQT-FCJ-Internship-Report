---
title: "Serverless URL Shortener"
date: 2026-07-14
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Build a Serverless, Private URL Shortener |
| Nguồn | [AWS Compute Blog](https://aws.amazon.com/blogs/compute/build-a-serverless-private-url-shortener/) |
| Chủ đề | URL shortener serverless, Lambda, API Gateway, S3 website redirect, CloudFront |
| Liên hệ workshop | Mục 5 — so sánh thiết kế AWS mẫu với kiến trúc Function URL + DynamoDB của mình |

#### 2. Tóm tắt nội dung

Bài viết xuất phát từ nhu cầu thực tế của Solutions Architect: thường xuyên gửi link tạm (pre-signed URL) dài và khó chia sẻ, nên tác giả muốn một URL shortener **private**, tự kiểm soát, mà không phải vận hành server. Giải pháp đề xuất dựa hoàn toàn dịch vụ managed: **S3**, **API Gateway**, **Lambda**, có thể bổ sung **CloudFront**, và đóng gói bằng **CloudFormation**.

Điểm then chốt kỹ thuật là khai thác khả năng **website redirect của S3**: mỗi short link là một object (thường rỗng hoặc rất nhỏ) mang metadata `WebsiteRedirectLocation` trỏ tới URL dài. Khi người dùng mở short URL trên website endpoint, S3 tự trả HTTP redirect mà **không cần Lambda chạy ở bước redirect**.

Phần tạo short link dùng trang HTML tĩnh trên S3 (admin UI). Người dùng bấm Shorten → POST tới API Gateway → Lambda validate → sinh mã ngắn ngẫu nhiên → PutObject kèm metadata redirect → trả short URL. CloudFormation trong bài tạo sẵn bucket, function, API và một số helper Lambda hỗ trợ triển khai.

#### 3. Nội dung chính

##### 3.1. S3 làm redirection engine

Sau khi bật Static Website Hosting, mỗi short code tương ứng một object key. Metadata website redirect gắn URL đích. Request tới website endpoint được S3 diễn giải thành redirect (301 theo hành vi website hosting). Cách này tối giản compute cho luồng đọc: không cold start Lambda khi hàng nghìn người chỉ click short link.

![Kiến trúc mẫu AWS: S3 redirect](/images/3-BlogsTranslated/3.1-Blog1/aws-sample-architecture.png)

##### 3.2. Tạo short link qua API Gateway + Lambda

Admin UI chỉ là frontend tĩnh. Logic tạo mã nằm ở Lambda (~vài chục dòng), được API Gateway bảo vệ và expose HTTP. Lambda chọn độ dài mã ngắn đủ (bài viết dùng khoảng 5–7 ký tự), ghi object lên S3 và trả URL mở được qua website/CloudFront.

##### 3.3. CloudFront và triển khai hạ tầng

CloudFront giúp gom entry point, có thể gắn custom domain và cải thiện phân phối toàn cầu. CloudFormation gom S3, Lambda, API Gateway và custom resources phụ trợ để dựng lại môi trường nhanh.

##### 3.4. Phạm vi “private” trong bài

“Private” ở đây nghiêng về **tự host / tự kiểm soát** shortener thay vì phụ thuộc dịch vụ rút gọn bên ngoài, hơn là VPC-private tuyệt đối. Người đọc cần nắm rõ bucket/website endpoint và policy công khai vẫn là phần quan trọng của mô hình S3 website.

#### 4. Nhận xét

Bài viết rất hữu ích vì đúng chủ đề URL shortener serverless, đồng thời cho thấy một trade-off kiến trúc khác hẳn workshop của mình.

| Hạng mục | AWS Compute Blog | Workshop của mình |
| --- | --- | --- |
| Lưu mapping | Object S3 + redirect metadata | DynamoDB `url-shortener-links` |
| Redirect | S3 website redirect | Lambda trả **HTTP 302** |
| API vào | API Gateway | **Lambda Function URL** |
| Đếm click / stats | Không phải trọng tâm | `clickCount` atomic + `/stats/{code}` |
| Frontend | Admin HTML trên S3 | UI rút gọn trên S3 + `config.js` |

![Kiến trúc workshop đã triển khai: S3 + Function URL + DynamoDB + CloudWatch/SNS](/images/3-BlogsTranslated/3.1-Blog1/my-workshop-architecture.png)

Mô hình S3 redirect của AWS **rẻ và gọn** khi chỉ cần rút gọn + chuyển hướng. Khi cần nghiệp vụ thêm (đếm click, stats, 404 có điều kiện, log lỗi tập trung trong handler), lớp API tập trung như Function URL + DynamoDB linh hoạt hơn. Trong workshop, mình xác nhận redirect bằng status **302** trên PowerShell và lưu mapping trên bảng DynamoDB:

![Xác nhận redirect 302 trong workshop](/images/3-BlogsTranslated/3.1-Blog1/redirect-302.png)

Kết luận học được: cùng bài toán serverless shortener có nhiều “đúng”, lựa chọn phụ thuộc yêu cầu mở rộng — đọc bài AWS giúp tránh nghĩ Function URL + DynamoDB là cách duy nhất, và ngược lại giúp biện luận vì sao lab thực tập chọn hướng đó.
