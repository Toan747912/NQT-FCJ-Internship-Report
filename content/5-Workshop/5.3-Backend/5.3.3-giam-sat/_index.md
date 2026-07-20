---
title: "CloudWatch + SNS monitoring"
date: 2026-07-14
weight: 3
chapter: false
pre: " 5.3.3. "
---

#### Goal

After create / redirect / stats worked, I added an **observe → alert** loop around Lambda: catch error patterns in logs, create an alarm, and email via SNS. (Atomic `clickCount` via `UpdateItem` is already in the handler in section 5.3.1.)

#### 1) CloudWatch Logs metric filter

On log group `/aws/lambda/url-shortener-backend`, I created metric filter **`URLShortenerErrorFilter`** with pattern `"[ERROR]"` (metric `ErrorCount`, namespace `URLShortenerApp`).

![Metric filter URLShortenerErrorFilter](/images/5-Workshop/5.3-Backend/metric-filter.png)

#### 2) SNS topic + email subscription

I created topic **`url-shortener-alerts`**, then an **EMAIL** protocol subscription (confirm before real alert mail arrives).

![SNS topic url-shortener-alerts](/images/5-Workshop/5.3-Backend/sns-topic.png)

![SNS email subscription (Pending confirmation)](/images/5-Workshop/5.3-Backend/sns-subscription.png)

#### 3) CloudWatch Alarms

I created alarms for the URL Shortener stack; the main error alarm is:

| Alarm | Condition (summary) |
| --- | --- |
| `URLShortener-Errors` | `ErrorCount >= 1` within ~5 minutes |
| `URLShortener-Throttles` | `Throttles >= 1` / 5 minutes |
| `URLShortener-Duration` | duration-related threshold |

![CloudWatch alarms list (URLShortener-Errors created)](/images/5-Workshop/5.3-Backend/alarm.png)

#### 4) Email when alarm enters ALARM

When the error metric crosses the threshold, CloudWatch changes state (e.g. `INSUFFICIENT_DATA` → `ALARM`) and SNS sends an AWS Notifications email.

![SNS alert email when alarm is ALARM](/images/5-Workshop/5.3-Backend/alarm-email.png)

#### What Insufficient data means

The alarm often shows **Insufficient data** when there are no datapoints yet (no `"[ERROR]"` logs in the evaluation window). That does **not** mean the alarm is broken — only that no error signal arrived. When Lambda logs enough `[ERROR]` lines, the metric rises and the alarm can go **In alarm** and notify SNS.

#### Architecture link

On the section 5.1 diagram, this is Steps 6–7: CloudWatch (Logs / Metrics / Metric filter / Alarms) → SNS Topic → admin email.
