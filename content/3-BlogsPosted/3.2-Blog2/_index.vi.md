---
title: "Blog 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# LAMBDA SCALE NHANH, NHƯNG DATABASE KHÔNG SCALE THEO CÙNG CÁCH

Trong quá trình làm dự án Live-Auction, nhóm bắt đầu chuyển dần các chức năng backend từ FastAPI sang AWS Lambda, trong khi database vẫn là MySQL trên Amazon RDS. Sự thay đổi kiến trúc này khiến nhóm phải xem lại một vấn đề vận hành quan trọng: database connection.

## Mô hình connection thay đổi khi dùng serverless

Với backend chạy lâu dài trên EC2 hoặc container, mô hình connection thường khá dễ kiểm soát:

`Application -> Connection Pool -> MySQL`

Application duy trì connection pool với giới hạn tương đối ổn định và tái sử dụng connection giữa các request. Khi chuyển sang Lambda, giả định này thay đổi. Lambda có thể tạo thêm execution environment khi số request đồng thời tăng, trong khi Amazon RDS vẫn có giới hạn về số connection, CPU và RAM.

Lambda có thể scale theo workload, nhưng các dependency phía sau không nhất thiết có cùng khả năng throughput. Reserved concurrency có thể được dùng để giới hạn function, từ đó tránh làm quá tải các resource phía sau như database.

## Vì sao điều này quan trọng với hệ thống Auction

Hãy giả sử lượng request tăng nhanh khi phiên đấu giá sắp kết thúc. Tại một thời điểm, 500 request đồng thời có thể cần đến tối đa 500 Lambda execution đồng thời. Nếu mỗi execution tạo một database connection mới, Amazon RDS có thể phải xử lý một lượng connection tăng đột ngột.

Lambda vẫn có thể scale, nhưng database có thể bắt đầu gặp:

* connection exhaustion;
* thời gian tạo connection tăng;
* query latency cao hơn;
* transaction chậm;
* request timeout; và
* ảnh hưởng đến các workload khác dùng chung database.

Với một nền tảng đấu giá, thời điểm cuối phiên lại chính là lúc bid traffic có khả năng tăng cao nhất. Vì vậy, database connection management cần được xem là một phần của serverless design, thay vì một việc xử lý bổ sung sau này.

## Amazon RDS Proxy hỗ trợ như thế nào

Amazon RDS Proxy là managed proxy của AWS, duy trì một pool database connection. Thay vì để từng Lambda execution environment mở và quản lý connection trực tiếp tới RDS, application kết nối thông qua proxy:

`Lambda -> Amazon RDS Proxy -> Amazon RDS`

Proxy có thể tái sử dụng và pool database connection, từ đó giảm áp lực lên database khi có nhiều Lambda execution ngắn hạn xuất hiện đồng thời. RDS Proxy cũng có thể cải thiện khả năng phục hồi của application trong quá trình database failover.

RDS Proxy không thay thế cho query optimization, transaction design hay concurrency limit hợp lý. Đây là một thành phần trong thiết kế tổng thể, nơi cả Lambda và database phụ thuộc phía sau đều được đánh giá.

## Bài học rút ra từ dự án

Khi đánh giá serverless scaling, không thể chỉ nhìn vào Lambda. Cần xem xét capacity, connection limit và failure mode của mọi downstream dependency. Với Live-Auction, điều đó có nghĩa là phải thiết kế cẩn thận đường kết nối từ Lambda tới RDS để traffic bidding tăng cao không tạo thêm áp lực có thể tránh được cho MySQL.

## Tài liệu tham khảo

* [Bài đăng gốc trên AWS Study Group VN](https://www.facebook.com/share/p/1GhthtrrpB/)
* [Hành vi scale của AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html)
* [Sử dụng Amazon RDS Proxy với AWS Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-rds-proxy.html)
* [Khái niệm Amazon RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html)
