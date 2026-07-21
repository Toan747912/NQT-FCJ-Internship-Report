---
title: "Đồng bộ tiến độ video realtime với AWS AppSync"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Xây dựng tính năng đồng bộ tiến độ video (Progress Syncing) realtime với AWS AppSync |
| Tác giả / Nguồn | AWS Study Group VN — bài chia sẻ của nhóm thực tập (tiếp nối Blog 2) |
| Chủ đề | AWS AppSync, GraphQL, DynamoDB Direct Resolver, WebSocket subscription, đồng bộ realtime, EdTech |
| AWS Docs liên quan | [AppSync real-time data](https://docs.aws.amazon.com/appsync/latest/devguide/real-time-data.html), [DynamoDB resolvers tutorial](https://docs.aws.amazon.com/appsync/latest/devguide/tutorial-dynamodb-resolvers.html) |

#### 2. Tóm tắt nội dung

Tiếp nối bài Transcribe về phụ đề, nhóm chia sẻ kiến trúc thứ hai cho EdTech/Video: **đồng bộ tiến độ xem video tức thời giữa các thiết bị** — đang xem dở trên laptop, mở điện thoại là tiếp tục đúng giây đó.

Thay vì REST API gọi liên tục để lưu và lấy trạng thái (độ trễ và tài nguyên khó tối ưu khi scale), nhóm dùng **AWS AppSync (GraphQL)** kết hợp **Amazon DynamoDB**, tận dụng **WebSockets** để đẩy cập nhật realtime.

![Đồng bộ tiến độ realtime với AWS AppSync và Amazon DynamoDB](/images/3-BlogsTranslated/3.3-Blog3/appsync-progress-sync.png)

#### 3. Nội dung chính

##### 3.1. Vấn đề: REST polling khó scale tốt

Lưu tiến độ bằng REST mỗi vài giây rồi gọi lại trên thiết bị khác có thể chạy được ở mức demo, nhưng khi traffic tăng thì độ trễ và tải backend tăng theo. Tự vận hành cụm WebSocket để push cập nhật còn thêm độ phức tạp vận hành.

##### 3.2. Lưu tiến độ bằng GraphQL Mutation + Direct Resolver

Trong lúc xem, frontend định kỳ (ví dụ mỗi 5 giây) gửi timestamp tiến độ hiện tại lên AppSync qua **GraphQL Mutation**.

AppSync dùng **Direct Resolver** ghi thẳng vào bảng **DynamoDB** — nhanh và tiết kiệm vì bỏ bước trung gian **Lambda** trên đường ghi đơn giản này.

##### 3.3. Đồng bộ tức thời bằng GraphQL Subscriptions

Khi cùng tài khoản mở trên thiết bị khác, client đó kết nối bằng **GraphQL Subscription**. Mỗi khi DynamoDB có bản ghi tiến độ mới (qua AppSync), thiết bị mới nhận data realtime qua **WebSocket** và **seek** video đúng thời điểm.

##### 3.4. Ưu điểm vận hành

Không cần tự quản lý hạ tầng WebSocket phức tạp. AppSync duy trì kết nối realtime và scale lớp đồng bộ, giảm tải cho backend khi nhiều thiết bị cùng theo dõi một tài khoản.

#### 4. Nhận xét

Pattern này bổ sung tốt cho Blog 2 (timestamp từng từ từ Transcribe để highlight kiểu karaoke): Blog 2 cải thiện **trải nghiệm trong player**, Blog 3 cải thiện **liên tục giữa nhiều thiết bị**. Hai bài cùng phác một nền tảng video bài giảng trên dịch vụ managed của AWS.

So với URL Shortener trong workshop, ý tưởng chung vẫn là **dữ liệu managed + client mỏng**, nhưng AppSync thêm kênh **push** mà Function URL + DynamoDB không có sẵn.

| Hạng mục | Progress Sync (AppSync + DynamoDB) | Workshop của mình |
| --- | --- | --- |
| Kiểu API | GraphQL (Mutation + Subscription) | HTTPS Function URL (kiểu REST) |
| Lưu trữ | DynamoDB qua Direct Resolver | DynamoDB từ Lambda |
| Mô hình đồng bộ | Push qua WebSocket | Client phải gọi lại |
| Tầng trung gian | Thường không cần Lambda trên đường ghi | Lambda luôn nằm trên đường đi |

Điều mình học được: với bài toán “xem tiếp trên thiết bị khác,” **AppSync Subscriptions + DynamoDB** gọn hơn nhiều so với polling REST. Direct Resolver đáng nhớ mỗi khi thao tác ghi chỉ là cập nhật key/value đơn giản và Lambda chỉ đóng vai trò chuyển tiếp.
