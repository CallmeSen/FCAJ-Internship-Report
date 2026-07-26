---
title: "Week 6 Worklog"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Understand the main use cases of the auction system.
* Integrate category, auction session, and authentication APIs.
* Build serverless backend services for the catalog, sessions, and realtime bidding.
* Standardize the Lambda packaging process.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 1 | - Reviewed the place-bid, view-bids, and start-auction-session use cases <br> - Checked CORS and authentication APIs <br> - Followed the removal of the old frontend deployment <br> - Studied lab **000066 - Building Serverless APIs** | 07/20/2026 | 07/20/2026 | [Auction use cases](https://github.com/CallmeSen/Live-Auction/commit/240d2be) <br> [Auth API integration](https://github.com/CallmeSen/Live-Auction/commit/72a7322) <br> [CORS update](https://github.com/CallmeSen/Live-Auction/commit/c7011cb) <br> <https://000066.awsstudygroup.com/> |
| 2 | - Reviewed the Category and Auction Session APIs <br> - Checked the removal of mock data <br> - Followed the frontend service/interface refactor <br> - Studied lab **000133 - Building Serverless CRUD with Lambda and DynamoDB** | 07/22/2026 | 07/22/2026 | [Category API](https://github.com/CallmeSen/Live-Auction/commit/8e48e51) <br> [Frontend API services](https://github.com/CallmeSen/Live-Auction/commit/12f3627) <br> [Service/interface refactor](https://github.com/CallmeSen/Live-Auction/commit/81a7689) <br> <https://000133.awsstudygroup.com/> |
| 3 | - Defined dependencies for the shared backend package <br> - Built shared configuration, models, errors, and HTTP utilities <br> - Prepared shared primitives for auction services <br> - Studied lab **000037 - Infrastructure as Code with AWS CloudFormation** | 07/24/2026 | 07/24/2026 | [Commit 9893411](https://github.com/CallmeSen/Live-Auction/commit/9893411) <br> [Commit b34bcad](https://github.com/CallmeSen/Live-Auction/commit/b34bcad) <br> <https://000037.awsstudygroup.com/> |
| 4 | - Built the admin command handler <br> - Built the WebSocket authorization handler <br> - Built the catalog and auction session handlers <br> - Studied lab **000117 - Serverless Chat Application** | 07/25/2026 | 07/25/2026 | [Commit e2c11fd](https://github.com/CallmeSen/Live-Auction/commit/e2c11fd) <br> [Commit 33b84a3](https://github.com/CallmeSen/Live-Auction/commit/33b84a3) <br> <https://000117.awsstudygroup.com/> |
| 5 | - Built the bid processor and broadcast handlers <br> - Connected the realtime bidding flow <br> - Created deterministic Lambda build tooling <br> - Studied lab **000023 - Automated Deployments with AWS CodePipeline** | 07/26/2026 | 07/26/2026 | [Commit faedb64](https://github.com/CallmeSen/Live-Auction/commit/faedb64) <br> [Commit 72fa099](https://github.com/CallmeSen/Live-Auction/commit/72fa099) <br> <https://000023.awsstudygroup.com/> |

### Week 6 Achievements:

* Developed a clearer understanding of the place-bid, view-bids, and start-auction-session use cases, including how data moves through the related APIs.

* Learned how to separate shared packages from bounded-context Lambda services so shared logic remains centralized while each service keeps a clear responsibility.

* Built handlers for authorization, catalog, auction sessions, and realtime bidding, connecting the main backend processing flows of the Live Auction system.

* Learned how to create stable and reproducible Lambda artifacts, making artifact validation and deployment preparation more reliable.

---
