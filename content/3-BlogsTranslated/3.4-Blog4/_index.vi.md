---
title: "DynamoDB counters"
date: 2026-07-14
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Implement resource counters with Amazon DynamoDB |
| Nguồn | [AWS Database Blog](https://aws.amazon.com/blogs/database/implement-resource-counters-with-amazon-dynamodb/) |
| Chủ đề | Atomic counter, UpdateItem, ConditionExpression, độ chính xác khi đồng thời, retry |
| Liên hệ workshop | Mục 5.3 — tăng `clickCount` khi redirect |

#### 2. Tóm tắt nội dung

Bài viết đi sâu bài toán **đếm tài nguyên** trên DynamoDB: vote, tồn kho, vé sự kiện… phải cập nhật đúng khi nhiều process chạy song song. Sai số undercount/overcount có thể dẫn tới overselling hoặc từ chối nhầm. Tác giả trình bày **bảy hướng tiếp cận**, đánh giá qua lăng kính độ chính xác, chi phí và độ phức tạp — đồng thời nhấn mạnh hành vi lỗi 500-series của hệ thống phân tán: client không luôn biết chắc update đã apply hay chưa trước khi retry.

#### 3. Nội dung chính

##### 3.1. Atomic counters

Cách đơn giản nhất: một `UpdateItem` với biểu thức `ADD` / tăng số. DynamoDB serialize thao tác trên cùng item nên ít race hơn kiểu Get-then-Put ở tầng ứng dụng. Chi phí thấp, code ngắn. Độ chính xác kém hơn một số pattern transaction khi kết hợp failure + retry — phù hợp khi chấp nhận xấp xỉ hoặc điều kiện đơn giản là đủ.

##### 3.2. ConditionExpression và ngưỡng

Có thể gắn condition để chặn update vượt ngưỡng (ví dụ không cho counter < 0). Nếu condition fail, DynamoDB báo lỗi có kiểm soát — ứng dụng quyết định trả 4xx thay vì ghi trạng thái sai.

##### 3.3. Các hướng nâng cao hơn atomic counter

Optimistic concurrency control, transaction + client request token, marker item, đếm bằng item collection / set… dành cho hệ thống cần idempotency và độ chính xác cao hơn (inventory bán hàng thật). Đi kèm chi phí và độ phức tạp vận hành lớn hơn.

##### 3.4. Ý nghĩa với retry SDK

SDK thường tự retry. Với counter không idempotent, retry sau lỗi mơ hồ có thể overcount. Bài viết buộc người thiết kế chọn: chấp nhận overcount khi retry, undercount khi không retry, hoặc chuyển sang pattern idempotent hơn.

#### 4. Nhận xét

Pattern atomic counter + condition khớp trực tiếp logic `clickCount` trong workshop:

- Redirect dùng `UpdateCommand` tăng atomic, tránh Get-then-Put.
- `ConditionExpression: attribute_exists(shortCode)` → mã không tồn tại thì ConditionalCheckFailed → 404, không tạo item “ma”.

![Bảng DynamoDB url-shortener-links](/images/3-BlogsTranslated/3.4-Blog4/dynamodb-table.png)

![Item sau khi test redirect / clickCount](/images/3-BlogsTranslated/3.4-Blog4/dynamodb-items.png)

Với lab URL shortener, atomic counter là đủ để minh họa số lượt click. Bài blog giúp biện luận lựa chọn đó và biết “đường đi tiếp theo” nếu sau này đếm phải tuyệt đối (transaction / idempotency token) thay vì chỉ demo.
