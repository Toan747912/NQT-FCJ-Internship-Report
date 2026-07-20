---
title: "Chuẩn bị"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.2. "
---

#### Mục tiêu

Chuẩn bị trước các tài nguyên nền (bảng dữ liệu + quyền IAM) để Lambda chỉ việc gắn role và chạy code, tránh sửa policy lung tung giữa chừng.

#### Tài nguyên cố định đã dùng

| Thành phần | Giá trị thực tế |
|---|---|
| Region | `ap-southeast-1` (Singapore) |
| DynamoDB table | `url-shortener-links` |
| Partition key | `shortCode` (String) |
| Capacity mode | On-demand |
| TTL attribute | `expiresAt` (bật Time to Live) |
| Lambda function | `url-shortener-backend` |
| IAM Role | `url-shortener-lambda-role` |
| Inline policy | `url-shortener-dynamodb-policy` |
| S3 bucket | `url-shortener-frontend-forward` |

#### DynamoDB table

Mình tạo bảng `url-shortener-links` với:

- **Partition key:** `shortCode` (S) — đủ để tra cứu theo mã ngắn.
- **Không dùng sort key** — mỗi `shortCode` là một item độc lập.
- **On-demand** — phù hợp traffic lab thất thường, không phải ước lượng RCU/WCU trước.

Sau khi tạo xong, bảng ở trạng thái **Active** (region `ap-southeast-1`).

![Bảng url-shortener-links đã tạo thành công](/images/5-Workshop/5.2-Chuan-bi/create-table.png)

Các thuộc tính khác (`originalUrl`, `clickCount`, `createdAt`, `expiresAt`) được ghi khi Put/Update item; DynamoDB không bắt buộc khai báo trước như schema quan hệ.

#### Time to Live (TTL)

Mình bật **Time to Live** trên bảng với attribute **`expiresAt`** để item hết hạn có thể bị DynamoDB xóa tự động theo epoch time — hữu ích nếu muốn short link tự hết hạn sau lab / demo, tránh bảng phình vô hạn.

![Đã bật TTL với attribute expiresAt](/images/5-Workshop/5.2-Chuan-bi/ttl-settings.png)

#### IAM Role cho Lambda

Mình tạo role **`url-shortener-lambda-role`** với trusted entity **AWS Lambda**, dùng làm execution role cho function backend.

![Role url-shortener-lambda-role đã tạo](/images/5-Workshop/5.2-Chuan-bi/iam-role-created.png)

Role được gắn tối thiểu hai lớp quyền:

1. `AWSLambdaBasicExecutionRole` (AWS managed) — ghi log ra CloudWatch Logs.
2. `url-shortener-dynamodb-policy` (customer inline) — chỉ các action cần thiết trên đúng ARN bảng `url-shortener-links`.

![Permissions của url-shortener-lambda-role](/images/5-Workshop/5.2-Chuan-bi/iam-role.png)

Nội dung policy DynamoDB mình dùng (thay `<ACCOUNT_ID>` bằng account thật):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowDynamoDBAccessToShortenerTable",
      "Effect": "Allow",
      "Action": [
        "dynamodb:PutItem",
        "dynamodb:GetItem",
        "dynamodb:UpdateItem"
      ],
      "Resource": "arn:aws:dynamodb:ap-southeast-1:<ACCOUNT_ID>:table/url-shortener-links"
    }
  ]
}
```

**Ý nghĩa least privilege:** không cấp `Scan`/`DeleteItem`/`*` toàn region — đủ cho create + redirect (Update) + đọc stats. Nếu thiếu `UpdateItem`, redirect vẫn có thể fail khi tăng `clickCount`.

#### Ghi chú trước khi sang Backend

- Region của bảng DynamoDB, Lambda và biến môi trường `TABLE_NAME` phải khớp (`url-shortener-links`).
- Tên bucket S3 phải **global unique**; mình chọn hậu tố `forward` → `url-shortener-frontend-forward`.
