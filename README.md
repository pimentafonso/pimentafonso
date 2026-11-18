### Hi, I'm Afonso

Backend developer (Node.js, Django) building production-shaped systems on AWS. I care about the failure paths: I deploy what I build on real AWS, break it on purpose, and publish what I measured, including what went wrong. Currently studying for AWS Solutions Architect Associate.

#### [aws-ha-web-platform](https://github.com/pimentafonso/aws-ha-web-platform)

A highly available web platform in CloudFormation: ECS Fargate across two AZs, RDS PostgreSQL Multi-AZ, ElastiCache for Valkey, CloudFront and WAF, deployed from GitHub Actions with OIDC (no long-lived keys).

- Stopping a task and failing over Valkey: **0 errors** seen by clients.
- RDS Multi-AZ failover: the database was back in **29 s** (48 s on a second run), but the app saw database errors for **6 to 14 minutes**. I traced it to IAM database authentication on the new primary; fix and re-measure next.

#### [aws-event-driven-orders](https://github.com/pimentafonso/aws-event-driven-orders)

Event-driven order processing in Terraform: HTTP API with idempotency keys, DynamoDB Streams as an outbox, an EventBridge Pipe, a Step Functions saga with compensation, and SQS with dead-letter queues.

- A k6 load test at 5, 10 and 20 orders a second found a real bug: **106** DynamoDB transaction conflicts were reported to customers as out of stock. After the fix: **4,169 of 4,169** orders confirmed.
- Fault injection at 50% payment and notifier failure: 40 orders, **0** failed executions, every dead-lettered notification redriven.

**Tools:** AWS · Terraform · CloudFormation · GitHub Actions · Python · Node.js · PostgreSQL · DynamoDB · Docker · k6

[LinkedIn](https://www.linkedin.com/in/silvafonso)
