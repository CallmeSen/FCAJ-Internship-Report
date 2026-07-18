---
title: "Week 5 Worklog"
date: 2026-07-13
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Review authentication, the register API, and database migration.
* Follow the frontend interface development progress.
* Set up a smoke-test pipeline with AWS CodeBuild.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 1 | - Followed the register API and authentication flow <br> - Reviewed the database migration <br> - Checked the UI v2 changes <br> - Studied lab **000134 - Serverless Storage and Auth with AWS Amplify** and lab **000135 - Frontend Integration with API Gateway** | 07/13/2026 | 07/13/2026 | [Register API](https://github.com/CallmeSen/Live-Auction/commit/3c59d97) <br> [Database migration](https://github.com/CallmeSen/Live-Auction/commit/847aa0f) <br> [UI v2](https://github.com/CallmeSen/Live-Auction/commit/89656fd) <br> <https://000134.awsstudygroup.com/> <br> <https://000135.awsstudygroup.com/> |
| 2 | - Created `buildspec.yml` <br> - Configured the CodeBuild smoke test <br> - Checked dependency installation and backend test execution <br> - Studied lab **000152 - DevOps with AWS CodePipeline** | 07/18/2026 | 07/18/2026 | [Commit 24c5019](https://github.com/CallmeSen/Live-Auction/commit/24c5019) <br> [Commit c01509c](https://github.com/CallmeSen/Live-Auction/commit/c01509c) <br> <https://000152.awsstudygroup.com/> |

### Week 5 Achievements:

* Gained a clearer understanding of how authentication and the register API are organized, including how registration and authentication connect between the frontend and backend.

* Understood the role of database migration in backend development and why schema changes need to be tracked carefully to keep the data consistent.

* Created a CodeBuild smoke pipeline with buildspec.yml to verify dependency installation and backend tests, providing a repeatable check before deployment.

---
