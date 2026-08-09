---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# TỐI ƯU CHI PHÍ LƯU TRỮ TRÊN AMAZON S3: STORAGE CLASSES VÀ LIFECYCLE POLICY

Khi mới học AWS, tôi từng nghĩ Amazon S3 đơn giản là nơi upload file lên và tải xuống khi cần. Trên thực tế, S3 còn cung cấp mô hình lưu trữ theo tầng, giúp giảm đáng kể chi phí vận hành khi lựa chọn storage class phù hợp với vòng đời dữ liệu.

Bài viết này giới thiệu hai tính năng hữu ích cho mục tiêu đó: **S3 Storage Classes** và **S3 Lifecycle Policy**.

## Vấn đề: không phải file nào cũng quan trọng như nhau theo thời gian

Hãy hình dung một S3 bucket lưu application log, ảnh do người dùng tải lên và file backup database:

* Log trong tuần thường được truy cập để debug.
* Log của tháng trước chỉ được xem lại khi cần.
* Log từ sáu tháng trước hầu như không được dùng, nhưng vẫn phải lưu để đáp ứng yêu cầu audit.

Nếu tất cả object luôn nằm trong S3 Standard, chi phí sẽ được tính theo mức hot storage cao nhất ngay cả khi phần lớn dữ liệu không còn được truy cập thường xuyên. Vì vậy, hiểu vòng đời dữ liệu là một phần quan trọng trong việc kiểm soát chi phí cloud.

## Các S3 Storage Class chính

1. **S3 Standard** phù hợp với dữ liệu được truy cập thường xuyên và cần độ trễ thấp, ví dụ website assets hoặc dữ liệu của application đang hoạt động.
2. **S3 Standard-Infrequent Access (Standard-IA)** vẫn cho phép truy cập nhanh nhưng có chi phí lưu trữ thấp hơn. Storage class này phù hợp với backup và disaster recovery, tuy nhiên có retrieval fee khi lấy dữ liệu.
3. **S3 One Zone-IA** chỉ lưu dữ liệu trong một Availability Zone. Chi phí thấp hơn Standard-IA nhưng chỉ nên dùng cho dữ liệu có thể tái tạo ở nơi khác.
4. **S3 Glacier Instant Retrieval** phù hợp với dữ liệu ít sử dụng nhưng vẫn cần lấy gần như tức thì, chẳng hạn ảnh y tế hoặc dữ liệu media.
5. **S3 Glacier Flexible Retrieval** có chi phí thấp hơn với thời gian lấy dữ liệu từ vài phút đến vài giờ, phù hợp cho backup định kỳ.
6. **S3 Glacier Deep Archive** là lựa chọn có chi phí thấp nhất cho dữ liệu lưu trữ dài hạn, hiếm khi truy cập và có thể chấp nhận thời gian lấy dữ liệu đến mười hai giờ.

## Tự động hóa bằng Lifecycle Policy

Không cần chuyển từng file thủ công giữa các storage class. S3 Lifecycle Policy cho phép tự động transition object theo thời gian, prefix hoặc tag.

Một lifecycle rule thực tế có thể là:

* Ngày 0-30: giữ object ở S3 Standard để phục vụ truy cập thường xuyên.
* Ngày 30-90: tự động chuyển sang S3 Standard-IA.
* Ngày 90-180: tự động chuyển sang S3 Glacier Flexible Retrieval.
* Sau 365 ngày: chuyển sang S3 Glacier Deep Archive.
* Sau bảy năm: hết hạn và xóa theo yêu cầu lưu trữ.

Toàn bộ quy trình này có thể cấu hình một lần trong S3 Console hoặc khai báo bằng Infrastructure as Code như Terraform và CloudFormation. Không cần cron job hay Lambda function riêng cho việc chuyển lớp lưu trữ.

## Một số lưu ý

* Mỗi lần transition có request cost, do đó không nên chuyển các object nhỏ quá thường xuyên.
* Object dưới 128 KB có thể không hưởng lợi từ việc chuyển sang IA hoặc Glacier vì kích thước tối thiểu được tính phí.
* Standard-IA và các Glacier class có thời gian lưu trữ tối thiểu. Xóa object sớm hơn vẫn có thể phát sinh chi phí.
* Lifecycle rule có thể áp dụng theo prefix hoặc tag, vì vậy có thể tách retention policy cho `logs/` và `backups/` trong cùng một bucket.

Amazon S3 không chỉ là nơi chứa file. Khi xem S3 như một hệ thống lưu trữ theo tầng và thiết kế theo đúng vòng đời dữ liệu, có thể giảm được một khoản chi phí vận hành đáng kể ngay cả trước khi tối ưu code của application.

## Tài liệu tham khảo

* [Bài đăng gốc trên AWS Study Group VN](https://www.facebook.com/share/p/14k93SJMxK5/)
* [Tổng quan về Amazon S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
* [Quản lý vòng đời object với S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)
* [Các thành phần cấu hình S3 Lifecycle](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intro-lifecycle-rules.html)
* [Bảng giá Amazon S3](https://aws.amazon.com/s3/pricing/)
