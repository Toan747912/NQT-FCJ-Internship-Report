---
title: "DynamoDB counters"
date: 2026-07-14
weight: 4
chapter: false
pre: " <b> 3.4. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Implement resource counters with Amazon DynamoDB |
| Source | [AWS Database Blog](https://aws.amazon.com/blogs/database/implement-resource-counters-with-amazon-dynamodb/) |
| Topics | Atomic counters, UpdateItem, ConditionExpression, concurrency accuracy, retries |
| Workshop link | Section 5.3 — incrementing `clickCount` on redirect |

#### 2. Summary

The article digs into **resource counters** on DynamoDB — votes, inventory, event tickets — that must stay correct under concurrent updates. Undercount/overcount can cause overselling or false rejects. The author covers **seven approaches**, judging accuracy, cost, and complexity, and emphasizes distributed 500-series failures: clients may not know whether an update applied before retrying.

#### 3. Main content

##### 3.1. Atomic counters

Simplest path: one `UpdateItem` with `ADD` / numeric increment. DynamoDB serializes updates on the same item, so it races less than application-level Get-then-Put. Low cost, short code. Less accurate than some transactional patterns under failure+retry — fine when approximation or simple conditions suffice.

##### 3.2. ConditionExpression and thresholds

Conditions can block updates that would cross a threshold (e.g. never go below zero). On failure, DynamoDB returns a controlled error so the app can respond with 4xx instead of writing bad state.

##### 3.3. Approaches beyond atomic counters

Optimistic concurrency, transactions + client request tokens, marker items, item-collection / set counting — for systems needing stronger idempotency and accuracy (real sellable inventory), at higher cost/complexity.

##### 3.4. SDK retries

SDKs often retry automatically. Non-idempotent counters can overcount after ambiguous failures. Designers must choose: tolerate overcount on retry, undercount without retry, or move to idempotent patterns.

#### 4. Reflection

Atomic counters + conditions map directly to workshop `clickCount` logic:

- Redirect uses `UpdateCommand` for atomic increments instead of Get-then-Put.
- `ConditionExpression: attribute_exists(shortCode)` → missing codes ConditionalCheckFailed → 404 without creating ghost items.

![DynamoDB table url-shortener-links](/images/3-BlogsTranslated/3.4-Blog4/dynamodb-table.png)

![Items after redirect / clickCount tests](/images/3-BlogsTranslated/3.4-Blog4/dynamodb-items.png)

For a shortener lab, atomic counters are enough to demonstrate clicks. The blog justifies that choice and shows the next step if counting must be absolute later (transactions / idempotency tokens).
