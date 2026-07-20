---
title: "Week 11 Worklog"
date: 2024-01-01
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

**Period:** 29/06/2026 – 05/07/2026

### Goals for Week 11:

* Get hands-on with AI/ML on AWS through SageMaker, Rekognition, Comprehend, and Bedrock.
* Tell apart plug-and-play AI Services from ML platforms meant for custom model training.

### Planned work this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Compare AI Services (Rekognition, Comprehend) against the ML Platform (SageMaker); get an overview of Generative AI and Bedrock. | 29/06/2026 | 29/06/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| Tue | Lab 1: Spin up a SageMaker Notebook Instance and train an image classification model. | 30/06/2026 | 01/07/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| Wed | Roll out a SageMaker Endpoint and invoke the inference API, reaching roughly 91% accuracy on the test set. | 02/07/2026 | 02/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| Thu | Practice wiring AI into applications via API and look into Foundation Models on Amazon Bedrock. | 03/07/2026 | 03/07/2026 | <https://000056.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |
| Fri | Write a Lambda function that auto-removes the SageMaker Endpoint once testing wraps up to avoid ongoing cost; close out the week. | 04/07/2026 | 04/07/2026 | <https://000022.awsstudygroup.com/><br><https://000066.awsstudygroup.com/> |

### What was accomplished in Week 11:

* Learned to tell AI Services apart from the SageMaker ML Platform.
* Trained and deployed an image classification model on SageMaker, hitting around 91% accuracy.
* Understood how to work with Bedrock Foundation Models through a single unified API.

### Challenges & Solutions:

* Deploying the endpoint took about 7 minutes and would keep costing money if left running → addressed this by writing a Lambda function that deletes the endpoint automatically once testing is done.

### Plan for Next Week:

* Wrap up the program, finish the capstone project, and put together the internship report.
