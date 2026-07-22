---
title: "Automatic Spaced Repetition System with Amazon Bedrock & Step Functions"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Tự động tạo hệ thống ôn tập "Spaced Repetition" bằng Amazon Bedrock & Step Functions |
| Author / Source | Toàn Ngô — [AWS Study Group VN](https://www.facebook.com/share/p/1DiaeMY6Sv/) (Facebook community post) |
| Topics | GenAI, Amazon Bedrock, AWS Step Functions, Wait state, event-driven architecture, EdTech |

#### 2. Summary

The post shares an architecture the AWS Study Group VN team built to solve a common EdTech pain point: automatically generating and scheduling review content based on **Spaced Repetition** (reviewing material at increasing intervals — e.g. 1 day, 3 days, 7 days after first learning — to improve long-term retention).

Instead of a traditional cron job that repeatedly polls a database to check whose turn it is to review, the team designed an **event-driven** flow that combines **Amazon Bedrock** for content generation with **AWS Step Functions** for orchestration and scheduling.

![Facebook post by AWS Study Group VN describing the Spaced Repetition architecture](/images/3-BlogsTranslated/3.1-Blog1/facebook-post.png)

#### 3. Main content

##### 3.1. Automatic question generation with GenAI (Amazon Bedrock)

When a learner finishes watching a lesson video, the system takes the lesson transcript and passes it through a large language model on **Amazon Bedrock**. With a single well-crafted prompt, Bedrock generates 3–5 multiple-choice questions closely tied to what was just studied — removing the need to manually author quiz content for every lesson.

##### 3.2. Scheduling reviews with AWS Step Functions

Rather than a cron job constantly scanning the database, the whole review pipeline is pushed into a **Step Functions** state machine. The key feature exploited here is the **Wait state**: the workflow "sleeps" for exactly 1 day, then sends the first review email/notification, sleeps again for 3 more days, sends the next review, and so on — modelling the spaced-repetition timeline directly as workflow states instead of application logic.

##### 3.3. Cost optimization

A Step Functions **Wait state** does not charge for the time spent waiting — cost is only incurred when the state **transitions** (i.e., when something actually happens). This is significantly cheaper than keeping an EC2 instance or a Lambda function alive (or repeatedly invoked) just to check "is it time yet?" for every single learner.

![Spaced Repetition workflow: Bedrock generates content, Step Functions schedules reviews at 1/3/7-day boxes](/images/3-BlogsTranslated/3.1-Blog1/spaced-repetition-architecture.png)

##### 3.4. Advantage: workflow as a visual, editable state machine

By moving the review scheduling logic into Step Functions, the whole process becomes a visual **state machine diagram** rather than logic buried inside application code. The team can change the review cadence (e.g., add a 14-day box) or the notification channel without touching the core business logic — only the state machine definition changes.

The post also references the official AWS docs used as the technical basis:
- [Integrating Amazon Bedrock with Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-bedrock.html)
- [Using the Wait state in Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-wait-state.html)

#### 4. Reflection

Although this post targets an EdTech use case rather than the URL-shortener problem in my workshop, the underlying architectural principle is the same one I applied in Section 5: **prefer event-driven, managed services over polling loops** to save cost and reduce operational overhead.

| Item | Spaced Repetition (Bedrock + Step Functions) | My workshop |
| --- | --- | --- |
| Trigger model | Event-driven state machine (Wait state) | Event-driven Lambda Function URL |
| "Waiting" mechanism | Step Functions Wait state (no compute cost while idle) | Not needed — request/response is synchronous |
| Content/logic generation | Amazon Bedrock (GenAI) | Static shortener logic in Lambda |
| Observability | Visual state machine graph | CloudWatch Logs + metric filter + SNS alarm (Section 5.3.3) |

The biggest takeaway for me is the **Wait state pattern**: it is a clean way to implement "do X, then wait N days, then do Y" without a scheduler service or a cron job that has to keep checking timestamps. If I extend my Serverless URL Shortener in the future — for example, to send a reminder when a short link is about to expire, or to auto-archive links unused for 30 days — Step Functions Wait states would be a much more cost-efficient option than a periodic Lambda triggered by EventBridge every few minutes. It is also a good reminder that combining GenAI (Bedrock) with orchestration services (Step Functions) is becoming a common pattern for building smart, low-maintenance automation on AWS.
