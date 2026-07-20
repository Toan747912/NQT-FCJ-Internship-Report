---
title: "Proposal"
date: 2026-07-14
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

#### Context and purpose

During the internship, the **Serverless URL Shortener** project completed its foundation phase: a static UI on **Amazon S3**, a backend on **AWS Lambda Function URL**, mapping storage in **Amazon DynamoDB**, plus basic error monitoring with **CloudWatch** (metric filter / alarm) and **SNS**.

This proposal outlines the next development direction: move from a lab/demo serverless model toward a more production-like operating model — while keeping cost, scope, and technical complexity under control for a personal account and the internship report evaluation goals.

#### Content structure

| Section | Focus |
| --- | --- |
| [2.1 Executive summary](2.1-Executive-Summary/) | Current state, proposal groups, and priorities |
| [2.2 Problem statement](2.2-Problem-Statement/) | Limits, proposed solutions, and expected benefits |
| [2.3 Proposed solution architecture](2.3-Architecture/) | Target architecture, deployment flow, and components to add |
| [2.4 Implementation plan](2.4-Implementation-Plan/) | Priority phases and delivery principles |
| [2.5 Development roadmap](2.5-Roadmap/) | Timeline and outcomes per phase |
| [2.6 Budget estimate](2.6-Budget/) | Cost items, budget levels, and cost control |
| [2.7 Risk assessment](2.7-Risks/) | Technical/ops risks and mitigations |
| [2.8 Expected outcomes](2.8-Expected-Outcomes/) | Success criteria after implementing the proposal |

#### Scope

These proposals **do not replace** the current S3 + Lambda Function URL + DynamoDB architecture. They add capability layers for edge HTTPS, access security, observability, short-code quality, deployment automation, and cost governance. Each item can be delivered in phases with technical evidence for evaluation and reporting.
