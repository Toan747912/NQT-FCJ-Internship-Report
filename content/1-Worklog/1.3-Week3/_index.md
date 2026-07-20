---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

**Period:** 04/05/2026 – 06/05/2026

### Week 3 Objectives:

* Design and roll out a network setup using Amazon VPC.
* Set up public/private subnets along with IGW, NAT Gateway, Security Groups and NACLs.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Learn VPC architecture (CIDR, Subnet, Route Table, IGW). Lab 1: Deploy a 10.0.0.0/16 VPC, set up Public & Private Subnets, and configure the Internet Gateway. | 04/05/2026 | 04/05/2026 | <https://000003.awsstudygroup.com/> |
| Tue | Set up a NAT Gateway for the private subnets; weigh Security Groups (stateful) against NACLs (stateless). | 05/05/2026 | 05/05/2026 | <https://000003.awsstudygroup.com/> |
| Wed | Lab 2: Networking Workshop — a multi-tier layout (web tier public, DB tier private); troubleshoot Route Tables / NAT; confirm the private subnet can reach the internet through the NAT Gateway. | 06/05/2026 | 06/05/2026 | <https://000092.awsstudygroup.com/><br><https://000003.awsstudygroup.com/> |

### Week 3 Achievements:

* Got a VPC up and running with public/private subnets, an IGW and a NAT Gateway.
* Made sense of how traffic flows through Route Tables.
* Learned what sets Security Groups apart from Network ACLs.

### Challenges & Solutions:

* The NAT Gateway wasn't working because the private subnet was missing a route → traced the issue by reviewing Route Tables against the lab documentation.

### Next Week Plan:

* Move on to Amazon EC2 — launching instances and setting up Auto Scaling.
