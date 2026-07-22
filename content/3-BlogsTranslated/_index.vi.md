---
title: "Các bài blogs đã dịch"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Phần này trình bày bản dịch và tóm tắt các bài viết kỹ thuật liên quan đến AWS, bao gồm cả bài viết chia sẻ từ cộng đồng. Mỗi mục nêu rõ nguồn gốc bài viết, nội dung chính, các điểm kỹ thuật đáng chú ý và phần nhận xét liên hệ với dự án workshop của mình. Mình sẽ cập nhật thêm các bài khác trong quá trình thực tập.

### [Blog 1 – Tự động tạo hệ thống ôn tập Spaced Repetition bằng Amazon Bedrock & Step Functions](3.1-Blog1/)

Tóm tắt bài viết từ cộng đồng AWS Study Group VN mô tả kiến trúc hướng sự kiện (dùng Amazon Bedrock để sinh câu hỏi GenAI + Wait state của AWS Step Functions để lên lịch) nhằm tự động tạo và gửi nội dung ôn tập theo phương pháp spaced repetition cho bài toán EdTech.

### [Blog 2 – Tự động hóa bôi sáng phụ đề video đồng bộ với giọng đọc bằng Amazon Transcribe](3.2-Blog2/)

Tóm tắt bài chia sẻ của AWS Study Group VN về pipeline phụ đề serverless (S3 → Lambda / Step Functions → Amazon Transcribe JSON theo từng từ) để bôi sáng phụ đề kiểu karaoke trên video player, kèm mẹo tách audio trước khi gọi Transcribe để tối ưu chi phí.

### [Blog 3 – Đồng bộ tiến độ video realtime với AWS AppSync](3.3-Blog3/)

Tóm tắt bài tiếp theo của AWS Study Group VN về đồng bộ tiến độ xem giữa nhiều thiết bị bằng AppSync GraphQL Mutation, DynamoDB Direct Resolver và Subscription qua WebSocket — không cần tự vận hành hạ tầng WebSocket.
