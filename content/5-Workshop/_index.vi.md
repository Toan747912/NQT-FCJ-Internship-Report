---
title: "Workshop"
date: 2026-07-14
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

#### Tổng quan

Mục 5 ghi lại quá trình mình triển khai ứng dụng **rút gọn đường link (URL Shortener)** theo mô hình **serverless** trên AWS. Mục tiêu không chỉ “chạy được demo”, mà còn nắm rõ cách các dịch vụ ghép với nhau: frontend tĩnh, API xử lý nghiệp vụ, và CSDL key-value có độ trễ thấp.

Kiến trúc chọn **Amazon S3** (Static Website Hosting) + **AWS Lambda Function URL** + **Amazon DynamoDB**, triển khai tại region **ap-southeast-1 (Singapore)**. Không dựng EC2, không dùng API Gateway — Lambda Function URL đóng vai trò endpoint HTTPS công khai cho API. Giám sát lỗi dùng **CloudWatch + SNS**.

![Kiến trúc Serverless URL Shortener](/images/5-Workshop/5.1-Tong-quan/architecture.png)

#### Demo project

**Video demo:** [URL Shortener Serverless — quy trình end-to-end](https://drive.google.com/file/d/1az6EVbShi64-Lg72U0uZnOoewGKCVeXn/view?usp=drive_link)

#### Bài toán và cách tiếp cận

Ứng dụng cần ba thao tác chính:

1. Nhận URL dài → sinh `shortCode` → lưu mapping và trả `shortUrl`.
2. Khi người dùng mở `shortUrl` → tra cứu `originalUrl` → **HTTP 302** về link gốc, đồng thời tăng `clickCount`.
3. Cho phép xem thống kê (`/stats/{shortCode}`) mà không làm tăng số click.

Với phạm vi lab này, Function URL + DynamoDB on-demand là đủ: triển khai nhanh, chi phí thấp theo request, và vẫn thể hiện được mô hình serverless end-to-end.

#### Phạm vi đã triển khai

| Lớp | Tài nguyên | Vai trò |
| --- | ---------- | ------- |
| Frontend | S3 bucket `url-shortener-frontend-forward` | Phục vụ UI (`index.html`, `config.js`) |
| Backend | Lambda `url-shortener-backend` + Function URL | Tạo mã, redirect, stats |
| Data | DynamoDB `url-shortener-links` (+ TTL `expiresAt`) | Lưu `shortCode` ↔ `originalUrl`, `clickCount` |
| IAM | Role + policy DynamoDB | Least privilege cho Lambda |
| Monitoring | CloudWatch Metric filter + Alarm + SNS | Cảnh báo khi log có `[ERROR]` |

#### Cấu trúc mục 5

1. [Tổng quan kiến trúc](5.1-Tong-quan/) — luồng request và lý do chọn dịch vụ.
2. [Chuẩn bị](5.2-Chuan-bi/) — bảng DynamoDB, IAM Role/policy thực tế đã tạo.
3. [Triển khai Backend](5.3-Backend/) — Lambda, Function URL, test API, giám sát CloudWatch/SNS.
4. [Triển khai Frontend](5.4-Frontend/) — S3 hosting, Bucket Policy, upload và e2e.
5. [Dọn dẹp](5.5-Don-dep/) — thu hồi tài nguyên sau demo.
