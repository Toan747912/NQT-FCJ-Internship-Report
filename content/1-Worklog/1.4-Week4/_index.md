---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Period:** 11/05/2026 – 17/05/2026

### Goals for Week 4:

* Provision and operate Amazon EC2 instances.
* Set up Auto Scaling alongside CloudWatch monitoring.

### Planned work items:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Lab 1: Spin up an EC2 instance (Amazon Linux 2), set up Apache, open ports 80/443, and reach it via its Public IP. | 11/05/2026 | 11/05/2026 | <https://000004.awsstudygroup.com/> |
| Tue | Review AMIs, Key Pairs, and Elastic IPs; lock down the SSH Security Group to a single personal IP address. | 12/05/2026 | 12/05/2026 | <https://000004.awsstudygroup.com/> |
| Wed | Lab 2: Set up a Launch Template plus an Auto Scaling Group (min=1, max=3) driven by CPU usage. | 13/05/2026 | 13/05/2026 | <https://000006.awsstudygroup.com/> |
| Thu | Lab 3: Assemble a CloudWatch Dashboard (CPU, Network, StatusCheck) and trigger an Alarm + SNS notification once CPU exceeds 70%. | 14/05/2026 | 14/05/2026 | <https://000036.awsstudygroup.com/><br><https://000008.awsstudygroup.com/> |
| Fri | Confirm Auto Scaling behaves correctly under load; revisit the full EC2 lifecycle (launch/stop/start/terminate). | 15/05/2026 | 15/05/2026 | <https://000006.awsstudygroup.com/><br><https://000004.awsstudygroup.com/> |

### What was accomplished in Week 4:

* Gained a solid grasp of the EC2 lifecycle and got a web server running in the cloud.
* Got CPU-driven Auto Scaling working end to end.
* Put proactive monitoring in place using CloudWatch together with SNS.

### Challenges & Solutions:

* SSH access failed since port 22 wasn't open → resolved by allowing inbound SSH only from my own IP (avoiding 0.0.0.0/0).

### Plan for the Following Week:

* Explore storage-related services: Amazon S3, RDS, and DynamoDB.
