---
title: "Blog 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# LIVE-AUCTION: XÂY DỰNG NỀN TẢNG ĐẤU GIÁ THỜI GIAN THỰC TRÊN AWS SERVERLESS

<figure style="text-align: center;">
    <a href="/FCAJ-Internship-Report/images/3-BlogPosted/high_availability_live_auction_aws_2026_v2.png">
        <img src="/FCAJ-Internship-Report/images/3-BlogPosted/high_availability_live_auction_aws_2026_v2.png" alt="Sơ đồ kiến trúc AWS serverless của Live-Auction" style="max-width: 100%; height: auto;">
    </a>
    <figcaption style="text-align: center;">Sơ đồ kiến trúc AWS serverless của hệ thống Live-Auction.</figcaption>
</figure>

Làm thế nào để một nền tảng đấu giá giữ được giá mới nhất khi có nhiều người cùng đặt giá trong gần như cùng một thời điểm? Đó là bài toán thực tế đứng sau dự án Live-Auction của nhóm mình.

Ban đầu, dự án là một web application với frontend React/Vite, backend FastAPI và database MySQL. Khi phân tích sâu hơn, nhóm nhận ra rằng hệ thống còn phải xử lý cập nhật thời gian thực, bid đồng thời, authentication, lưu hình ảnh, thay đổi trạng thái theo lịch và khả năng khôi phục khi có lỗi. Thử thách không chỉ là đưa code lên AWS, mà còn là quyết định phần nào cần xử lý đồng bộ và phần nào nên được tách thành các dịch vụ nhỏ theo hướng event-driven.

Demo hiện tại chưa đặt mục tiêu xử lý lưu lượng của một sàn đấu giá thương mại quy mô lớn. Việc ước lượng chính xác quy mô và chi phí vận hành trong giai đoạn đầu vẫn còn khó khăn, đồng thời phần FastAPI/MySQL được giữ lại để phục vụ phát triển local. Bù lại, kiến trúc serverless đã được triển khai và kiểm thử xoay quanh các use case đấu giá cụ thể, tạo tiền đề để nhóm tiếp tục mở rộng hệ thống.

## Bài toán của hệ thống đấu giá

Một auction platform không thể chỉ lưu bid cuối cùng vào database. Khi nhiều bidder gửi request cho cùng một item, hệ thống cần bảo đảm:

* Bid thấp hơn minimum increment bị từ chối.
* Hai bid đồng thời không ghi đè sai trạng thái của nhau.
* Request gửi lại không tạo thêm một giao dịch thứ hai.
* Kết quả accepted hoặc rejected được gửi đến những người đang theo dõi room.
* Các lỗi xử lý và thay đổi trạng thái vẫn có thể được truy nguyên.

## Kiến trúc serverless được áp dụng

### Frontend và phân phối nội dung

Ứng dụng React/Vite được build thành static asset và phân phối qua Amazon CloudFront từ các Amazon S3 bucket private. Bidder application và admin dashboard có artifact triển khai riêng. Hình ảnh sản phẩm được phân phối qua một media distribution riêng để lưu lượng file không cạnh tranh với request API.

### Authentication và phân quyền

Amazon Cognito User Pool xử lý đăng ký, xác nhận tài khoản, đăng nhập, khôi phục mật khẩu và refresh token. Cognito group tách quyền của user thông thường và administrator. Lambda post-confirmation hoàn tất bước khởi tạo user sau sign-up. REST và WebSocket đều kiểm tra Cognito JWT trước khi cho phép thực hiện operation được bảo vệ.

### Các Lambda service

REST API được kết nối với các handler chuyên biệt thay vì dồn toàn bộ nghiệp vụ vào một backend process lớn:

1. `session-service` quản lý auction session và session rule.
2. `item-service` quản lý item và cấp presigned URL để upload hình ảnh.
3. `query-service` phục vụ catalog, auction state và bid history.
4. `admin-command` xử lý moderation, scheduled transition và audit query.

