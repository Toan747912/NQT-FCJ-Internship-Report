---
title: "Week 10 Worklog"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Period:** 22/06/2026 – 28/06/2026

### Goals for Week 10:

* Stand up a data lake on AWS combining S3, Glue, Athena, and QuickSight.
* Run queries against large S3 datasets without standing up a conventional database server.

### Planned work this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| Mon | Review the data lake architecture: S3 for storage, Glue for ETL, Athena for querying, QuickSight for BI. | 22/06/2026 | 22/06/2026 | <https://000070.awsstudygroup.com/><br><https://000035.awsstudygroup.com/> |
| Tue | Lab 1: Push a CSV of roughly 100,000 rows into S3, then build an Athena table and query it with SQL directly. | 23/06/2026 | 24/06/2026 | <https://000106.awsstudygroup.com/><br><https://000040.awsstudygroup.com/> |
| Wed | Work through AWS Glue Crawler / ETL exercises; resolve DynamicFrame API errors by converting to a Spark DataFrame via `toDF()`. | 25/06/2026 | 25/06/2026 | <https://000040.awsstudygroup.com/><br><https://000105.awsstudygroup.com/> |
| Thu | Cut Athena costs using Parquet format and daily partitioning, then build visualizations in QuickSight. | 26/06/2026 | 26/06/2026 | <https://000073.awsstudygroup.com/><br><https://000106.awsstudygroup.com/> |
| Fri | Recap the full S3 → Glue → Athena → QuickSight pipeline along with cost-saving best practices. | 27/06/2026 | 27/06/2026 | <https://000070.awsstudygroup.com/><br><https://cloudjourney.awsstudygroup.com/> |

### What was accomplished in Week 10:

* Ran Athena queries against large S3 datasets with no database server involved.
* Applied Glue for ETL work and cut Athena costs via Parquet plus partitioning.
* Built visualizations of the results in QuickSight.

### Challenges & Solutions:

* A Glue Job failed from misuse of the DynamicFrame API → resolved by following the Glue documentation and converting to a Spark DataFrame with `toDF()`.

### Plan for Next Week:

* Dive into AI/ML services — SageMaker, Rekognition, and Amazon Bedrock.
