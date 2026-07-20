---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Thời gian:** 01/06/2026 – 07/06/2026

### Mục tiêu của tuần 7:

* Rèn luyện Infrastructure as Code thông qua CloudFormation và CDK.
* Dựng CI/CD pipeline và dùng Systems Manager Session Manager để truy cập an toàn.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Lab 1: Soạn file CloudFormation YAML để triển khai VPC, 2 Subnet, Security Group và EC2 chỉ bằng một lệnh CLI duy nhất. | 01/06/2026 | 01/06/2026 | <https://000037.awsstudygroup.com/><br><https://000102.awsstudygroup.com/> |
| 3 | Lab 2: Dựng dự án CDK bằng TypeScript kết hợp S3 và Lambda; thực thi `cdk bootstrap`, `cdk synth`, `cdk deploy`. | 02/06/2026 | 02/06/2026 | <https://000038.awsstudygroup.com/><br><https://000076.awsstudygroup.com/> |
| 4 | Lab 3: Ghép nối quy trình CodePipeline — Source (CodeCommit) → Build (CodeBuild) → Deploy (CloudFormation). | 03/06/2026 | 04/06/2026 | <https://000023.awsstudygroup.com/><br><https://000084.awsstudygroup.com/> |
| 5 | Lab 4: Truy cập EC2 khi không có public IP và cổng 22 bị đóng, thay bằng SSM Session Manager. | 05/06/2026 | 05/06/2026 | <https://000058.awsstudygroup.com/><br><https://000031.awsstudygroup.com/> |
| 6 | Nhìn lại lợi ích của IaC (kiểm soát phiên bản, tái sử dụng, tự động hóa); xác nhận pipeline chạy đúng sau từng lần push. | 06/06/2026 | 06/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Những gì đạt được trong tuần 7:

* Triển khai hạ tầng thành công bằng cả CloudFormation lẫn CDK.
* Hoàn thiện một CI/CD pipeline khép kín từ đầu đến cuối.
* Truy cập EC2 an toàn thông qua Session Manager mà không cần SSH.

### Khó khăn và cách giải quyết:

* Lần deploy CDK đầu tiên thất bại vì tài khoản chưa được bootstrap → khắc phục bằng cách chạy `cdk bootstrap` rồi deploy lại.

### Dự kiến công việc tuần sau:

* Tìm hiểu Container Services — Docker, Amazon ECS và Fargate.
