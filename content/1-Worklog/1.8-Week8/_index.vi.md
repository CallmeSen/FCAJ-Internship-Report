---
title: "Worklog Tuần 8"
date: 2026-08-03
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Kiểm tra và điều chỉnh identity/integration deployment trên AWS.
* Hoàn thiện authentication, chat và realtime flow trên frontend.
* Đồng bộ backend handlers với test contracts và build process.
* Chuyển các auction pages sang serverless catalog API.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 1 | - Điều chỉnh Cognito identity và integration deployment checks <br> - Hoàn thiện auth/account operations và confirm sign-up flow <br> - Cải thiện auction chat và realtime UI flow <br> - Học lab **000082 - Custom Domains and SSL for Serverless Applications** và lab **000008 - Monitoring with Amazon CloudWatch** | 03/08/2026 | 03/08/2026 | [Infrastructure checks](https://github.com/CallmeSen/Live-Auction/commit/c81d401) <br> [Auth, chat, and realtime flows](https://github.com/CallmeSen/Live-Auction/commit/13da054) <br> <https://000082.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |
| 2 | - Đồng bộ backend handlers và build test contracts <br> - Chuyển auction pages sang serverless catalog API <br> - Cập nhật README, git configuration và AWS deployment guidance <br> - Học lab **000136 - Document Management System Deployment with AWS SAM** và lab **000130 - Edge Computing with CloudFront and Lambda@Edge** | 04/08/2026 | 04/08/2026 | [Backend contracts](https://github.com/CallmeSen/Live-Auction/commit/51132ee) <br> [Serverless catalog migration](https://github.com/CallmeSen/Live-Auction/commit/161a72a) <br> [AWS deployment guidance](https://github.com/CallmeSen/Live-Auction/commit/cd99e0d) <br> <https://000136.awsstudygroup.com/> <br> <https://000130.awsstudygroup.com/> |

### Kết quả đạt được tuần 8:

* Hiểu và điều chỉnh được các bước kiểm tra identity và integration deployment, qua đó xác định rõ hơn các điều kiện cần kiểm tra trước khi đưa thay đổi lên môi trường triển khai.

* Hoàn thiện thêm authentication, account, chat và realtime flow, đồng thời kiểm tra sự liên kết giữa các thao tác người dùng và phản hồi từ backend.

* Đồng bộ backend handlers với build/test contracts để hành vi của handler, bước build và các bài test sử dụng cùng một kỳ vọng rõ ràng hơn.

* Kết nối auction pages với serverless catalog API, đồng thời cập nhật README, git configuration và tài liệu deployment để việc chạy project và tiếp tục triển khai thuận tiện hơn.

---
