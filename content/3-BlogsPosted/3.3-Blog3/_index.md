---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# LIVE-AUCTION: BUILDING A REAL-TIME AUCTION PLATFORM ON AWS SERVERLESS

<figure style="text-align: center;">
    <a href="/FCAJ-Internship-Report/images/3-BlogPosted/high_availability_live_auction_aws_2026_v2.png">
        <img src="/FCAJ-Internship-Report/images/3-BlogPosted/high_availability_live_auction_aws_2026_v2.png" alt="Live-Auction AWS serverless architecture" style="max-width: 100%; height: auto;">
    </a>
    <figcaption style="text-align: center;">AWS serverless architecture for the Live-Auction platform.</figcaption>
</figure>

How can an auction platform keep one consistent price when many bidders submit bids almost at the same time? That was the practical problem behind our Live-Auction project.

The project started as a familiar web application with a React/Vite frontend, a FastAPI backend, and a MySQL database. As we analyzed the requirements more closely, we found that the system also needed real-time updates, concurrent-bid handling, authentication, image storage, scheduled state changes, and recovery controls. The challenge was not simply moving code to AWS. It was deciding which operations should remain synchronous and which should be separated into small event-driven services.

The current demonstration does not claim to process the traffic of a large commercial auction marketplace. Estimating the true scale and operating cost was difficult during the early stages, and the FastAPI/MySQL path is still retained for local development. However, the serverless architecture has been implemented and tested around concrete auction use cases, providing a strong foundation for future improvements.

## The auction-system problem

An auction platform cannot safely store only the last bid received. When several bidders submit requests for the same item, the system must ensure that:

* a bid below the minimum increment is rejected;
* concurrent bids cannot overwrite the wrong state;
* a repeated request does not create a second transaction;
* accepted or rejected results reach everyone watching the room; and
* failures and state changes remain traceable.

## The serverless architecture

### Frontend and content delivery

The React/Vite applications are built as static assets and delivered through Amazon CloudFront from private Amazon S3 buckets. The bidder application and admin dashboard use separate deployment artifacts. Product images are served through a dedicated media distribution so that file traffic does not compete with API requests.

### Authentication and authorization

Amazon Cognito User Pool handles registration, confirmation, login, password recovery, and token refresh. Cognito groups separate normal users from administrators. A post-confirmation Lambda completes user setup after sign-up. REST and WebSocket requests validate the Cognito JWT before protected operations are allowed.

### Focused Lambda services

The REST API is connected to focused handlers rather than one large backend process:

1. `session-service` manages auction sessions and session rules.
2. `item-service` manages items and issues presigned image-upload URLs.
3. `query-service` serves the catalog, auction state, and bid history.
4. `admin-command` handles moderation, scheduled transitions, and audit queries.

## Real-time bid processing

1. A bidder connects to the API Gateway WebSocket API and joins an item room.
2. `ws-authorizer` validates the token; `ws-handler` stores the connection, room membership, and bidder alias in DynamoDB.
3. When the bidder submits a bid, the WebSocket handler validates the context and sends a command to Amazon SQS FIFO with a message group for the item.
4. The `bid-processor` Lambda checks the session and minimum increment and performs a conditional update on `item_auction_state`.
5. The processor writes an accepted or rejected event and an idempotency record so repeated requests do not change the result.
6. The `broadcast` Lambda reads active connections and sends the outcome to every participant through the API Gateway management API. Stale connections are removed during this step.

## Automation and operations

EventBridge Scheduler can invoke `admin-command` for scheduled start, close, and other lifecycle transitions. A scheduler dead-letter queue keeps failed invocations visible for investigation.

Terraform modules provision identity, data, messaging, compute, API, edge, security, observability, backup, and CI/CD in dependency order. CodeBuild creates deterministic Lambda packages and frontend assets, while CodePipeline and CodeDeploy support controlled version promotion.

CloudWatch collects Lambda logs and custom bid metrics and raises alarms for latency, function errors, rejected bids, and DLQ messages. CloudTrail, AWS Config, IAM Access Analyzer, versioned audit storage, and AWS Backup provide operational evidence and recovery controls.

## Practical considerations

* Serverless still requires explicit boundaries, access patterns, retry behavior, and permission policies.
* SQS FIFO ordering applies within a message group, so the group key must match the unit that needs sequential processing.
* Conditional writes and idempotency records must be designed together to handle race conditions and duplicate delivery.
* WebSocket connections can disappear at any time, so TTL and cleanup are necessary.
* Reliability must be evaluated together with observability, DLQs, audit records, and backups, not only with Lambda scaling.

## Lessons learned

The main lesson from the project is that AWS provides the building blocks, but correctness comes from how those blocks are connected. Splitting the system into independent services forced us to define the source of truth, the messages that require ordering, the failures that can be retried, and the operations that must be audited.

Within the current scope, Live-Auction demonstrates that a real-time auction workflow can be decomposed into testable services and deployed repeatedly with Terraform. Future work includes larger-scale load testing, multi-region recovery drills, richer notifications, and deeper analytics.

## References

* [Original post on Facebook](https://www.facebook.com/share/p/14njRQp6aFU/)
* [Amazon API Gateway WebSocket APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-overview.html)
* [Amazon SQS FIFO queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html)
* [DynamoDB conditional writes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
* [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

Thank you for taking the time to read about our project. Feedback on the bidding flow, serverless boundaries, and ways to improve platform reliability would be very welcome.

#AWS #Serverless #AWSLambda #AmazonDynamoDB #AmazonAPIGateway #AmazonCognito #AmazonSQS #Terraform #CloudEngineering #LiveAuction
