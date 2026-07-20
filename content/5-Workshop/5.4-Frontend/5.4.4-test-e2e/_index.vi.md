---
title: "Test end-to-end"
date: 2026-07-14
weight: 4
chapter: false
pre: " 5.4.4. "
---

#### Kịch bản đã chạy trên trình duyệt

1. Mở website endpoint:  
   `http://url-shortener-frontend-forward.s3-website-ap-southeast-1.amazonaws.com`
2. Dán một URL dài (ví dụ console AWS / `https://www.google.com`).
3. (Tuỳ chọn) nhập **mã tuỳ chỉnh** (ví dụ `awss`, 3–20 ký tự chữ/số/`-`/`_`) hoặc để trống để hệ thống tự sinh.
4. Bấm **Tạo link ngắn** → UI hiển thị `shortUrl` dạng Function URL + `shortCode`.
5. Mở `shortUrl` → trình duyệt chuyển về đúng link gốc.
6. Bấm **Xem số liệu** → UI hiện `clickCount`, thời điểm tạo và click gần nhất.

![Giao diện Rút gọn Link trên S3 website](/images/5-Workshop/5.4-Frontend/frontend-ui.png)

![Kết quả tạo link ngắn (mã tuỳ chỉnh awss)](/images/5-Workshop/5.4-Frontend/test-result.png)

![Xem số liệu — clickCount và thời gian](/images/5-Workshop/5.4-Frontend/test-e2e.png)

#### Kiểm tra CORS trên DevTools

Vì origin của S3 website **khác** origin của Lambda Function URL, trình duyệt bắt buộc preflight:

- Request `OPTIONS` (preflight) → 200
- Request `POST`/`fetch` tạo link → 200 + response JSON

Trên tab **Network** (tick **Preserve log**), mình thấy các request tới Function URL gồm preflight và fetch thành công — chứng tỏ CORS trên Function URL và header từ Lambda đã khớp.

![cors network](/images/5-Workshop/5.4-Frontend/cors-network.png)

#### Ý nghĩa bài test này

Đây là lần đầu toàn chuỗi **S3 → Lambda → DynamoDB → redirect → stats** chạy trên trình duyệt thật, không chỉ test curl backend. Nếu chỉ gọi API bằng curl mà không qua UI, sẽ bỏ sót lỗi CORS — lỗi rất hay gặp khi ghép static frontend với Function URL.
