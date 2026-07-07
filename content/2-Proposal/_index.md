---
title: "Proposal"
date: 2026-07-13
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# LIVE AUCTION PLATFORM ON AWS

## A serverless real-time auction platform for bidders, sellers, and administrators

### 1. Executive Summary

Live-Auction is an online auction platform for browsing products, creating auction sessions, placing bids, and receiving price updates in real time. The repository contains an earlier FastAPI/MySQL implementation for local development and a serverless AWS deployment path implemented with Terraform and Lambda handlers.

The AWS architecture uses React/Vite applications delivered through Amazon CloudFront and private Amazon S3 buckets. Amazon Cognito manages authentication and `USER`/`ADMIN` groups. Amazon API Gateway exposes REST and WebSocket APIs. AWS Lambda provides focused session, item, query, administration, WebSocket, bid-processing, and broadcast handlers. Amazon DynamoDB stores catalog records, current auction state, bid events, WebSocket connections, idempotency records, and audit events.

The main design goal is to process concurrent bids correctly. Bid commands are ordered through Amazon SQS FIFO, validated by a Lambda processor, applied with conditional DynamoDB writes, and broadcast to all connected participants. EventBridge Scheduler manages time-based transitions, while CloudWatch, CloudTrail, AWS Config, IAM Access Analyzer, and AWS Backup support operation and recovery.

### 2. Problem Statement and Objectives

An auction platform must keep one consistent price while many bidders submit requests almost simultaneously. It must reject bids below the minimum increment, prevent duplicate requests from being applied twice, preserve an audit trail, and notify connected users without requiring page refreshes.

The project objectives are to:

- provide bidder, seller, and administrator workflows;
- support Cognito registration, confirmation, login, and role-based authorization;
- manage sessions, categories, items, presigned image uploads, and bid history;
- provide WebSocket room membership and real-time bid results;
- provision the system repeatably with Terraform and deliver artifacts through CodeBuild/CodePipeline; and
- add monitoring, security evidence, dead-letter queues, and backup controls.

### 3. AWS Architecture

The following image is the reference architecture for the Live-Auction AWS deployment. Click it to view the full-size diagram.

[![Live-Auction AWS serverless architecture](/FCAJ-Internship-Report/images/2-Proposal/image.png?v=20260809)](/FCAJ-Internship-Report/images/2-Proposal/image.png?v=20260809)

#### Client and edge

Bidder, seller, and admin React/Vite applications are built as static assets. CloudFront distributes the frontend from private S3 origins using Origin Access Control. A separate media distribution serves product images from the encrypted media bucket.

#### Identity and API

Cognito User Pool handles account flows and groups. A post-confirmation Lambda completes the default user setup. REST API Gateway routes authenticated requests to `session-service`, `item-service`, `query-service`, and `admin-command`. The WebSocket API uses a Lambda authorizer, `ws-handler`, and routes for `$connect`, `$disconnect`, `joinRoom`, and `placeBid`.

#### Data and bid processing

DynamoDB tables are separated by access pattern: `auction_catalog`, `category_catalog`, `item_auction_state`, `bid_events`, `websocket_connections`, `item_bidder_aliases`, `idempotency`, and `admin_audit_events`. The item service issues presigned URLs so the browser can upload media directly to S3.

The bid flow is:

1. A bidder connects and joins an item room.
2. `ws-handler` validates the context and sends the command to the SQS FIFO bid queue.
3. `bid-processor` validates the session and minimum increment and performs a conditional state update.
4. The processor writes an accepted or rejected event and an idempotency record.
5. `broadcast` publishes the result to active room connections through the API Gateway management API.

EventBridge Scheduler invokes `admin-command` for scheduled transitions. Bid and scheduler queues have DLQs so failed messages remain visible for investigation.

### 4. Infrastructure and Delivery

Terraform modules are applied in dependency order: remote state, foundation, identity, data, messaging, compute, API, edge, observability, security, backup, and CI/CD. Remote state is stored in S3 with a DynamoDB lock table.

CodeBuild creates deterministic Lambda packages and frontend assets. CodePipeline stores encrypted versioned artifacts and promotes a selected Lambda version through CodeDeploy. CloudWatch collects logs and custom metrics and raises alarms for bid latency, Lambda errors, rejected bids, and DLQ messages. CloudTrail, AWS Config, IAM Access Analyzer, and AWS Backup provide audit and recovery controls.

### 5. Security and Reliability

- Validate Cognito JWTs and enforce group-based permissions for protected operations.
- Use least-privilege IAM roles and keep secrets outside source control.
- Keep S3 buckets private and deliver media through CloudFront origin access control.
- Use FIFO message groups, conditional DynamoDB writes, idempotency records, and bounded retries for bid correctness.
- Monitor stale WebSocket connections, function failures, latency, and DLQ depth.
- Retain admin audit events and test scoped backup and restore procedures.

The current serverless stack does not provision EC2, RDS, Aurora, RDS Proxy, ECS, ALB, VPC, or Kinesis. Those services remain possible future alternatives rather than deployed components of this proposal.

### 6. Expected Results

The completed platform is expected to provide a deployable browser-based auction experience with Cognito authentication, seller and administrator workflows, catalog and media management, real-time auction rooms, ordered bid processing, bid history, audit events, operational alarms, and repeatable Terraform/CI/CD deployment.
