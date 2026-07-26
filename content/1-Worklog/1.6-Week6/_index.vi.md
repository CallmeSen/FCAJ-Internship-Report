---
title: "Worklog Tuần 6"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Hiểu các use case chính của hệ thống đấu giá.
* Tích hợp các API category, auction session và authentication.
* Xây dựng backend serverless cho catalog, session và realtime bidding.
* Chuẩn hóa quy trình đóng gói Lambda.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 1 | - Rà soát use case đặt giá, xem lịch sử trả giá và bắt đầu auction session <br> - Kiểm tra CORS và auth API <br> - Theo dõi việc loại bỏ frontend deployment cũ <br> - Học lab **000066 - Building Serverless APIs** | 20/07/2026 | 20/07/2026 | [Auction use cases](https://github.com/CallmeSen/Live-Auction/commit/240d2be) <br> [Auth API integration](https://github.com/CallmeSen/Live-Auction/commit/72a7322) <br> [CORS update](https://github.com/CallmeSen/Live-Auction/commit/c7011cb) <br> <https://000066.awsstudygroup.com/> |
| 2 | - Rà soát Category/Auction Session API <br> - Kiểm tra việc bỏ mock data <br> - Theo dõi refactor frontend service/interface <br> - Học lab **000133 - Building Serverless CRUD with Lambda and DynamoDB** | 22/07/2026 | 22/07/2026 | [Category API](https://github.com/CallmeSen/Live-Auction/commit/8e48e51) <br> [Frontend API services](https://github.com/CallmeSen/Live-Auction/commit/12f3627) <br> [Service/interface refactor](https://github.com/CallmeSen/Live-Auction/commit/81a7689) <br> <https://000133.awsstudygroup.com/> |
| 3 | - Khai báo dependency cho shared backend package <br> - Xây dựng shared configuration, models, errors và HTTP utilities <br> - Chuẩn bị primitives dùng chung cho auction services <br> - Học lab **000037 - Infrastructure as Code with AWS CloudFormation** | 24/07/2026 | 24/07/2026 | [Commit 9893411](https://github.com/CallmeSen/Live-Auction/commit/9893411) <br> [Commit b34bcad](https://github.com/CallmeSen/Live-Auction/commit/b34bcad) <br> <https://000037.awsstudygroup.com/> |
| 4 | - Xây dựng admin command handler <br> - Xây dựng WebSocket authorization handler <br> - Xây dựng catalog và auction session handlers <br> - Học lab **000117 - Serverless Chat Application** | 25/07/2026 | 25/07/2026 | [Commit e2c11fd](https://github.com/CallmeSen/Live-Auction/commit/e2c11fd) <br> [Commit 33b84a3](https://github.com/CallmeSen/Live-Auction/commit/33b84a3) <br> <https://000117.awsstudygroup.com/> |
| 5 | - Xây dựng bid processor và broadcast handlers <br> - Kết nối luồng realtime bidding <br> - Tạo deterministic Lambda build tooling <br> - Học lab **000023 - Automated Deployments with AWS CodePipeline** | 26/07/2026 | 26/07/2026 | [Commit faedb64](https://github.com/CallmeSen/Live-Auction/commit/faedb64) <br> [Commit 72fa099](https://github.com/CallmeSen/Live-Auction/commit/72fa099) <br> <https://000023.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:

* Hiểu rõ hơn các use case đặt giá, xem lịch sử trả giá và bắt đầu auction session, đồng thời theo dõi cách dữ liệu đi qua các API liên quan.

* Nắm được cách tách shared package và các bounded-context Lambda service để phần dùng chung được quản lý tập trung mà từng service vẫn giữ được phạm vi rõ ràng.

* Xây dựng được các handler cho authorization, catalog, auction session và realtime bidding, kết nối được các luồng xử lý backend quan trọng của Live Auction.

* Biết cách tạo Lambda artifact có kết quả ổn định và có thể tái lập, giúp việc kiểm tra artifact và chuẩn bị triển khai đáng tin cậy hơn.

---
