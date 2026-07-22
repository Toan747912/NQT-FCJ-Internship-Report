---
title: "Tự động hóa bôi sáng phụ đề video đồng bộ với giọng đọc bằng Amazon Transcribe"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

#### 1. Thông tin nguồn

| Hạng mục | Nội dung |
| --- | --- |
| Tiêu đề gốc | Tự động hóa tính năng bôi sáng phụ đề video đồng bộ với giọng đọc bằng Amazon Transcribe |
| Tác giả / Nguồn | Toàn Ngô — [AWS Study Group VN](https://www.facebook.com/share/p/191PW65UTV/) (bài chia sẻ trên Facebook) |
| Chủ đề | Amazon Transcribe, S3, Lambda, Step Functions, pipeline media serverless, EdTech, bôi sáng phụ đề kiểu karaoke |
| AWS Blog liên quan | [Serverless video subtitles](https://aws.amazon.com/blogs/compute/implementing-serverless-video-subtitles/), [Video subtitles with translation (ML)](https://aws.amazon.com/blogs/machine-learning/create-video-subtitles-with-translation-using-machine-learning/) |

#### 2. Tóm tắt nội dung

Bài viết chia sẻ một use-case thực tế cho nền tảng học trực tuyến (EdTech) hoặc streaming: **bôi sáng phụ đề theo từng từ**, chạy chữ đồng bộ với giọng đọc — trải nghiệm giống karaoke — mà không phải căn chỉnh thời gian thủ công hay phụ thuộc file `.srt` cứng nhắc.

Giải pháp đề xuất là **pipeline serverless**: upload video lên **Amazon S3** → kích hoạt **Lambda** (hoặc điều phối bằng **Step Functions**) → tạo job **Amazon Transcribe** → frontend dùng JSON chi tiết để highlight đúng từ đang được nói theo thời gian phát video.

![Bài viết Facebook của AWS Study Group VN về bôi sáng phụ đề bằng Amazon Transcribe](/images/3-BlogsTranslated/3.2-Blog2/facebook-post.png)

#### 3. Nội dung chính

##### 3.1. Vấn đề: đồng bộ thủ công tốn công

Trước đây, để transcript khớp với tiếng nói thường phải căn thời gian bằng tay hoặc chỉnh file `.srt`. Với nhiều video bài giảng, cách làm này không mở rộng được.

##### 3.2. Luồng serverless với Amazon Transcribe

1. Người dùng upload video bài giảng lên **Amazon S3**.
2. Sự kiện S3 gọi **AWS Lambda** (hoặc khởi chạy **AWS Step Functions**) để tạo job xử lý trên **Amazon Transcribe**.
3. Điểm mấu chốt: Transcribe không chỉ trả text thuần, mà xuất **JSON** chi tiết — mỗi từ có `start_time`, `end_time` (độ chính xác tới mili-giây) và **confidence score**.
4. JSON được lưu S3 hoặc đẩy vào database để frontend gọi ra.

##### 3.3. Xử lý trên frontend (kiểu karaoke)

Khi video player chạy, chỉ cần theo dõi **current time** của video, so sánh với `start_time` / `end_time` của từng từ trong JSON, rồi đổi màu / bôi sáng đúng từ giảng viên đang nói.

##### 3.4. Chi phí và tối ưu

Transcribe tính phí theo **số phút âm thanh** được xử lý. Để tối ưu chi phí và thời gian, nên dùng Lambda (hoặc **Amazon Elastic Transcoder**) tách audio (MP3) từ video trước, rồi mới đưa file audio nhẹ hơn cho Transcribe — thay vì bắt hệ thống xử lý nguyên file video nặng.

Sơ đồ liên quan trên AWS Machine Learning Blog còn cho thấy cùng một transcript có thể nối tiếp **AWS Translate**, **Amazon Polly** (audio đã dịch), Python tạo file phụ đề, rồi **MoviePy** ghép thành media cuối — hữu ích khi nền tảng cần phụ đề đa ngôn ngữ hoặc lồng tiếng ngoài tính năng highlight.

![Pipeline phụ đề / dịch thuật serverless: Transcribe → Translate → Polly + Python subtitles → MoviePy](/images/3-BlogsTranslated/3.2-Blog2/transcribe-subtitle-architecture.png)

#### 4. Nhận xét

Bài viết khớp với tư duy workshop của mình: **xử lý serverless theo sự kiện** (S3 → Lambda / Step Functions) và lưu kết quả có cấu trúc để client mỏng tiêu thụ — cùng tinh thần với URL Shortener (S3 + Lambda Function URL + DynamoDB), nhưng áp dụng cho media/AI thay vì redirect link.

| Hạng mục | Bôi sáng phụ đề với Transcribe | Workshop của mình |
| --- | --- | --- |
| Trigger | Sự kiện upload S3 | Request HTTPS tới Function URL |
| Phần xử lý nặng | Job Amazon Transcribe (bất đồng bộ) | Lambda handler (request/response đồng bộ) |
| Lưu kết quả | JSON transcript trên S3 / DB | Mapping trên DynamoDB |
| Vai trò client | Highlight từ theo `currentTime` và timestamp | UI rút gọn / redirect / stats |

Điều mình học được: khi sản phẩm cần đồng bộ chính xác với lời nói, **timestamp từng từ của Amazon Transcribe** gần như thay thế việc căn phụ đề thủ công. Kết hợp pipeline upload serverless giúp vận hành nhẹ — và tách audio trước khi gọi Transcribe là mẹo tối ưu chi phí rõ ràng nếu sau này mình làm tính năng video bài giảng.
