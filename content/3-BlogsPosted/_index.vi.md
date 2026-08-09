---
title: "Các bài blog đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Phần này giới thiệu các bài viết kỹ thuật tôi đã chia sẻ trong [AWS Study Group VN](https://www.facebook.com/groups/awsstudygroupfcj). Nội dung được đúc kết từ quá trình học AWS và phát triển dự án Live-Auction, tập trung vào các vấn đề thực tế trong cloud engineering.

### [Blog 1 - Tối ưu chi phí lưu trữ trên Amazon S3](3.1-Blog1/)
Bài viết trình bày các S3 Storage Classes và S3 Lifecycle Policy, kèm một chiến lược lưu trữ thực tế cho application log, file người dùng tải lên và database backup.

### [Blog 2 - Lambda scale nhanh, nhưng database không scale theo cùng cách](3.2-Blog2/)
Bài viết phân tích áp lực database connection khi chuyển backend Live-Auction sang AWS Lambda và cách Amazon RDS Proxy có thể hỗ trợ bảo vệ Amazon RDS trong thời điểm traffic tăng cao.

### [Blog 3 - Xây dựng nền tảng đấu giá thời gian thực trên AWS Serverless](3.3-Blog3/)
Bài viết chia sẻ hành trình thiết kế Live-Auction với Cognito, API Gateway, Lambda, DynamoDB, SQS FIFO, WebSocket, Terraform và các dịch vụ giám sát AWS.
