---
title: "Worklog Tuần 3"
date: 2026-06-29
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Phân tích yêu cầu và các thành phần chính của hệ thống Live Auction.
* Thiết kế kiến trúc AWS cho hệ thống, bao gồm high availability và realtime bidding.
* Tìm hiểu cách cấu hình CodeBuild để tự động kiểm tra backend.
* Ghi lại system design, sơ đồ kiến trúc và tài liệu hướng dẫn triển khai.

### Các công việc cần triển khai trong tuần này:

| Ngày | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 1 | - Phân tích yêu cầu và các bounded context của Live Auction <br> - Phác thảo AWS architecture <br> - Điều chỉnh cấu hình CodeBuild để chạy backend test <br> - Học lab **000017 - CI/CD Pipeline with AWS CodePipeline** | 29/06/2026 | 29/06/2026 | [Commit 40f8559](https://github.com/CallmeSen/Live-Auction/commit/40f8559) <br> <https://000017.awsstudygroup.com/> |
| 2 | - Hoàn thiện sơ đồ **Complete AWS System Design** <br> - Mô tả **Realtime Bid Flow** <br> - Thiết kế **Data Model and State Machine** cho auction session <br> - Học lab **000101 - Building Highly Available Web Applications** | 03/07/2026 | 03/07/2026 | <https://000101.awsstudygroup.com/> |
| 3 | - Ghi tài liệu system design và kiến trúc high availability <br> - Viết runbook setup/deployment cho Live Auction <br> - Rà soát các giả định về security, networking và vận hành <br> - Học lab **000102 - Infrastructure as Code Workshop Series** và lab **000008 - Monitoring with Amazon CloudWatch** | 04/07/2026 | 04/07/2026 | <https://000102.awsstudygroup.com/> <br> <https://000008.awsstudygroup.com/> |

### Kết quả đạt được tuần 3:

* Sau khi phân tích yêu cầu, xác định rõ hơn trách nhiệm của từng bounded context và luồng xử lý chính từ lúc tạo auction session đến khi cập nhật giá theo thời gian thực.

* Hoàn thiện bộ sơ đồ AWS architecture, realtime bid flow và data model/state machine, tạo cơ sở thống nhất để trao đổi về cách hệ thống vận hành.

* Cấu hình được CodeBuild để cài đặt dependency và chạy backend unit test, giúp phát hiện sớm các lỗi liên quan đến môi trường build và mã nguồn.

* Ghi lại tài liệu system design và runbook setup/deployment, đồng thời lưu ý các giả định về security, networking và vận hành cho các bước triển khai tiếp theo.

---
