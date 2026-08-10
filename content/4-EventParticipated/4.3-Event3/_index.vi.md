---
title: "Event 3"
date: 2026-08-03
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch "AWS FCAJ Agent Forge - Deepdive"

### Tổng Quan Sự Kiện

- **Tên sự kiện:** AWS FCAJ Agent Forge - Deepdive
- **Hình thức:** Buổi học chuyên sâu online (lý thuyết + hands-on lab)
- **Thời gian tham dự:** Thứ Bảy, 01/08/2026, khoảng 09:02–10:24 (UTC+7)
- **Nguồn phần lý thuyết:** [AWS FCAJ Agent Forge - Deepdive - YouTube](https://www.youtube.com/live/F58sam40jxk)
- **Nguồn phần thực hành:** [AgentForge - Ho Chi Min City](http://agentforge-hcmc-workshop-p371s08u.s3-website-ap-southeast-1.amazonaws.com/00-Overview/00-Dashboard-Overview.html)
- **Link đăng ký / check-in:** [AWS FCAJ Agent Forge - Deepdive trên Luma](https://luma.com/e/ticket/evt-O188dSz2Z4ahLAI?pk=g-NXbyLXvN9u2HPvc)
- **Trọng tâm:** Kiến trúc Agentic AI, tích hợp dịch vụ AWS và quy trình triển khai thực tế

### Diễn giả

- **Nghĩa Trần** - Agentic SA
- **Anh Phạm** - Cloud Consultant, G-AsiaPacific Vietnam

### Mục Đích Của Sự Kiện

- Hiểu các khái niệm cốt lõi của **hệ thống AI agent** trên AWS
- Nắm cách thiết kế workflow agent từ prompt đến sử dụng công cụ
- Kết nối lý thuyết với thực hành thông qua bài lab từng bước
- Củng cố kỹ năng triển khai, kiểm thử và cải tiến agent
- Tăng mức sẵn sàng áp dụng AI agent vào công việc thực tập và project sau này

### Nội Dung Nổi Bật

#### Lý thuyết: Tư duy và kiến trúc Agentic AI

- Buổi học nhấn mạnh rằng AI agent không chỉ là chatbot, mà là workflow gồm suy luận, công cụ, ngữ cảnh và hành động
- Một kiến trúc tốt cần tách rõ các lớp: instruction layer, orchestration flow, tích hợp data/tool và kiểm tra output
- Prompt cần được thiết kế có cấu trúc, rõ ràng và hướng mục tiêu để giảm mơ hồ khi thực thi
- Retrieval, grounding và quản lý ngữ cảnh là yếu tố quan trọng để tăng độ liên quan và độ tin cậy của phản hồi

#### Lý thuyết: Độ tin cậy, bảo mật và vận hành

- Xây dựng AI agent cần chú trọng tính ổn định, không chỉ chất lượng model
- Sự kiện đề cập các điểm thực tế như kiểm soát truy cập, an toàn dữ liệu và ranh giới quyền hạn
- Logging, observability và vòng lặp đánh giá là cần thiết để theo dõi hành vi agent và cải thiện chất lượng theo thời gian
- Việc dùng AI có trách nhiệm cần khả năng truy vết và guardrail rõ ràng cho các thao tác không an toàn hoặc ngoài phạm vi

#### Hands-on Lab: Xây và chạy workflow agent

- Phần lab chuyển hóa lý thuyết thành các bước triển khai cụ thể, từ setup đến chạy thử
- Các hoạt động thực hành tập trung vào tạo và cấu hình luồng agent, kết nối tài nguyên cần thiết và chạy các kịch bản test
- Quy trình thể hiện rõ cách lặp cải tiến: chạy -> quan sát output -> chỉnh prompt/cấu hình -> chạy lại
- Lab củng cố rằng chất lượng thực tế đến từ kiểm chứng lặp lại, không phải thiết lập một lần

### Những Gì Học Được

#### Kiến Thức Kỹ Thuật

- Hệ thống agent cần được thiết kế theo **workflow end-to-end**, không phải các prompt rời rạc
- Chất lượng prompt ảnh hưởng trực tiếp đến tính nhất quán, khả năng hành động và độ an toàn của output
- Tích hợp công cụ phải rõ ràng, có kiểm soát và bám sát phạm vi bài toán
- Đánh giá cần cả kiểm tra chức năng (đúng/sai) và kiểm tra vận hành (ổn định/an toàn)

#### Tư Duy Kỹ Sư

- Bắt đầu từ yêu cầu và hành vi mong đợi trước khi chọn chi tiết triển khai
- Giữ vòng lặp cải tiến ngắn, có thể đo lường khi tinh chỉnh prompt/logic
- Xem observability và error handling là thành phần cốt lõi của giải pháp
- Ưu tiên các pattern có thể lặp lại để agent dễ bảo trì và mở rộng theo team

### Ứng Dụng Vào Công Việc

- Áp dụng prompt template có cấu trúc thay vì prompt ngẫu hứng trong task thực tập
- Dùng vòng lặp kiểm chứng khi làm tính năng liên quan AI: đặt tiêu chí -> test -> tinh chỉnh
- Thiết kế task cho agent với ranh giới rõ về công cụ, nguồn dữ liệu và output kỳ vọng
- Thêm logging cơ bản và các checkpoint review khi tự động hóa workflow kỹ thuật
- Ghi rõ giả định và ràng buộc để teammate có thể tái sử dụng và cải tiến cùng workflow

### Trải Nghiệm Trong Event

Theo dõi **"AWS FCAJ Agent Forge - Deepdive"** là trải nghiệm hữu ích vì sự kiện kết nối liền mạch giữa tư duy kiến trúc và triển khai thực hành.

#### Điểm mình thấy hữu ích nhất

- Phần lý thuyết đưa ra mô hình tư duy rõ ràng về cách thiết kế và vận hành AI agent
- Phần lab biến mô hình đó thành hành động cụ thể, giúp kiến thức dễ thấm hơn
- Sự kết hợp giữa chiến lược (why) và triển khai (how) làm mình tự tin hơn khi xây dựng workflow agent

#### Điểm cần cải thiện thêm

- Mình cần tiếp tục rèn prompt engineering có kỷ luật để output ổn định hơn
- Cần luyện thêm các kịch bản đánh giá để phát hiện failure pattern sớm
- Cần cải thiện thói quen viết tài liệu để workflow dễ tái lập và thân thiện với làm việc nhóm

> Tổng thể, sự kiện giúp mình chuyển từ mức hiểu cơ bản về AI assistant sang góc nhìn thực tiễn và thiên về kỹ thuật hơn khi xây dựng AI agent trên AWS.

