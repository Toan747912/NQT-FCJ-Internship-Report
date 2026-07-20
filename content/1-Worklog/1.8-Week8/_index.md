---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Period:** 08/06/2026 – 10/06/2026

### Goals for Week 8:

* Package applications into containers with Docker and roll them out on Amazon ECS / Fargate.
* Grasp how the EC2 launch type differs from Fargate.

### This week's planned work:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Lab 1: Draft a Dockerfile for a Node.js app, build the image on the local machine, then push it to Amazon ECR. | 08/06/2026 | 08/06/2026 | <https://000015.awsstudygroup.com/> |
| Tue | Lab 2: Stand up an ECS Cluster, a Task Definition pointing to the ECR image, and an ECS Service running 2 tasks behind an ALB; set resource limits and environment variables, and correct the IAM Role so ECR pulls work. | 09/06/2026 | 09/06/2026 | <https://000016.awsstudygroup.com/><br><https://000017.awsstudygroup.com/> |
| Wed | Lab 3: Move the workload to the Fargate launch type — no EC2 instances to manage, billed by vCPU/memory; weigh Fargate against the EC2 launch type and confirm stability. | 10/06/2026 | 10/06/2026 | <https://000067.awsstudygroup.com/><br><https://000016.awsstudygroup.com/> |

### What I accomplished in Week 8:

* Carried the app through the full pipeline: Dockerfile → build → ECR → ECS.
* Stood up an ECS Service fronted by an ALB, running 2 tasks.
* Got the app running on Fargate with no servers to manage.

### Challenges & Solutions:

* The ECS Service failed to start because the Task Execution Role was missing ECR pull rights → fixed by attaching the `AmazonEC2ContainerRegistryReadOnly` policy.

### Plan for the Following Week:

* Move on to Amazon EKS — provisioning and operating a Kubernetes cluster on AWS.
