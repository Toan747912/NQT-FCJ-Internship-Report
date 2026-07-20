---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**Period:** 15/06/2026 – 21/06/2026

### Goals for Week 9:

* Stand up and operate an Amazon EKS cluster.
* Get hands-on with core Kubernetes objects: Pods, Deployments, Services, ConfigMaps, and Helm.

### This week's planned work:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Cover Kubernetes architecture — Control Plane, Worker Nodes, etcd — then install `eksctl` and `kubectl`. | 15/06/2026 | 15/06/2026 | <https://000126.awsstudygroup.com/><br><https://000065.awsstudygroup.com/> |
| Tue | Lab 1: Spin up an EKS Cluster via `eksctl`, point kubectl at it, and confirm the node group is healthy (`kubectl get nodes`). | 16/06/2026 | 17/06/2026 | <https://000062.awsstudygroup.com/><br><https://000065.awsstudygroup.com/> |
| Wed | Work through Deployment / Service exercises (ClusterIP, NodePort, LoadBalancer) and track how a Pod's lifecycle unfolds. | 18/06/2026 | 18/06/2026 | <https://000126.awsstudygroup.com/> |
| Thu | Chase down a CrashLoopBackOff using `kubectl logs` and `kubectl describe`; verify the required environment variables are set. | 19/06/2026 | 19/06/2026 | <https://000126.awsstudygroup.com/><br><https://000062.awsstudygroup.com/> |
| Fri | Revisit Deployment self-healing and the reconciliation loop; put together an ECS-versus-EKS summary. | 20/06/2026 | 20/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### What I accomplished in Week 9:

* Stood up an EKS cluster and connected to it via kubectl.
* Came to understand Pod lifecycle, Deployment self-healing, and the different Service types.
* Tracked down a CrashLoopBackOff to a missing required environment variable and resolved it.

### Challenges & Solutions:

* Pods kept cycling through CrashLoopBackOff → dug in with `kubectl logs` / `describe` and traced it to a missing required env var.

### Plan for the Following Week:

* Move on to Data & Analytics — Athena, Glue, and QuickSight.
