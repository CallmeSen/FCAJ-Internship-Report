---
title: "Worklog Tuần 5"
date: 2026-07-13
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Rà soát authentication, register API và database migration.
* Theo dõi sự phát triển của giao diện frontend.
* Thiết lập pipeline smoke test bằng AWS CodeBuild.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 1 | - Theo dõi register API và authentication flow <br> - Rà soát database migration <br> - Kiểm tra các thay đổi UI v2 <br> - Học lab **000134 - Serverless Storage and Auth with AWS Amplify** và lab **000135 - Frontend Integration with API Gateway** | 13/07/2026 | 13/07/2026 | [Register API](https://github.com/CallmeSen/Live-Auction/commit/3c59d97) <br> [Database migration](https://github.com/CallmeSen/Live-Auction/commit/847aa0f) <br> [UI v2](https://github.com/CallmeSen/Live-Auction/commit/89656fd) <br> <https://000134.awsstudygroup.com/> <br> <https://000135.awsstudygroup.com/> |
| 2 | - Tạo file `buildspec.yml` <br> - Cấu hình CodeBuild smoke test <br> - Kiểm tra bước cài dependency và chạy backend test <br> - Học lab **000152 - DevOps with AWS CodePipeline** | 18/07/2026 | 18/07/2026 | [Commit 24c5019](https://github.com/CallmeSen/Live-Auction/commit/24c5019) <br> [Commit c01509c](https://github.com/CallmeSen/Live-Auction/commit/c01509c) <br> <https://000152.awsstudygroup.com/> |

### Kết quả đạt được tuần 5:

* Hiểu rõ hơn cách authentication và register API được tổ chức trong project, cũng như cách các bước đăng ký và xác thực liên kết với nhau giữa frontend và backend.

* Nắm được vai trò của database migration trong quá trình phát triển backend và hiểu việc thay đổi schema cần được theo dõi để giữ dữ liệu nhất quán.

* Tạo được CodeBuild smoke pipeline với buildspec.yml để kiểm tra cài dependency và chạy backend test, qua đó có một bước kiểm tra lặp lại được trước khi triển khai.

---
