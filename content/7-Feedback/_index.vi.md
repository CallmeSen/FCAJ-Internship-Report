---
title: "Chia sẻ và đóng góp ý kiến"
date: 2026-08-15
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

Phần này ghi lại cảm nhận của em về chương trình thực tập First Cloud AI Journey và dự án Live-Auction. Nội dung được viết từ góc nhìn của một thực tập sinh làm việc trong repository dùng chung, tiếp nhận feedback kỹ thuật và từng bước đảm nhận các công việc liên quan đến mã nguồn ứng dụng và triển khai AWS.

### Đánh giá chung

**1. Môi trường làm việc**  
Môi trường làm việc cởi mở và gắn với thực tế. Dự án sử dụng GitHub làm không gian làm việc chung nên em có thể quan sát mối liên hệ giữa các thay đổi ở frontend, backend, infrastructure và tài liệu. Việc làm việc với branch và các điểm tích hợp thực tế giúp trải nghiệm khác với những bài tập chỉ triển khai độc lập. Đồng thời, repository dùng chung yêu cầu em giữ commit rõ phạm vi và chủ động thông báo khi thay đổi có thể ảnh hưởng đến phần khác.

**2. Sự hỗ trợ từ mentor và ban tổ chức**  
Mentor và các thành viên hướng dẫn giúp em hiểu định hướng chung nhưng vẫn khuyến khích em tự tìm nguyên nhân và tự kiểm chứng giải pháp. Các trao đổi về AWS architecture, authentication, serverless handler, testing và deployment giúp em có cơ sở tốt hơn khi lựa chọn kỹ thuật. Ban tổ chức cũng cung cấp lịch học, workshop và yêu cầu báo cáo, nhờ đó quá trình thực tập có mốc theo dõi rõ ràng.

**3. Mức độ phù hợp với chuyên ngành**  
Dự án Live-Auction phù hợp với chuyên ngành Công nghệ thông tin của em. Em vận dụng kiến thức lập trình, cơ sở dữ liệu, thiết kế phần mềm, quản lý mã nguồn và kiểm thử, đồng thời học thêm các vấn đề đặc thù của cloud như IAM, đóng gói Lambda, tích hợp API, giao tiếp WebSocket và infrastructure as code. Sự kết hợp này giúp em hiểu rõ hơn cách kiến thức nền tảng được sử dụng trong một quy trình engineering hướng đến vận hành thực tế.

**4. Cơ hội học tập và phát triển kỹ năng**  
Dự án cho em trải nghiệm toàn bộ vòng đời phát triển. Em bắt đầu từ system design và chuẩn bị CodeBuild, sau đó làm việc với shared backend primitives, auction và realtime handler, các luồng authentication và bidding ở frontend, kiểm tra infrastructure và build artifact xác định. Việc viết test cho authorization, catalog, bidding, broadcast và deployment contract giúp em chuyển từ kiểm tra thủ công sang suy nghĩ dựa trên behavior mà hệ thống phải đảm bảo.

**5. Văn hóa công ty và tinh thần làm việc nhóm**  
Nhóm khuyến khích mọi người cập nhật tiến độ, đặt câu hỏi và cùng review vấn đề theo hướng xây dựng. Frontend và backend không thể hoàn thành tách rời vì phụ thuộc vào các interface đã thống nhất. Sự phụ thuộc này giúp em học cách làm rõ giả định, tôn trọng thay đổi của thành viên khác và tập trung trao đổi vào ảnh hưởng đối với người dùng cũng như toàn hệ thống.

**6. Chính sách và lợi ích của chương trình**  
Cấu trúc FCAJ tạo ra lộ trình học tập rõ ràng thông qua worklog hằng tuần, các workshop kỹ thuật, sự kiện và dự án tổng kết. Workshop củng cố nền tảng AWS, còn Live-Auction tạo môi trường để em áp dụng kiến thức đó vào sản phẩm. Sự kết hợp giữa học có hướng dẫn và triển khai thực tế là giá trị lớn nhất em nhận được trong kỳ thực tập.

---

### Các câu hỏi bổ sung

**Điều gì làm em hài lòng nhất trong kỳ thực tập?**  
Điều làm em hài lòng nhất là được chứng kiến dự án chuyển từ các chức năng riêng lẻ thành một hệ thống có thể kiểm chứng bằng contract, test và deployment validation. Việc kết nối authentication và auction workflow với realtime bidding, sau đó bổ sung backend test và kiểm tra build Lambda lặp lại, giúp em thấy rõ từng cải tiến nhỏ đều góp phần tăng độ tin cậy của hệ thống.

**Chương trình hoặc nhóm nên cải thiện điều gì cho các thực tập sinh sau?**  
Các dự án sau nên công bố sớm API contract ban đầu, checklist môi trường và sơ đồ phân công trách nhiệm. Những tài liệu này sẽ giảm thời gian mỗi thành viên phải tự điều tra cùng một vấn đề khi frontend và backend phát triển song song. Một buổi integration checkpoint ngắn theo tuần cũng giúp phát hiện mismatch sớm hơn trước giai đoạn deployment cuối.

**Em có giới thiệu chương trình này cho bạn bè không? Vì sao?**  
Có. Em sẽ giới thiệu chương trình cho những sinh viên sẵn sàng tự học và phối hợp trong nhóm. Chương trình cung cấp kiến thức AWS, quy trình phát triển phần mềm thực tế, sự hướng dẫn kỹ thuật và một dự án có thể chứng minh kết quả bằng code, test và tài liệu. Khối lượng công việc có thử thách, nhưng chính điều đó làm cho việc học trở nên có ý nghĩa.

### Đề xuất và kỳ vọng

- Cung cấp một reference implementation nhỏ, API contract thống nhất và sơ đồ interface ở đầu dự án, đồng thời vẫn để thực tập sinh chủ động đưa ra quyết định thiết kế.
- Tổ chức một buổi integration review ngắn hằng tuần với đại diện frontend, backend, infrastructure và testing.
- Duy trì checklist dùng chung về credential, biến môi trường, các stage triển khai, dữ liệu test và việc dọn dẹp tài nguyên AWS tạm thời.
- Tiếp tục các workshop về observability, security, cost control và xử lý sự cố bên cạnh các buổi giới thiệu dịch vụ.
- Duy trì worklog và quy trình feedback hằng tuần vì hoạt động này giúp em nhìn lại đồng thời kết quả kỹ thuật và tác phong làm việc.