## Luồng xử lý bid thời gian thực

1. Bidder kết nối tới API Gateway WebSocket và tham gia room của item.
2. `ws-authorizer` kiểm tra token; `ws-handler` lưu connection, room membership và bidder alias trong DynamoDB.
3. Khi bidder đặt giá, WebSocket handler kiểm tra context rồi gửi bid command vào Amazon SQS FIFO với message group theo từng item.
4. Lambda `bid-processor` kiểm tra session, minimum increment và thực hiện conditional update trên `item_auction_state`.
5. Processor ghi accepted hoặc rejected event cùng idempotency record để request gửi lặp lại không làm thay đổi kết quả.
6. Lambda `broadcast` đọc các connection còn hoạt động và gửi kết quả đến mọi người trong room thông qua API Gateway management API. Connection stale được xóa trong quá trình này.

## Tự động hóa và vận hành

Các mốc start, close và transition theo thời gian có thể được EventBridge Scheduler gọi đến `admin-command`. Scheduler dead-letter queue giúp giữ lại invocation thất bại để operator kiểm tra.

Các Terraform module provision identity, data, messaging, compute, API, edge, security, observability, backup và CI/CD theo đúng thứ tự phụ thuộc. CodeBuild đóng gói Lambda artifact deterministic cùng frontend asset; CodePipeline và CodeDeploy hỗ trợ promote một version có kiểm soát.

CloudWatch thu thập Lambda log và custom bid metric, đồng thời cảnh báo khi latency tăng, function lỗi, bid bị reject hoặc DLQ có message. CloudTrail, AWS Config, IAM Access Analyzer, audit storage có versioning và AWS Backup cung cấp bằng chứng vận hành cũng như cơ chế khôi phục.

## Một số lưu ý trong quá trình triển khai

* Serverless không có nghĩa là bỏ qua các quyết định về boundary, access pattern, retry behavior và permission policy.
* SQS FIFO chỉ bảo đảm thứ tự trong message group, vì vậy group cần được chọn phù hợp với item hoặc nghiệp vụ cần tuần tự hóa.
* Conditional write và idempotency phải được thiết kế cùng nhau để xử lý race condition và duplicate delivery.
* WebSocket connection có thể mất bất kỳ lúc nào, nên hệ thống cần TTL và cơ chế cleanup.
* Độ tin cậy phải được đánh giá cùng với khả năng quan sát, DLQ, audit và backup chứ không chỉ dựa vào việc Lambda có thể scale.

## Bài học rút ra

Bài học lớn nhất của nhóm là AWS cung cấp các building block, nhưng tính đúng đắn đến từ cách các building block được kết nối với nhau. Khi tách hệ thống thành các service độc lập, nhóm phải xác định rõ dữ liệu nào là nguồn sự thật, message nào cần giữ thứ tự, lỗi nào được retry và thao tác nào phải ghi audit.

Trong phạm vi hiện tại, Live-Auction đã cho thấy một workflow đấu giá thời gian thực có thể được tách thành các service dễ kiểm thử và triển khai lặp lại bằng Terraform. Những hướng phát triển tiếp theo gồm load test ở quy mô lớn hơn, diễn tập khôi phục đa vùng, bổ sung notification và phát triển analytics chuyên sâu.

Cảm ơn mọi người đã dành thời gian đọc bài chia sẻ về dự án của nhóm mình. Nhóm rất mong nhận được góp ý về bidding flow, ranh giới giữa các serverless service và những cách cải thiện độ tin cậy của nền tảng trong tương lai.

## Tài liệu tham khảo

* [Bài đăng gốc trên Facebook](https://www.facebook.com/share/p/14njRQp6aFU/)
* [Amazon API Gateway WebSocket APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/apigateway-websocket-api-overview.html)
* [Amazon SQS FIFO queues](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/FIFO-queues.html)
* [DynamoDB conditional writes](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.ConditionExpressions.html)
* [AWS Lambda documentation](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html)

