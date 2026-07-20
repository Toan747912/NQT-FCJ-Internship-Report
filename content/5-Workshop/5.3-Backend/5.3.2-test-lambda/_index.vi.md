---
title: "Test API"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.3.2. "
---

#### Mục tiêu kiểm thử

Xác nhận backend hoạt động độc lập với frontend theo ba kịch bản: tạo link, redirect 302, xem stats — rồi đối chiếu dữ liệu trên DynamoDB.

#### 1) Tạo link ngắn (`POST /`)

```bash
curl -X POST https://<function-url>/ \
  -H "Content-Type: application/json" \
  -d '{"url":"https://www.google.com"}'
```

Response mẫu khi thành công:

```json
{
  "shortCode": "aZ3kT9",
  "shortUrl": "https://<function-url>/aZ3kT9",
  "originalUrl": "https://www.google.com"
}
```

Sau khi gắn frontend, thao tác tương đương trên UI cũng cho kết quả short URL cùng dạng Function URL + mã ngắn (có thể dùng mã tuỳ chỉnh, ví dụ `awss`):

![Kết quả tạo link ngắn trên giao diện](/images/5-Workshop/5.3-Backend/frontend-shorten-result.png)

#### 2) Redirect (`GET /{shortCode}`)

Mở short URL trên trình duyệt phải đưa về URL gốc. Để **nhìn thấy status 302** (không để client tự follow), mình dùng PowerShell:

```powershell
Invoke-WebRequest -Uri "https://<function-url>/<shortCode>" -MaximumRedirection 0
```

Kết quả quan sát được: `StatusCode = 302`, `StatusDescription = Found`. Đây là bằng chứng redirect đúng nghĩa HTTP, không chỉ “mở link rồi thấy trang đích”.

![Test redirect HTTP 302](/images/5-Workshop/5.3-Backend/test-redirect-302.png)

#### 3) Stats (`GET /stats/{shortCode}`)

```bash
curl https://<function-url>/stats/<shortCode>
```

```json
{
  "shortCode": "aZ3kT9",
  "originalUrl": "https://www.google.com",
  "clickCount": 1,
  "createdAt": "..."
}
```

Mỗi lần redirect thành công, `clickCount` tăng; gọi `/stats/...` chỉ đọc, không làm tăng thêm.

#### 4) Đối chiếu DynamoDB

Vào **Explore table items** của bảng `url-shortener-links`, mình thấy các item với `shortCode`, `originalUrl`, `clickCount`, `createdAt` — khớp với các mã đã tạo khi test (ví dụ short code trên UI / PowerShell).

![dynamodb items](/images/5-Workshop/5.3-Backend/dynamodb-items.png)

#### Kết luận kiểm thử backend

Backend đã đáp ứng đủ vòng đời của URL shortener: ghi mapping → redirect có đếm → đọc thống kê. Các lỗi hay gặp trong lúc test (CORS, 403 IAM, ConditionalCheckFailed khi mã sai) đều tra được qua CloudWatch Logs của function.
