---
title: "Prerequisites"
date: 2026-07-14
weight: 2
chapter: false
pre: " 5.2. "
---

#### Goal

Prepare the foundation (data table + IAM permissions) so Lambda only needs to attach a role and run code, without mid-flight policy fixes.

#### Fixed resources used

| Component | Actual value |
|---|---|
| Region | `ap-southeast-1` (Singapore) |
| DynamoDB table | `url-shortener-links` |
| Partition key | `shortCode` (String) |
| Capacity mode | On-demand |
| TTL attribute | `expiresAt` (Time to Live enabled) |
| Lambda function | `url-shortener-backend` |
| IAM Role | `url-shortener-lambda-role` |
| Inline policy | `url-shortener-dynamodb-policy` |
| S3 bucket | `url-shortener-frontend-forward` |

#### DynamoDB table

I created `url-shortener-links` with:

- **Partition key:** `shortCode` (S) — enough for lookup by short code.
- **No sort key** — each `shortCode` is one independent item.
- **On-demand** — fits lab traffic without sizing RCU/WCU upfront.

After creation, the table status is **Active** in `ap-southeast-1`.

![url-shortener-links table created successfully](/images/5-Workshop/5.2-Chuan-bi/create-table.png)

Attributes like `originalUrl`, `clickCount`, `createdAt`, and `expiresAt` are written on Put/Update; DynamoDB does not require a relational-style schema declaration first.

#### Time to Live (TTL)

I enabled **Time to Live** on the table with attribute **`expiresAt`** so expired items can be removed automatically by epoch time — useful if short links should expire after a lab/demo and the table should not grow forever.

![TTL enabled with expiresAt attribute](/images/5-Workshop/5.2-Chuan-bi/ttl-settings.png)

#### IAM role for Lambda

I created role **`url-shortener-lambda-role`** trusted by **AWS Lambda** as the backend execution role.

![url-shortener-lambda-role created](/images/5-Workshop/5.2-Chuan-bi/iam-role-created.png)

The role has at least two permission layers:

1. `AWSLambdaBasicExecutionRole` (AWS managed) — write CloudWatch Logs.
2. `url-shortener-dynamodb-policy` (customer inline) — only required actions on the `url-shortener-links` table ARN.

![url-shortener-lambda-role permissions](/images/5-Workshop/5.2-Chuan-bi/iam-role.png)

DynamoDB policy content (replace `<ACCOUNT_ID>`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowDynamoDBAccessToShortenerTable",
      "Effect": "Allow",
      "Action": [
        "dynamodb:PutItem",
        "dynamodb:GetItem",
        "dynamodb:UpdateItem"
      ],
      "Resource": "arn:aws:dynamodb:ap-southeast-1:<ACCOUNT_ID>:table/url-shortener-links"
    }
  ]
}
```

**Least privilege:** no `Scan`/`DeleteItem`/`*` across the region — enough for create + redirect Update + stats read. Missing `UpdateItem` breaks click increments on redirect.

#### Notes before Backend

- DynamoDB region, Lambda region, and `TABLE_NAME` must match (`url-shortener-links`).
- S3 bucket names are globally unique; I used suffix `forward` → `url-shortener-frontend-forward`.
