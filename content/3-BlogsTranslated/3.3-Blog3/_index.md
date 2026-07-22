---
title: "Realtime video progress syncing with AWS AppSync"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Xây dựng tính năng đồng bộ tiến độ video (Progress Syncing) realtime với AWS AppSync |
| Author / Source | Toàn Ngô — [AWS Study Group VN](https://www.facebook.com/share/p/1FPP7H5zBg/) (Facebook community post) |
| Topics | AWS AppSync, GraphQL, DynamoDB Direct Resolver, WebSocket subscriptions, realtime sync, EdTech |
| Related AWS docs | [AppSync real-time data](https://docs.aws.amazon.com/appsync/latest/devguide/real-time-data.html), [DynamoDB resolvers tutorial](https://docs.aws.amazon.com/appsync/latest/devguide/tutorial-dynamodb-resolvers.html) |

#### 2. Summary

Following the Transcribe subtitle post, the team shares a second EdTech/video architecture: **realtime progress syncing** across devices — pause a lecture on a laptop and continue on a phone at the exact same second.

Instead of a traditional REST API that repeatedly saves and polls watch state (latency and cost grow as traffic scales), they use **AWS AppSync (GraphQL)** with **Amazon DynamoDB**, relying on **WebSockets** for push updates.

![Facebook post by AWS Study Group VN on AWS AppSync progress syncing](/images/3-BlogsTranslated/3.3-Blog3/facebook-post.png)

#### 3. Main content

##### 3.1. Pain point: REST polling does not scale well

Saving progress via REST every few seconds and re-fetching on another device works for demos, but at scale it increases latency and backend load. Maintaining your own WebSocket fleet for push updates adds operational complexity.

##### 3.2. Save progress with GraphQL Mutation + Direct Resolver

While the learner watches, the frontend periodically (e.g. every 5 seconds) sends the current playback timestamp to AppSync via a **GraphQL Mutation**.

AppSync uses a **Direct Resolver** to write progress straight into a **DynamoDB** table — fast and cost-efficient because it skips an intermediate **Lambda** hop for this simple write path.

##### 3.3. Sync instantly with GraphQL Subscriptions

When the same account opens on another device, that client connects with a **GraphQL Subscription**. Whenever DynamoDB gets a new progress record (through AppSync), the second device receives the update in realtime over **WebSocket** and **seeks** the video to the correct position.

##### 3.4. Operational advantage

Teams do not manage WebSocket infrastructure themselves. AppSync handles connection lifecycle and scales the realtime layer, reducing backend burden for multi-device sync.

![Progress Syncing realtime with AWS AppSync and Amazon DynamoDB](/images/3-BlogsTranslated/3.3-Blog3/appsync-progress-sync.png)

#### 4. Reflection

This pattern complements Blog 2 (Transcribe word timestamps for karaoke-style highlights): Blog 2 improves **in-player experience**, while Blog 3 improves **cross-device continuity**. Together they sketch a fuller lecture-video platform on managed AWS services.

Compared with my workshop URL Shortener, the shared idea is still **managed data + thin clients**, but AppSync adds a **push** channel that my Function URL + DynamoDB design does not provide out of the box.

| Item | Progress Sync (AppSync + DynamoDB) | My workshop |
| --- | --- | --- |
| API style | GraphQL (Mutation + Subscription) | HTTPS Function URL (REST-like) |
| Data store | DynamoDB via Direct Resolver | DynamoDB from Lambda |
| Sync model | Push over WebSocket | Client must request again |
| Middle tier | Often no Lambda on write path | Lambda always in the path |

Takeaway: for “continue watching on another device,” **AppSync Subscriptions + DynamoDB** is a cleaner fit than polling REST. Direct Resolvers are worth remembering whenever the write is a simple key/value update and Lambda would only forward the call.
