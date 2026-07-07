---
title: "Đề xuất"
date: 2026-07-13
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# NỀN TẢNG ĐẤU GIÁ TRỰC TUYẾN LIVE AUCTION TRÊN AWS

## Nền tảng đấu giá thời gian thực theo kiến trúc serverless cho người mua, người bán và quản trị viên

### 1. Tóm tắt đề xuất

Live-Auction là nền tảng đấu giá trực tuyến cho phép xem sản phẩm, tạo phiên đấu giá, đặt giá và nhận cập nhật giá theo thời gian thực. Repo có phần FastAPI/MySQL phục vụ phát triển local và đường triển khai serverless trên AWS được thực hiện bằng Terraform cùng các Lambda handler.

Kiến trúc AWS sử dụng các ứng dụng React/Vite được phân phối qua Amazon CloudFront và private Amazon S3 bucket. Amazon Cognito quản lý authentication và hai group `USER`/`ADMIN`. Amazon API Gateway cung cấp REST API và WebSocket API. AWS Lambda xử lý session, item, query, admin, WebSocket, bid processor và broadcast. Amazon DynamoDB lưu catalog, current auction state, bid event, WebSocket connection, idempotency record và audit event.

Mục tiêu chính là xử lý đúng các bid đồng thời. Bid command được sắp xếp qua Amazon SQS FIFO, Lambda processor kiểm tra và cập nhật bằng conditional write trên DynamoDB, sau đó broadcast kết quả đến các client đang kết nối. EventBridge Scheduler xử lý transition theo thời gian; CloudWatch, CloudTrail, AWS Config, IAM Access Analyzer và AWS Backup hỗ trợ vận hành và khôi phục.

### 2. Vấn đề và mục tiêu

Hệ thống đấu giá phải duy trì một mức giá nhất quán khi nhiều người gửi request gần như cùng lúc. Hệ thống cần từ chối bid thấp hơn minimum increment, không áp dụng duplicate request nhiều lần, lưu audit trail và cập nhật cho người dùng mà không cần refresh trang.

Mục tiêu của dự án gồm:

- cung cấp workflow cho bidder, seller và administrator;
- hỗ trợ Cognito đăng ký, xác nhận, đăng nhập và phân quyền;
- quản lý session, category, item, presigned image upload và bid history;
- cung cấp WebSocket room và kết quả bid thời gian thực;
- triển khai lặp lại bằng Terraform và phân phối artifact qua CodeBuild/CodePipeline; và
- bổ sung monitoring, security evidence, dead-letter queue và backup.

### 3. Kiến trúc AWS

Sơ đồ dưới đây là kiến trúc tham chiếu cho đường triển khai Live-Auction trên AWS. Nhấn vào sơ đồ để xem kích thước đầy đủ.

[![Sơ đồ kiến trúc AWS serverless của Live-Auction](/FCAJ-Internship-Report/images/2-Proposal/image.png?v=20260809)](/FCAJ-Internship-Report/images/2-Proposal/image.png?v=20260809)

#### Client và edge

Các ứng dụng React/Vite dành cho bidder, seller và admin được build thành static asset. CloudFront phân phối frontend từ S3 origin private bằng Origin Access Control. Một media distribution riêng phân phối hình ảnh sản phẩm từ media bucket đã mã hóa.

#### Identity và API

Cognito User Pool xử lý các luồng tài khoản và group. Lambda post-confirmation hoàn tất bước khởi tạo user. REST API Gateway chuyển request đã xác thực đến `session-service`, `item-service`, `query-service` và `admin-command`. WebSocket API sử dụng Lambda authorizer, `ws-handler` và các route `$connect`, `$disconnect`, `joinRoom`, `placeBid`.

#### Data và bid processing

Các bảng DynamoDB được tách theo access pattern: `auction_catalog`, `category_catalog`, `item_auction_state`, `bid_events`, `websocket_connections`, `item_bidder_aliases`, `idempotency` và `admin_audit_events`. Item service cấp presigned URL để trình duyệt upload media trực tiếp lên S3.

Luồng xử lý bid:

1. Bidder kết nối và tham gia room của item.
2. `ws-handler` kiểm tra context rồi gửi command vào SQS FIFO bid queue.
3. `bid-processor` kiểm tra session, minimum increment và thực hiện conditional state update.
4. Processor ghi accepted/rejected event cùng idempotency record.
5. `broadcast` gửi kết quả đến các connection còn hoạt động thông qua API Gateway management API.

EventBridge Scheduler gọi `admin-command` để thực hiện transition theo lịch. Bid queue và scheduler queue đều có DLQ để giữ lại message lỗi cho việc kiểm tra.

### 4. Hạ tầng và CI/CD

Các Terraform module được triển khai theo thứ tự phụ thuộc: remote state, foundation, identity, data, messaging, compute, API, edge, observability, security, backup và CI/CD. Remote state được lưu trong S3 với DynamoDB lock table.

CodeBuild tạo Lambda package deterministic và frontend asset. CodePipeline lưu artifact có version và encryption, sau đó CodeDeploy promote Lambda version được chọn. CloudWatch thu thập log, custom metric và cảnh báo bid latency, Lambda error, rejected bid và DLQ. CloudTrail, AWS Config, IAM Access Analyzer và AWS Backup cung cấp audit và recovery control.

### 5. Bảo mật và độ tin cậy

- Xác thực Cognito JWT và kiểm tra group cho các operation được bảo vệ.
- Sử dụng IAM least privilege và không đưa secret vào source control.
- Giữ S3 bucket private, phân phối media qua CloudFront Origin Access Control.
- Kết hợp FIFO message group, conditional DynamoDB write, idempotency record và retry có giới hạn.
- Theo dõi WebSocket connection stale, function error, latency và DLQ.
- Lưu admin audit event và kiểm tra quy trình backup/restore theo phạm vi giới hạn.

Serverless stack hiện tại không provision EC2, RDS, Aurora, RDS Proxy, ECS, ALB, VPC hay Kinesis. Đây là các hướng có thể nghiên cứu sau, không phải thành phần đang triển khai trong đề xuất này.

### 6. Kết quả kỳ vọng

Hệ thống hoàn chỉnh dự kiến cung cấp trải nghiệm đấu giá trên trình duyệt với Cognito authentication, workflow cho seller và administrator, quản lý catalog/media, auction room thời gian thực, bid processing theo thứ tự, bid history, audit event, cảnh báo vận hành và quy trình triển khai Terraform/CI/CD có thể lặp lại.
