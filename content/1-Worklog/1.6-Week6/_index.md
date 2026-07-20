---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Period:** 25/05/2026 – 31/05/2026

### Goals for Week 6:

* Develop serverless applications using Lambda, API Gateway, and Step Functions.
* Grasp event-driven design patterns along with the pay-per-invocation pricing model.

### Planned work items:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Lab 1: Write a Python-based Lambda function that removes EC2 snapshots older than 30 days, triggered by EventBridge each day at 2:00 AM. | 25/05/2026 | 25/05/2026 | <https://000022.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |
| Tue | Lab 2: Build a Book Store REST API combining API Gateway, Lambda, and DynamoDB (CRUD operations with appropriate JSON status codes). | 26/05/2026 | 27/05/2026 | <https://000078.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |
| Wed | Keep building out the Book Store backend; wire in S3 where needed; check API responses for correctness. | 28/05/2026 | 28/05/2026 | <https://000078.awsstudygroup.com/><br><https://000079.awsstudygroup.com/> |
| Thu | Lab 3: Model a workflow in Step Functions — ValidateOrder → ProcessPayment → UpdateInventory → SendNotification. | 29/05/2026 | 29/05/2026 | <https://000047.awsstudygroup.com/> |
| Fri | Exercise error handling and retry logic; adjust the Lambda timeout from 3s to 30s and work on shrinking cold-start time. | 30/05/2026 | 30/05/2026 | <https://000047.awsstudygroup.com/><br><https://000077.awsstudygroup.com/> |

### What was accomplished in Week 6:

* Came to understand event-driven architecture and why serverless is beneficial.
* Delivered a working Book Store REST API using API Gateway, Lambda, and DynamoDB.
* Modeled a multi-stage workflow in Step Functions, complete with error handling and retries.

### Challenges & Solutions:

* Lambda kept timing out under the default 3-second limit → raised the timeout to 30 seconds and streamlined the code to cut down cold-start time.

### Plan for the Following Week:

* Study Infrastructure as Code via CloudFormation and CDK, plus CI/CD pipelines.
