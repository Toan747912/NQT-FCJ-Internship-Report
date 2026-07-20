---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Period:** 18/05/2026 – 20/05/2026

### Goals for Week 5:

* Get hands-on with cloud storage options: S3, RDS, DynamoDB, ElastiCache.
* Learn to pick the appropriate storage service based on use case, cost, and performance needs.

### Planned work items:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Lab 1: Host a static site on S3 — upload the HTML/CSS/JS files, turn on hosting, and apply a public-read Bucket Policy. Lab 2: Stand up RDS MySQL inside a Private Subnet with Multi-AZ enabled; connect from EC2 and perform CRUD operations. | 18/05/2026 | 18/05/2026 | <https://000057.awsstudygroup.com/><br><https://000005.awsstudygroup.com/> |
| Tue | Lab 3: Set up a DynamoDB table (Partition/Sort Key); exercise PutItem, GetItem, Query, and Scan; compare results against a GSI. | 19/05/2026 | 19/05/2026 | <https://000060.awsstudygroup.com/><br><https://000039.awsstudygroup.com/> |
| Wed | Lab 4: Stand up ElastiCache Redis to cache RDS query results (latency drops from ~50ms to ~2ms). Recap the trade-offs among S3 / RDS / DynamoDB / ElastiCache; double-check the RDS ← EC2 Security Group rules. | 20/05/2026 | 20/05/2026 | <https://000061.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |

### What was accomplished in Week 5:

* Got a static website live on S3.
* Stood up a Multi-AZ RDS instance and practiced DynamoDB queries with a GSI.
* Cut query latency by roughly 25x by introducing ElastiCache Redis.

### Challenges & Solutions:

* EC2 couldn't reach RDS since the RDS Security Group was blocking inbound traffic from the EC2 SG → corrected the inbound rules.

### Plan for the Following Week:

* Study serverless architecture using AWS Lambda and API Gateway.
