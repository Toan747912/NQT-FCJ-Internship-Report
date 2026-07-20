---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Period:** 01/06/2026 – 07/06/2026

### Goals for Week 7:

* Get hands-on with Infrastructure as Code using CloudFormation and CDK.
* Stand up a CI/CD pipeline and rely on Systems Manager Session Manager for secure host access.

### This week's planned work:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Lab 1: Author a CloudFormation YAML template that spins up a VPC, 2 Subnets, a Security Group, and an EC2 instance from a single CLI command. | 01/06/2026 | 01/06/2026 | <https://000037.awsstudygroup.com/><br><https://000102.awsstudygroup.com/> |
| Tue | Lab 2: Bootstrap a TypeScript CDK project pairing S3 with Lambda; execute `cdk bootstrap`, `cdk synth`, and `cdk deploy`. | 02/06/2026 | 02/06/2026 | <https://000038.awsstudygroup.com/><br><https://000076.awsstudygroup.com/> |
| Wed | Lab 3: Assemble a CodePipeline flow — Source (CodeCommit) → Build (CodeBuild) → Deploy (CloudFormation). | 03/06/2026 | 04/06/2026 | <https://000023.awsstudygroup.com/><br><https://000084.awsstudygroup.com/> |
| Thu | Lab 4: Reach an EC2 instance with no public IP and port 22 closed, using SSM Session Manager instead. | 05/06/2026 | 05/06/2026 | <https://000058.awsstudygroup.com/><br><https://000031.awsstudygroup.com/> |
| Fri | Recap why IaC matters (version control, reusability, automation); confirm the pipeline runs cleanly after each push. | 06/06/2026 | 06/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### What I accomplished in Week 7:

* Provisioned infrastructure through both CloudFormation and CDK.
* Assembled a complete CI/CD pipeline from end to end.
* Reached EC2 securely through Session Manager, with no SSH required.

### Challenges & Solutions:

* The initial CDK deployment failed since the account hadn't been bootstrapped yet → resolved by running `cdk bootstrap` and redeploying.

### Plan for the Following Week:

* Dive into Container Services — Docker, Amazon ECS, and Fargate.
