---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# LAMBDA SCALES FAST, BUT THE DATABASE DOES NOT SCALE THE SAME WAY

While working on the Live-Auction project, our team began moving backend capabilities from FastAPI toward AWS Lambda while continuing to use MySQL on Amazon RDS. That architecture change required us to reconsider an important operational concern: database connections.

## The connection model changes with serverless

For a long-running application on an EC2 instance or container, the connection model is usually predictable:

`Application -> Connection Pool -> MySQL`

The application keeps a connection pool with a relatively stable upper limit and reuses connections across requests. AWS Lambda changes that assumption. Lambda can create more execution environments as concurrent demand increases, while Amazon RDS still has finite connection, CPU, and memory capacity.

Lambda can scale with the incoming workload, but its downstream dependencies do not necessarily have the same throughput. Reserved concurrency can help limit a function so it does not overload resources behind it, including a database.

## Why this matters for an auction system

Imagine that traffic rises sharply when an auction session approaches its closing time. At a given point, 500 concurrent requests can require up to 500 concurrent Lambda executions. If each execution creates a new database connection, Amazon RDS may need to process a sudden surge of connections.

The Lambda function itself may still scale, but the database can experience:

* connection exhaustion;
* increased connection-creation time;
* higher query latency;
* slower transactions;
* request timeouts; and
* impact on other workloads sharing the same database.

For an auction platform, the final phase of a session is exactly when bid traffic is most likely to peak. Database connection management therefore needs to be treated as part of the serverless design, not as a separate afterthought.

## How Amazon RDS Proxy helps

Amazon RDS Proxy is an AWS-managed proxy that maintains a pool of database connections. Rather than allowing every Lambda execution environment to open and manage its own direct connection to RDS, the application connects through the proxy:

`Lambda -> Amazon RDS Proxy -> Amazon RDS`

The proxy can reuse and pool database connections, reducing pressure on the database when short-lived Lambda executions occur at high concurrency. It can also improve resilience during database failover events.

RDS Proxy is not a replacement for query optimization, transaction design, or appropriate concurrency limits. It is one important component of a broader design that considers both Lambda and the database it depends on.

## Lessons from the project

Serverless scaling should never be assessed by looking at Lambda alone. The capacity, connection limits, and failure modes of every downstream dependency must be considered. For Live-Auction, that means designing the Lambda-to-RDS path carefully so that a surge in bids does not create avoidable pressure on MySQL.

## References

* [Original post on AWS Study Group VN](https://www.facebook.com/share/p/1GhthtrrpB/)
* [Lambda scaling behavior](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html)
* [Using Amazon RDS Proxy with AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-rds-proxy.html)
* [Amazon RDS Proxy concepts](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html)
