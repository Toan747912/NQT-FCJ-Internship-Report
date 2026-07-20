---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

**Period:** 27/04/2026 – 29/04/2026

### Week 2 Objectives:

* Handle identity and access management through AWS IAM.
* Put Least Privilege, MFA, and IAM Roles for EC2 into practice.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Learn the IAM model (User, Group, Role, Policy), Least Privilege, MFA. Lab 1: Set up IAM Users and Groups (Dev, Ops), attach Managed Policies, and validate with the Policy Simulator. | 27/04/2026 | 27/04/2026 | <https://000002.awsstudygroup.com/> |
| Tue | Learn about IAM Permission Boundaries and how they restrict user permissions. | 28/04/2026 | 28/04/2026 | <https://000030.awsstudygroup.com/> |
| Wed | Lab 2: Build an IAM Role for EC2 (Instance Profile) that reaches S3 without needing Access Keys; attach the Role, confirm access works, and go over IAM Role & Condition concepts. | 29/04/2026 | 29/04/2026 | <https://000048.awsstudygroup.com/><br><https://000044.awsstudygroup.com/> |

### Week 2 Achievements:

* Came to understand User, Group, Role, Policy and the Least Privilege principle.
* Set up IAM Users/Groups and checked permissions worked correctly via Policy Simulator.
* Got an IAM Role configured so EC2 could reach S3 without relying on Access Keys.

### Challenges & Solutions:

* Kept running into JSON syntax mistakes when writing IAM Policies → turned to the Console's Policy Editor and AWS documentation for help.

### Next Week Plan:

* Get into Amazon VPC — building out a private virtual network on AWS.
