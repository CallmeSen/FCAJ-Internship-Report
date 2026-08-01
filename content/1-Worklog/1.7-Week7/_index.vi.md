---
title: "Worklog Tuần 7"
date: 2026-07-27
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Xây dựng và kiểm tra các thành phần infrastructure cho Live Auction.
* Hoàn thiện authentication, auction workflow và realtime frontend.
* Mở rộng backend unit test và kiểm tra build artifact.
* Tham dự sự kiện AWS FCAJ Agent Forge - Deepdive.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 1 | - Bổ sung AWS infrastructure và integration test scripts <br> - Cấu hình frontend runtime/test tooling <br> - Viết unit test cho shared auction utilities <br> - Học lab **000140 - Distributed Tracing with X-Ray and CloudWatch** | 27/07/2026 | 27/07/2026 | [Infrastructure](https://github.com/CallmeSen/Live-Auction/commit/eb8306b) <br> [Frontend tooling](https://github.com/CallmeSen/Live-Auction/commit/5513c30) <br> [Backend utility tests](https://github.com/CallmeSen/Live-Auction/commit/caabe8b) <br> <https://000140.awsstudygroup.com/> |
| 2 | - Xây dựng authentication provider và Cognito operations <br> - Hoàn thiện auction room, bid panel và auction pages <br> - Bổ sung test cho admin command và authorization <br> - Học lab **000141 - Cross-Domain Authentication with Amazon Cognito** | 28/07/2026 | 28/07/2026 | [Authentication and auction workflows](https://github.com/CallmeSen/Live-Auction/commit/81665b3) <br> [Authorization tests](https://github.com/CallmeSen/Live-Auction/commit/7569815) <br> <https://000141.awsstudygroup.com/> |
| 3 | - Kết nối realtime bidding và serverless catalog services <br> - Xây dựng WebSocket protocol/client adapters <br> - Bổ sung test cho auction và realtime handlers <br> - Học lab **000078 - Serverless Backend with Lambda, S3, and DynamoDB** | 29/07/2026 | 29/07/2026 | [Realtime and serverless services](https://github.com/CallmeSen/Live-Auction/commit/d94254c) <br> [Auction/realtime tests](https://github.com/CallmeSen/Live-Auction/commit/99893b9) <br> <https://000078.awsstudygroup.com/> |
| 4 | - Kiểm tra deterministic zip và Lambda build artifacts <br> - Cập nhật test configuration để xác nhận artifact reproducibility <br> - Học lab **000022 - Serverless Automation with AWS Lambda** | 30/07/2026 | 30/07/2026 | [Build artifact tests](https://github.com/CallmeSen/Live-Auction/commit/2f9d917) <br> <https://000022.awsstudygroup.com/> |
| 5 | - Tham dự AWS FCAJ Agent Forge - Deepdive <br> - Học về Agentic AI architecture, prompt, tools, context và action <br> - Thực hành xây dựng và kiểm thử agent workflow trên AWS | 01/08/2026 | 01/08/2026 | [Bài thu hoạch Event 3](../../4-EventParticipated/4.3-Event3/) <br> [AWS FCAJ Agent Forge - Deepdive](https://www.youtube.com/live/F58sam40jxk) <br> [AgentForge workshop](http://agentforge-hcmc-workshop-p371s08u.s3-website-ap-southeast-1.amazonaws.com/00-Overview/00-Dashboard-Overview.html) |

### Kết quả đạt được tuần 7:

* Xây dựng được nền tảng infrastructure và runtime/test tooling cho frontend và backend, giúp các bước chạy thử và kiểm tra có cấu hình nhất quán hơn.

* Hoàn thiện các luồng authentication, auction room, bidding và serverless service integration, từ đó kết nối rõ hơn trải nghiệm người dùng với các service phía sau.

* Mở rộng backend test coverage cho utilities, authorization, auction handlers và realtime handlers, giúp kiểm tra được nhiều tình huống hơn khi tiếp tục thay đổi hệ thống.

* Biết cách kiểm tra tính reproducible của Lambda build artifacts và hiểu được vì sao artifact có thể tái lập là điều quan trọng đối với quy trình triển khai serverless.

* Hiểu thêm về kiến trúc Agentic AI và quy trình xây dựng agent workflow trên AWS.

---
