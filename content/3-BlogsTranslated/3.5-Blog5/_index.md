---
title: "CloudWatch Lambda errors"
date: 2026-07-14
weight: 5
chapter: false
pre: " <b> 3.5. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | How to get notified on specific Lambda function error patterns using CloudWatch |
| Source | [AWS Cloud Operations Blog](https://aws.amazon.com/blogs/mt/get-notified-specific-lambda-function-error-patterns-using-cloudwatch/) |
| Topics | CloudWatch Logs filters / subscriptions, Lambda Errors metric, SNS notifications |
| Workshop link | Section 5.3.3 — metric filter `"[ERROR]"` + alarm + SNS |

#### 2. Summary

The article highlights a practical limit of CloudWatch Alarms on Lambda’s **Errors** metric: you learn *that* something failed, but not **what the log said**. For richer alerts, AWS combines **CloudWatch Logs filter patterns** (e.g. `ERROR`, `CRITICAL`, custom text) with subscriptions: matching lines invoke an error-processing Lambda → publish to **SNS** → email/SMS. That delivers both a signal and context, and can blueprint automated reactions to dangerous patterns.

#### 3. Main content

##### 3.1. Errors metric versus log filters

- **Errors metric**: aggregate per-minute signal — good for “did the function fail?”
- **Log filters**: match specific strings in CloudWatch Logs (e.g. `"[ERROR]"` written by code). Better for business-specific error text, not only runtime exceptions.

##### 3.2. Architecture in the article

Business Lambdas write logs → CloudWatch Logs → matching filter → “error processing” Lambda → SNS topic → subscribers. An event-driven observation pattern.

##### 3.3. Building and testing filters

Pick log group `/aws/lambda/<function-name>`, set a filter pattern, attach a destination. Validate by forcing matching logs and confirming SNS delivery. Filters that are too broad waste cost; too narrow miss incidents.

##### 3.4. Extensions

The same pattern can drive reactive automation (tickets, remediators), not only email.

#### 4. Reflection

In section 5.3.3 I implemented a related “log error → alert” path:

1. Metric filter on `/aws/lambda/url-shortener-backend` with pattern `"[ERROR]"`.
2. Metric `URLShortenerErrorCount` + Alarm `url-shortener-error-alarm`.
3. SNS email subscription.

![CloudWatch Alarm in the workshop](/images/3-BlogsTranslated/3.5-Blog5/cloudwatch-alarm.png)

Difference vs the article: subscription → processor Lambda for **log text** in SNS; I used metric filter → alarm → SNS for an **error-count** signal. Same **observe → alert** loop. Alarm **Insufficient data** when no `[ERROR]` lines exist is expected — the AWS post helps explain that correctly in the report instead of assuming a bad alarm config.
