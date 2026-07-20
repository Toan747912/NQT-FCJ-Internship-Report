---
title: "Upload frontend & cấu hình Function URL"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.4.3. "
---

#### Object đã upload

Trên tab **Objects** của bucket `url-shortener-frontend-forward`, mình upload 3 file (Upload succeeded, tổng ~3.1 MB):

| File | Type | Vai trò |
| ---- | ---- | ------- |
| `index.html` | `text/html` | UI nhập URL dài, gọi API, hiển thị `shortUrl` |
| `config.js` | `text/javascript` | Khai báo `LAMBDA_URL` / Function URL thật của Lambda |
| `forest-anime-bg.png` | `image/png` | Ảnh nền giao diện |

![Upload succeeded — index.html, config.js, forest-anime-bg.png](/images/5-Workshop/5.4-Frontend/upload-files.png)

#### Vai trò `config.js`

Thay vì hard-code Function URL trong HTML, mình tách cấu hình sang `config.js` để:

- Đổi endpoint Lambda mà không sửa logic UI nhiều.
- Dễ đối chiếu khi screenshot / báo cáo (file config rõ ràng trên S3).

Nội dung `config.js` trỏ về Function URL đã copy ở mục 5.3.1:

```javascript
window.APP_CONFIG = {
  LAMBDA_URL: "https://xxxx.lambda-url.ap-southeast-1.on.aws"
};
```

![config.js trỏ tới Lambda Function URL](/images/5-Workshop/5.4-Frontend/config-js.png)

(`index.html` dùng `window.APP_CONFIG.LAMBDA_URL` khi `fetch` `POST /`.)

#### Content-Type

Upload qua console thường nhận diện đúng `text/html`, `application/javascript`, `image/png`. Nếu tự upload bằng CLI mà sai Content-Type, trình duyệt có thể không chạy JS đúng — lúc lab mình dùng Upload trên console nên không gặp lỗi này.
