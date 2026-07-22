---
title: "Auto-highlight video subtitles synced with speech using Amazon Transcribe"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

#### 1. Source information

| Item | Details |
| --- | --- |
| Original title | Tự động hóa tính năng bôi sáng phụ đề video đồng bộ với giọng đọc bằng Amazon Transcribe |
| Author / Source | Toàn Ngô — [AWS Study Group VN](https://www.facebook.com/share/p/191PW65UTV/) (Facebook community post) |
| Topics | Amazon Transcribe, S3, Lambda, Step Functions, serverless media pipeline, EdTech, karaoke-style subtitle highlight |
| Related AWS blogs | [Serverless video subtitles](https://aws.amazon.com/blogs/compute/implementing-serverless-video-subtitles/), [Video subtitles with translation (ML)](https://aws.amazon.com/blogs/machine-learning/create-video-subtitles-with-translation-using-machine-learning/) |

#### 2. Summary

The post describes a practical EdTech / video-streaming use case: **word-level subtitle highlighting** that stays in sync with the speaker — similar to karaoke — without manually aligning timestamps or editing rigid `.srt` files.

The proposed design is a **serverless pipeline**: upload video to **Amazon S3** → trigger **Lambda** (or orchestrate with **Step Functions**) → run an **Amazon Transcribe** job → consume a rich JSON transcript on the frontend to highlight the current word from the video player's current time.

![Facebook post by AWS Study Group VN on Amazon Transcribe subtitle highlighting](/images/3-BlogsTranslated/3.2-Blog2/facebook-post.png)

#### 3. Main content

##### 3.1. Pain point: manual sync is expensive

Traditionally, building a transcript that matches spoken audio requires manual time alignment or hard-to-maintain `.srt` files. For lecture platforms with many videos, that effort does not scale.

##### 3.2. Serverless workflow with Amazon Transcribe

1. The user uploads a lecture video to **Amazon S3**.
2. An S3 event invokes **AWS Lambda** (or starts an **AWS Step Functions** workflow) to create an **Amazon Transcribe** transcription job.
3. Transcribe returns not only plain text, but a detailed **JSON** where **each word** has `start_time`, `end_time` (millisecond precision), and a **confidence** score.
4. That JSON is stored in S3 (or a database) for the frontend to fetch.

##### 3.3. Frontend karaoke-style highlight

On the client, while the video plays, a small tracker compares the player's **current time** with each word's `start_time` / `end_time` and changes color / highlight for the word being spoken — matching the lecturer in near real time.

##### 3.4. Cost optimization

Transcribe is billed by **minutes of audio processed**. To cut cost and job time, extract audio (e.g. MP3) with **Lambda** or **Amazon Elastic Transcoder** first, then send the lighter audio file to Transcribe instead of the full heavy video.

The related AWS Machine Learning Blog diagram also shows how the same transcript can feed **AWS Translate**, **Amazon Polly** (translated audio), Python subtitle generation, and **MoviePy** assembly into a final media file — useful when the platform needs multi-language subtitles or dubbed audio as well as highlight sync.

![Serverless subtitle / translation pipeline: Transcribe → Translate → Polly + Python subtitles → MoviePy](/images/3-BlogsTranslated/3.2-Blog2/transcribe-subtitle-architecture.png)

#### 4. Reflection

This post connects well to my workshop mindset: **event-driven serverless processing** (S3 → Lambda / Step Functions) and storing structured results for a thin client to consume — similar in spirit to my URL Shortener (S3 + Lambda Function URL + DynamoDB), but for media/AI services instead of link redirects.

| Item | Transcribe subtitle highlight | My workshop |
| --- | --- | --- |
| Trigger | S3 upload event | HTTPS request to Function URL |
| Heavy work | Amazon Transcribe job (async) | Lambda handler (sync request/response) |
| Result store | JSON transcript on S3 / DB | Mapping in DynamoDB |
| Client role | Highlight words by `currentTime` vs timestamps | Shorten / redirect / stats UI |

Takeaway: when a product needs precise speech timing, **Amazon Transcribe's word-level timestamps** remove most of the manual subtitle alignment work. Pairing that with a serverless upload pipeline keeps operations light — and extracting audio before Transcribe is a simple, high-impact cost tip I would apply if I built a lecture-video feature later.
