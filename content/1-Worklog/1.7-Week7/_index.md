---
title: "Week 7 Worklog"
date: 2026-07-27
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Build and test the infrastructure components for Live Auction.
* Complete authentication, auction workflows, and realtime frontend features.
* Expand backend unit-test coverage and validate build artifacts.
* Attend the AWS FCAJ Agent Forge - Deepdive event.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 1 | - Added AWS infrastructure and integration test scripts <br> - Configured frontend runtime and test tooling <br> - Wrote unit tests for shared auction utilities <br> - Studied lab **000140 - Distributed Tracing with X-Ray and CloudWatch** | 07/27/2026 | 07/27/2026 | [Infrastructure](https://github.com/CallmeSen/Live-Auction/commit/eb8306b) <br> [Frontend tooling](https://github.com/CallmeSen/Live-Auction/commit/5513c30) <br> [Backend utility tests](https://github.com/CallmeSen/Live-Auction/commit/caabe8b) <br> <https://000140.awsstudygroup.com/> |
| 2 | - Built the authentication provider and Cognito operations <br> - Completed the auction room, bid panel, and auction pages <br> - Added tests for admin commands and authorization <br> - Studied lab **000141 - Cross-Domain Authentication with Amazon Cognito** | 07/28/2026 | 07/28/2026 | [Authentication and auction workflows](https://github.com/CallmeSen/Live-Auction/commit/81665b3) <br> [Authorization tests](https://github.com/CallmeSen/Live-Auction/commit/7569815) <br> <https://000141.awsstudygroup.com/> |
| 3 | - Connected realtime bidding and serverless catalog services <br> - Built WebSocket protocol/client adapters <br> - Added tests for auction and realtime handlers <br> - Studied lab **000078 - Serverless Backend with Lambda, S3, and DynamoDB** | 07/29/2026 | 07/29/2026 | [Realtime and serverless services](https://github.com/CallmeSen/Live-Auction/commit/d94254c) <br> [Auction/realtime tests](https://github.com/CallmeSen/Live-Auction/commit/99893b9) <br> <https://000078.awsstudygroup.com/> |
| 4 | - Tested deterministic zip generation and Lambda build artifacts <br> - Updated test configuration to validate artifact reproducibility <br> - Studied lab **000022 - Serverless Automation with AWS Lambda** | 07/30/2026 | 07/30/2026 | [Build artifact tests](https://github.com/CallmeSen/Live-Auction/commit/2f9d917) <br> <https://000022.awsstudygroup.com/> |
| 5 | - Attended the AWS FCAJ Agent Forge - Deepdive <br> - Learned about Agentic AI architecture, prompts, tools, context, and actions <br> - Practiced building and testing an agent workflow on AWS | 08/01/2026 | 08/01/2026 | [Event 3 report](../../4-EventParticipated/4.3-Event3/) <br> [AWS FCAJ Agent Forge - Deepdive](https://www.youtube.com/live/F58sam40jxk) <br> [AgentForge workshop](http://agentforge-hcmc-workshop-p371s08u.s3-website-ap-southeast-1.amazonaws.com/00-Overview/00-Dashboard-Overview.html) |

### Week 7 Achievements:

* Built the infrastructure and runtime/test tooling foundations for the frontend and backend, giving local and integration checks a more consistent configuration.

* Completed the authentication, auction room, bidding, and serverless service integration flows, connecting the user experience more clearly with the supporting services.

* Expanded backend test coverage for utilities, authorization, auction handlers, and realtime handlers, allowing more scenarios to be checked as the system continued to change.

* Learned how to validate the reproducibility of Lambda build artifacts and why repeatable artifacts are important for a reliable serverless deployment process.

* Learned more about Agentic AI architecture and the process of building an agent workflow on AWS.

---
