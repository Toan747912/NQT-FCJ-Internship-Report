---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Thời gian:** 08/06/2026 – 10/06/2026

### Mục tiêu của tuần 8:

* Đóng gói ứng dụng thành container bằng Docker rồi triển khai trên Amazon ECS / Fargate.
* Nắm được điểm khác nhau giữa EC2 launch type và Fargate.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Lab 1: Soạn Dockerfile cho ứng dụng Node.js, build image ngay trên máy, sau đó đẩy lên Amazon ECR. | 08/06/2026 | 08/06/2026 | <https://000015.awsstudygroup.com/> |
| 3 | Lab 2: Dựng ECS Cluster, Task Definition trỏ tới image trên ECR, và ECS Service chạy 2 task phía sau ALB; thiết lập giới hạn tài nguyên, biến môi trường; sửa IAM Role để pull ECR hoạt động. | 09/06/2026 | 09/06/2026 | <https://000016.awsstudygroup.com/><br><https://000017.awsstudygroup.com/> |
| 4 | Lab 3: Chuyển workload sang launch type Fargate — không phải quản lý EC2, tính phí theo vCPU/memory; đối chiếu Fargate với EC2 launch type và xác nhận độ ổn định. | 10/06/2026 | 10/06/2026 | <https://000067.awsstudygroup.com/><br><https://000016.awsstudygroup.com/> |

### Những gì đạt được trong tuần 8:

* Đi hết luồng triển khai: Dockerfile → build → ECR → ECS.
* Dựng thành công ECS Service có ALB đứng trước, chạy 2 task.
* Đưa ứng dụng chạy trên Fargate mà không cần quản lý server nào.

### Khó khăn và cách giải quyết:

* ECS Service không khởi động được vì Task Execution Role thiếu quyền pull ECR → khắc phục bằng cách gắn policy `AmazonEC2ContainerRegistryReadOnly`.

### Dự kiến công việc tuần sau:

* Chuyển sang Amazon EKS — triển khai và vận hành Kubernetes cluster trên AWS.
