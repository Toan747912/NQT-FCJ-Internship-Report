---
title: "Tạo Lambda function & Function URL"
date: 2026-07-14
weight: 1
chapter: false
pre: " 5.3.1. "
---

#### Cấu hình function đã tạo

| Thuộc tính | Giá trị |
| ---------- | ------- |
| Name | `url-shortener-backend` |
| Runtime | Node.js 20.x |
| Handler file | `index.mjs` |
| Region | `ap-southeast-1` |
| Env | `TABLE_NAME=url-shortener-links` |
| Function URL Auth | `NONE` |
| CORS | Allow origin `*`, methods `GET, POST` (và preflight OPTIONS) |

Mình chọn Node.js 20 vì runtime Lambda đã có sẵn AWS SDK v3 (`@aws-sdk/client-dynamodb`, `@aws-sdk/lib-dynamodb`) — paste code trên console là chạy, không cần đóng gói `node_modules` cho lab này.

Function **`url-shortener-backend`** dùng file handler `index.mjs`. Trong code editor, mình triển khai client DynamoDB Document Client, hàm `generateShortCode()` (mã ~6 ký tự) và `isValidUrl()` (chỉ chấp nhận `http`/`https`), rồi **Deploy** để cập nhật function.

![Code Lambda url-shortener-backend (index.mjs)](/images/5-Workshop/5.3-Backend/create-lambda.png)

#### Logic cốt lõi trong handler

Phần lõi mình triển khai có thể tóm tắt như sau (đã rút gọn so với code đầy đủ trên console):

**1) Tạo short link — `POST /`**

- Parse body JSON, lấy `url` và kiểm tra bằng `isValidUrl`.
- Sinh `shortCode` ngẫu nhiên ~6 ký tự (a–zA–Z0–9) qua `generateShortCode`.
- `PutCommand` vào bảng `TABLE_NAME` với `shortCode`, `originalUrl`, `clickCount: 0`, `createdAt`.
- Trả JSON `{ shortCode, shortUrl, originalUrl }` trong đó `shortUrl = functionUrl + "/" + shortCode`.

**2) Redirect — `GET /{shortCode}`**

- Dùng `UpdateCommand` tăng `clickCount` atomic (`SET clickCount = if_not_exists(clickCount, :zero) + :one`).
- `ConditionExpression: attribute_exists(shortCode)` → nếu mã không tồn tại thì ConditionalCheckFailed → trả **404**.
- Thành công → trả status **302** với header `Location: originalUrl`.

**3) Stats — `GET /stats/{shortCode}`**

- Đọc item và trả `{ shortCode, originalUrl, clickCount, createdAt }` **không** tăng đếm.

**4) CORS**

- Mọi response JSON/redirect cần header `Access-Control-Allow-Origin: *` (và Allow-Headers/Methods phù hợp) vì frontend gọi từ origin S3 website khác domain Function URL.
- Request preflight `OPTIONS` phải trả 200/204 kèm CORS headers — nếu thiếu, trình duyệt chặn `POST` dù Lambda có chạy.

#### Function URL

Sau khi bật Function URL (Auth type **NONE**, Invoke mode **BUFFERED**), mình cấu hình CORS Allow origin `*`, Allow headers `content-type`, Allow methods `GET` / `POST`, rồi copy endpoint dạng:

`https://xxxx.lambda-url.ap-southeast-1.on.aws/`

![Function URL + CORS của url-shortener-backend](/images/5-Workshop/5.3-Backend/function-url.png)

Endpoint này được ghi vào `config.js` của frontend (mục 5.4). Auth `NONE` phù hợp API rút gọn link công khai trong lab; môi trường production nên cân nhắc auth, rate limit hoặc đặt CloudFront phía trước.

#### Điểm cần lưu ý khi cấu hình

- Sai `TABLE_NAME` hoặc sai region → Put/Update fail (thường thấy lỗi trong CloudWatch Logs).
- Role thiếu `dynamodb:UpdateItem` → tạo link có thể ổn nhưng redirect tăng click sẽ lỗi.
- CORS chỉ mở trên Function URL vẫn chưa đủ nếu handler không trả header CORS trên response thực tế.
