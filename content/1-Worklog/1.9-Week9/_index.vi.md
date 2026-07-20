---
title: "Worklog Tuần 9"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Thời gian:** 15/06/2026 – 21/06/2026

### Mục tiêu của tuần 9:

* Dựng và vận hành một Amazon EKS cluster.
* Thực hành các đối tượng cốt lõi của Kubernetes: Pods, Deployments, Services, ConfigMaps, Helm.

### Công việc dự kiến trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Tìm hiểu kiến trúc Kubernetes gồm Control Plane, Worker Nodes, etcd; sau đó cài đặt `eksctl` và `kubectl`. | 15/06/2026 | 15/06/2026 | <https://000126.awsstudygroup.com/><br><https://000065.awsstudygroup.com/> |
| 3 | Lab 1: Dựng EKS Cluster bằng `eksctl`, trỏ kubectl vào cluster, xác nhận node group hoạt động tốt (`kubectl get nodes`). | 16/06/2026 | 17/06/2026 | <https://000062.awsstudygroup.com/><br><https://000065.awsstudygroup.com/> |
| 4 | Thực hành các bài tập Deployment / Service (ClusterIP, NodePort, LoadBalancer) và theo dõi vòng đời của một Pod. | 18/06/2026 | 18/06/2026 | <https://000126.awsstudygroup.com/> |
| 5 | Truy tìm lỗi CrashLoopBackOff bằng `kubectl logs` và `kubectl describe`; xác nhận các biến môi trường cần thiết đã được thiết lập. | 19/06/2026 | 19/06/2026 | <https://000126.awsstudygroup.com/><br><https://000062.awsstudygroup.com/> |
| 6 | Xem lại cơ chế self-healing của Deployment và reconciliation loop; tổng hợp bảng so sánh ECS với EKS. | 20/06/2026 | 20/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Những gì đạt được trong tuần 9:

* Dựng thành công EKS cluster và kết nối được qua kubectl.
* Nắm được vòng đời Pod, cơ chế self-healing của Deployment và các loại Service.
* Truy ra nguyên nhân CrashLoopBackOff là do thiếu biến môi trường bắt buộc và khắc phục được.

### Khó khăn và cách giải quyết:

* Các Pod liên tục rơi vào CrashLoopBackOff → đào sâu bằng `kubectl logs` / `describe` và xác định nguyên nhân là thiếu biến môi trường bắt buộc.

### Dự kiến công việc tuần sau:

* Chuyển sang tìm hiểu Data & Analytics — Athena, Glue và QuickSight.
