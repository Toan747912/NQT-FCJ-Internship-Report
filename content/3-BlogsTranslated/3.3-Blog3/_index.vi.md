---
title: "S3 Static Website"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Tutorial: Configuring a static website on Amazon S3 |
| Nguồn | [Amazon S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html) |
| Chủ đề | Static Website Hosting, Block Public Access, Bucket Policy, website endpoint |
| Liên hệ workshop | Mục 5.4 — frontend `url-shortener-frontend-forward` |

#### 2. Tóm tắt nội dung

Tài liệu chính thức hướng dẫn biến bucket S3 thành website tĩnh phục vụ HTML/JS/CSS/ảnh. Quy trình gồm: tạo bucket, bật **Static website hosting** và chỉ định index document (`index.html`), chỉnh **Block Public Access**, gắn **Bucket Policy** cho phép `s3:GetObject` công khai, upload nội dung, rồi kiểm thử bằng **website endpoint**.

AWS nhấn mạnh: website endpoint mặc định là **HTTP** (không HTTPS). Nếu giữ đầy đủ Block Public Access và vẫn muốn website an toàn hơn, docs khuyến nghị dùng **CloudFront** với Origin Access Control (OAC) thay vì mở public bucket thuần.

#### 3. Nội dung chính

##### 3.1. Bật Static website hosting

Trong tab Properties, bật hosting kiểu bucket website, đặt Index document khớp chính xác tên file upload (phân biệt hoa thường). Sau khi Save, console hiển thị **Bucket website endpoint** dùng để mở site.

![Static website hosting đã bật trên bucket workshop](/images/3-BlogsTranslated/3.3-Blog3/s3-website.png)

##### 3.2. Block Public Access và Bucket Policy

Chỉ bật hosting chưa đủ. Object phải được phép đọc công khai (hoặc được CloudFront đọc hộ). Policy tối thiểu cho lab thường là `Principal: "*"`, `Action: s3:GetObject`, `Resource: arn:aws:s3:::bucket-name/*` — **không** cần cấp list/write công khai.

##### 3.3. Upload nội dung và test endpoint

Upload `index.html` (và các asset). Mở website endpoint — nếu thiếu policy / còn block public, trình duyệt nhận 403. Cần phân biệt website endpoint với REST API endpoint của S3: hành vi redirect/website chỉ áp dụng đúng website endpoint.

![Objects frontend đã upload](/images/3-BlogsTranslated/3.3-Blog3/s3-objects.png)

##### 3.4. Hạn chế và hướng production

HTTP-only, thiếu CDN và TLS — chấp nhận được cho lab. Production nên CloudFront + ACM + (tuỳ chọn) custom domain.

#### 4. Nhận xét

Docs này gần như là checklist mình đã làm trong workshop: bucket `url-shortener-frontend-forward`, enable hosting, policy `GetObject`, upload `index.html`/`config.js`/ảnh nền, test e2e trên website endpoint Singapore. Điểm học thêm quan trọng để viết báo cáo: hiểu vì sao lab còn HTTP, và ghi rõ hướng cải thiện CloudFront — tránh hiểu nhầm S3 website endpoint đã “production-ready HTTPS”.
