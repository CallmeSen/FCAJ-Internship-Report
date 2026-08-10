---
title: "Sharing and Feedback"
date: 2026-08-15
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

This section records my reflections on the First Cloud AI Journey internship and the Live-Auction project. I write these comments from the perspective of an intern who worked with a shared repository, received technical feedback, and gradually took on responsibilities across application code and AWS delivery.

### Overall Evaluation

**1. Working Environment**  
The working environment was open and practical. The project used GitHub as a shared workspace, so I could observe how frontend, backend, infrastructure, and documentation changes were connected. Working with real branches and integration points made the experience more realistic than completing isolated school assignments. At the same time, the shared repository required me to keep commits focused and communicate when a change affected another part of the system.

**2. Support from Mentor / Team Admin**  
Mentor and team guidance helped me understand the expected direction without removing the responsibility to investigate problems myself. Discussions about AWS architecture, authentication, serverless handlers, testing, and deployment gave me a clearer way to evaluate technical choices. The program administration also provided the schedule, workshops, and reporting structure needed to keep the internship on track.

**3. Relevance of Work to Academic Major**  
The Live-Auction project was closely related to my Information Technology major. I applied programming, database, software design, version control, and testing knowledge while learning cloud-specific concerns such as IAM boundaries, Lambda packaging, API integration, WebSocket communication, and infrastructure as code. This connection helped me understand how academic foundations are used in a production-oriented engineering process.

**4. Learning and Skill Development Opportunities**  
The project exposed me to the complete development cycle. I started with system design and CodeBuild preparation, then worked with shared backend primitives, auction and realtime handlers, frontend authentication and bidding workflows, infrastructure checks, and deterministic build artifacts. Writing tests for authorization, catalog behavior, bidding, broadcasts, and deployment contracts improved my ability to reason about expected behavior instead of relying only on manual testing.

**5. Company Culture and Team Spirit**  
The team encouraged members to share progress, ask questions, and review problems constructively. Frontend and backend work could not be completed independently because both sides depended on agreed interfaces. That dependency encouraged me to clarify assumptions, respect other contributors' changes, and focus discussions on the impact on users and the system rather than on individual ownership.

**6. Internship Policies and Benefits**  
The FCAJ structure provided a clear learning path through weekly worklogs, technical workshops, events, and a final project. These activities complemented the Live-Auction work: workshops strengthened my AWS foundation, while the project gave me a place to apply it. The combination of guided learning and practical delivery was the most valuable benefit of the internship.

---

### Additional Questions

**What did you find most satisfying during your internship?**  
The most satisfying part was seeing the project move from a collection of application features toward a system that could be checked through contracts, tests, and deployment validation. In particular, connecting authentication and auction workflows to realtime bidding services, then adding backend tests and reproducible Lambda build checks, showed me how small engineering improvements contribute to reliability.

**What should the program or team improve for future interns?**  
Future projects would benefit from publishing an initial API contract, environment checklist, and ownership map earlier. These references would reduce duplicated investigation when frontend and backend are developed in parallel. A regular integration checkpoint would also make it easier to identify mismatches before the final deployment period.

**Would you recommend this internship to a friend? Why?**  
Yes. I would recommend the program to students who are willing to learn independently and work collaboratively. It provides access to AWS concepts, real software delivery practices, technical mentoring, and a project where the results can be demonstrated through code, tests, and documentation. The experience is demanding, but that is also what makes the learning meaningful.

### Suggestions and Expectations

- Provide a small reference implementation and an agreed API contract at the beginning of each project, while still leaving room for interns to make design decisions.
- Schedule a short weekly integration review for frontend, backend, infrastructure, and testing representatives.
- Maintain a shared checklist for credentials, environment variables, deployment stages, test data, and cleanup of temporary AWS resources.
- Continue technical workshops on observability, security, cost control, and incident troubleshooting in addition to service introductions.
- Keep the weekly worklog and feedback process because it encouraged me to review both technical results and professional habits.

