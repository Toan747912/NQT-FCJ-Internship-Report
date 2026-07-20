---
title: "Proposed solution architecture"
date: 2026-07-14
weight: 3
chapter: false
pre: " <b> 2.3. </b> "
---

This section describes the target architecture after expansion, while keeping the S3 + Lambda + DynamoDB core already built in the workshop.

#### Current architecture (baseline)

![Current Serverless URL Shortener architecture](/images/2-Proposal/current-architecture.png)

Baseline already in place: S3 Static Website → Lambda Function URL → DynamoDB, IAM least privilege, CloudWatch + SNS error alerts. Child sections propose HTTPS edge (CloudFront/WAF) and tighter security without replacing this core.

#### Contents

- [Target architecture direction](2.3.1-Target-Architecture/)
- [Deployment flow after expansion](2.3.2-Deployment-Flow/)
- [Components to add](2.3.3-Components-to-Add/)
