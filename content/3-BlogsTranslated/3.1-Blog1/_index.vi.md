---
title: "Tự động tạo hệ thống ôn tập Spaced Repetition bằng Amazon Bedrock & Step Functions"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Tự động tạo hệ thống ôn tập "Spaced Repetition" bằng Amazon Bedrock & Step Functions |
| Tác giả / Nguồn | Toàn Ngô — [AWS Study Group VN](https://www.facebook.com/share/p/1DiaeMY6Sv/) (bài chia sẻ trên Facebook) |
| Chủ đề | GenAI, Amazon Bedrock, AWS Step Functions, Wait state, kiến trúc event-driven, EdTech |

#### 2. Tóm tắt nội dung

Bài viết chia sẻ kiến trúc mà nhóm AWS Study Group VN xây dựng để giải quyết bài toán phổ biến trong EdTech: tự động tạo và lên lịch gửi nội dung ôn tập theo phương pháp **Spaced Repetition** (Lặp lại ngắt quãng — ôn lại bài học theo các mốc thời gian tăng dần, ví dụ 1 ngày, 3 ngày, 7 ngày sau khi học, để giúp người học nhớ lâu hơn).

Thay vì dùng cronjob truyền thống quét database liên tục để kiểm tra ai cần ôn bài, nhóm thiết kế một luồng **hướng sự kiện (event-driven)** kết hợp **Amazon Bedrock** để sinh nội dung và **AWS Step Functions** để điều phối, lên lịch.

![Bài viết Facebook của AWS Study Group VN mô tả kiến trúc Spaced Repetition](/images/3-BlogsTranslated/3.1-Blog1/facebook-post.png)

#### 3. Nội dung chính

##### 3.1. Sinh câu hỏi tự động bằng GenAI (Amazon Bedrock)

Khi học viên xem xong video bài học, hệ thống lấy phần transcript (văn bản) của bài giảng và đưa qua mô hình ngôn ngữ lớn trên **Amazon Bedrock**. Chỉ với một prompt chuẩn, Bedrock sẽ tự động "đẻ" ra 3–5 câu hỏi trắc nghiệm bám sát nội dung vừa học, giúp loại bỏ việc phải tự soạn câu hỏi thủ công cho từng bài học.

##### 3.2. Lên lịch gửi bài ôn tập bằng AWS Step Functions

Thay vì dùng cronjob quét database liên tục, toàn bộ luồng gửi bài ôn tập được đẩy vào một state machine của **Step Functions**. Điểm "ăn tiền" ở đây là tính năng **Wait state**: workflow sẽ "ngủ" (pause) đúng 1 ngày, sau đó gửi email/thông báo ôn tập lần 1, rồi lại "ngủ" tiếp 3 ngày, gửi tiếp lần 2… — mô hình hoá trực tiếp mốc thời gian ôn tập bằng các state của workflow, thay vì viết logic đếm thời gian trong code ứng dụng.

##### 3.3. Tối ưu chi phí

Wait state trong Step Functions **không tính phí cho thời gian chờ (compute time)** — chi phí chỉ phát sinh khi trạng thái (state) **thay đổi**, tức là khi có việc thực sự xảy ra. Cách này rẻ hơn đáng kể so với việc giữ một EC2 hay Lambda chạy/được gọi liên tục chỉ để kiểm tra "đã đến lúc chưa?" cho từng học viên.

![Luồng workflow Spaced Repetition: Bedrock sinh nội dung, Step Functions lên lịch ôn tập ở các mốc 1/3/7 ngày](/images/3-BlogsTranslated/3.1-Blog1/spaced-repetition-architecture.png)

##### 3.4. Ưu điểm: workflow trở thành một sơ đồ trực quan, dễ chỉnh sửa

Nhờ đưa logic lên lịch ôn tập vào Step Functions, toàn bộ quy trình phức tạp trở thành một **sơ đồ state machine trực quan** thay vì logic ẩn trong code ứng dụng. Nhóm có thể dễ dàng thay đổi kịch bản gửi bài (ví dụ thêm mốc 14 ngày) hoặc kênh thông báo mà không cần sửa logic nghiệp vụ cốt lõi — chỉ cần chỉnh định nghĩa state machine.

Bài viết cũng dẫn tài liệu AWS chuẩn được dùng làm cơ sở kỹ thuật:
- [Tích hợp Amazon Bedrock vào Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-bedrock.html)
- [Cách sử dụng Wait state trong Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-wait-state.html)

#### 4. Nhận xét

Mặc dù bài viết hướng tới bài toán EdTech khác với URL shortener trong workshop của mình, nhưng nguyên lý kiến trúc phía sau lại giống với nguyên tắc mình áp dụng ở Mục 5: **ưu tiên kiến trúc hướng sự kiện (event-driven), dùng dịch vụ managed thay cho vòng lặp polling** để giảm chi phí và giảm công vận hành.

| Hạng mục | Spaced Repetition (Bedrock + Step Functions) | Workshop của mình |
| --- | --- | --- |
| Mô hình trigger | State machine event-driven (Wait state) | Lambda Function URL event-driven |
| Cơ chế "chờ" | Wait state của Step Functions (không tính phí compute khi chờ) | Không cần — request/response xử lý đồng bộ |
| Sinh nội dung / logic | Amazon Bedrock (GenAI) | Logic rút gọn URL cố định trong Lambda |
| Giám sát | Sơ đồ state machine trực quan | CloudWatch Logs + metric filter + SNS alarm (Mục 5.3.3) |

Điều mình học được nhiều nhất là **pattern Wait state**: một cách gọn để triển khai "làm X, chờ N ngày, rồi làm Y" mà không cần dịch vụ lập lịch riêng hay cronjob phải liên tục kiểm tra timestamp. Nếu sau này mở rộng Serverless URL Shortener của mình — ví dụ gửi nhắc nhở khi short link sắp hết hạn, hoặc tự động lưu trữ (archive) các link không dùng sau 30 ngày — thì Step Functions Wait state sẽ là lựa chọn tiết kiệm chi phí hơn nhiều so với việc dùng EventBridge gọi Lambda định kỳ vài phút một lần. Đây cũng là gợi ý hay rằng việc kết hợp GenAI (Bedrock) với dịch vụ điều phối (Step Functions) đang trở thành một pattern phổ biến để xây dựng automation thông minh, ít phải bảo trì trên AWS.
