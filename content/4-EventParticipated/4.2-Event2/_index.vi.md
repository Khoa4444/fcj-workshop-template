---
title: "Event 2"
date: 2026-07-25
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Báo cáo tham gia sự kiện “First Cloud AI Journey × Agentic AI Build Week”

## 1. Thông tin sự kiện

- **Tên sự kiện:** First Cloud AI Journey × Agentic AI Build Week (FCAJ × AABW)
- **Thời gian:** 25/7/2026
- **Địa điểm:** Tầng 26, Bitexco Tower, 02 Hải Triều, phường Sài Gòn, Thành phố Hồ Chí Minh
- **Vai trò:** Người tham dự

## 2. Tổng quan

FCAJ × AABW là sự kiện xoay quanh hành trình xây dựng sản phẩm với AWS và Agentic AI. Các đội tham gia chia sẻ cách biến một vấn đề thực tế thành sản phẩm thử nghiệm trong thời gian ngắn: xác định bài toán, thiết kế kiến trúc, tích hợp AI agent, cân đối chi phí, demo và rút kinh nghiệm sau quá trình phát triển.

Điểm nổi bật của sự kiện là tính thực hành cao. Thay vì chỉ giới thiệu công nghệ, các diễn giả trình bày toàn bộ quá trình xây dựng sản phẩm, những quyết định kỹ thuật, khó khăn khi làm việc nhóm và bài học nhận được từ hackathon.

## 3. Nội dung nổi bật

### 3.1. Hackathon Journey – dự án S.H.E.P.H.E.R.D.

Nhóm **3KA** chia sẻ hành trình tham gia hackathon trong 24 giờ. Động lực của nhóm là thử sức ngoài môi trường lớp học, tích lũy kinh nghiệm AI và AWS, xây dựng MVP đầu-cuối trong áp lực thời gian, cũng như rèn luyện khả năng phối hợp nhóm.

Dự án **S.H.E.P.H.E.R.D.** (Smart Human-flow Evaluation, Prediction, Hazard Detection, Response, and Dispatch) hỗ trợ vận hành không gian đông người. Hệ thống phân tích luồng camera để phát hiện và theo dõi người, đo mật độ đám đông, ước lượng hàng chờ, nhận diện nguy cơ ùn tắc, đưa ra cảnh báo sớm và đề xuất hành động cho nhân sự vận hành.

Kiến trúc được định hướng với YOLO và ByteTrack cho thị giác máy tính, Amazon SageMaker cho suy luận, Amazon Bedrock AgentCore + Strands cho lớp agentic AI, cùng dashboard React để theo dõi. Tác tử giám sát liên tục đọc các chỉ số, dự báo nguy cơ quá tải và gửi cảnh báo chủ động; Operator Copilot cho phép nhân viên đặt câu hỏi bằng ngôn ngữ tự nhiên dựa trên số liệu thời gian thực.

Những thách thức chính gồm duy trì luồng video ổn định, giảm độ trễ suy luận, giữ vết đối tượng giữa các frame, lựa chọn vị trí camera, kiểm soát chi phí và giới hạn phạm vi trong thời gian hackathon. Bài học nhóm rút ra là cần xác định rõ tiêu chí hoàn thành, chuẩn bị sẵn công cụ/tài khoản, phân vai từ đầu và luyện tập câu chuyện demo ngắn gọn.

### 3.2. One Team – KFC Bot Agent

Nhóm **One Team** giới thiệu **KFC Bot Agent**, một agent đặt món hội thoại đa kênh. Bài toán xuất phát từ việc trải nghiệm đặt món thường bị gián đoạn khi người dùng phải chuyển ứng dụng, tạo tài khoản mới hoặc lặp lại nhu cầu với nhân viên hỗ trợ.

Sản phẩm hướng đến trải nghiệm đặt hàng trực tiếp trong các kênh như Zalo, WhatsApp và các kênh mở rộng trong tương lai. Agent không chỉ trả lời hội thoại mà còn thực hiện quy trình đặt món: hiểu ý định, lập kế hoạch bước xử lý, tra cứu dữ liệu nghiệp vụ tin cậy, cập nhật giỏ hàng và áp dụng khuyến mãi, sau đó xác nhận lại với trạng thái giỏ hàng thực.

Điểm đáng chú ý trong thiết kế là tư duy “design once, deploy everywhere”: thêm kênh mới bằng adapter, thêm nghiệp vụ bằng connector và thêm khả năng bằng tool. Nhóm cũng trình bày các chỉ số vận hành mục tiêu như chi phí hạ tầng khoảng 88 USD/tháng trong kịch bản 500 đơn/ngày, độ trễ đầu cuối 3–5 giây và việc giảm công sức hạ tầng nhờ AgentCore.

### 3.3. SA Professional AI Native App

Nhóm trình bày **SA Professional AI Native App**, công cụ hỗ trợ Solution Architect xử lý yêu cầu thiết kế hệ thống trong thời gian ngắn. Bài toán thực tế là SA phải đọc BRD/PRD, trích xuất yêu cầu, tạo bản kiến trúc ban đầu, vẽ sơ đồ và ước tính chi phí AWS, trong khi khách hàng thường cần phản hồi ngay.

Ứng dụng có thể phân tích yêu cầu tự nhiên và dữ liệu có cấu trúc; đề xuất các phương án kiến trúc có xét đến hybrid cloud và tiêu chuẩn công ty; tạo sơ đồ Draw.io/AWS có thể chỉnh sửa; ước tính chi phí định hướng cho khu vực ap-southeast-1; và chỉ ra giả định, khuyến nghị hoặc khoảng trống yêu cầu. Người dùng tiếp tục tinh chỉnh qua giao diện chat và chỉ dẫn theo từng dự án.

Giá trị thực tế của công cụ là chuyển quá trình làm việc từ đọc tài liệu và bắt đầu từ trang trắng sang tạo Requirements Catalogue trong vài phút, có bản kiến trúc ban đầu để phản biện, sinh IaC tự động và có ước tính AWS đồng thời với kiến trúc.

### 3.4. Signal Scout

Nhóm Signal Scout giới thiệu nền tảng AI hỗ trợ theo dõi thay đổi chiến lược doanh nghiệp. Sản phẩm kết nối các tín hiệu rời rạc từ dữ liệu doanh nghiệp, thu thập và kiểm chứng bằng chứng, phân tích chỉ số và dựng kịch bản để giúp đội ngũ chiến lược, quản trị rủi ro, competitive intelligence và quản lý khách hàng doanh nghiệp ra quyết định.

Giá trị cốt lõi của Signal Scout là phát hiện sớm tín hiệu tái cấu trúc hoặc thay đổi chiến lược, trình bày kết luận có bằng chứng, đồng thời giữ con người trong vòng kiểm soát khi ra quyết định. Kiến trúc sử dụng các dịch vụ AWS như Bedrock, AgentCore, WAF, Amplify, CloudWatch, DynamoDB, Lambda, S3, API Gateway và Cognito; kết hợp Apify/TinyFish để thu thập dữ liệu và Langfuse để quan sát hoạt động AI.

Phần chia sẻ chi phí cho thấy hệ thống có thể vận hành theo nhiều mức tải: tổng mức ước tính khoảng 81 USD, 94 USD hoặc 359 USD mỗi tháng, tùy mức sử dụng và các dịch vụ bên ngoài. Điều này nhấn mạnh yêu cầu thiết kế kiến trúc phù hợp với ngân sách ngay từ giai đoạn MVP.

## 4. Kiến thức và kinh nghiệm thu nhận được

- Hiểu quy trình đưa một ý tưởng AI từ bài toán thực tế đến MVP có thể demo trong hackathon.
- Nhận thấy agentic AI hiệu quả khi được kết nối với dữ liệu, công cụ và bước xác thực rõ ràng, thay vì chỉ tạo câu trả lời hội thoại.
- Biết cách kết hợp computer vision, AI agent, dashboard và cloud inference trong bài toán giám sát thời gian thực.
- Hiểu giá trị của kiến trúc có khả năng mở rộng theo kênh, nghiệp vụ và tính năng.
- Có thêm góc nhìn về việc tự động hóa công việc của Solution Architect, từ trích xuất yêu cầu đến sinh sơ đồ, IaC và ước tính chi phí.
- Nhận thức rõ hơn về vai trò của bằng chứng, quan sát hệ thống, kiểm soát chi phí và human-in-the-loop khi triển khai AI cho doanh nghiệp.

## 5. Khả năng áp dụng

Tôi có thể áp dụng tư duy hackathon vào các dự án cá nhân bằng cách chọn một vấn đề nhỏ, xác định MVP và ưu tiên hoàn thiện một tính năng cốt lõi. Khi xây dựng chatbot hoặc AI agent, tôi sẽ thiết kế luồng hành động có kiểm chứng từ dữ liệu nghiệp vụ thay vì chỉ dựa vào câu trả lời của mô hình. Với các bài toán trên AWS, tôi sẽ cân nhắc chi phí, độ trễ, khả năng quan sát và mở rộng ngay từ đầu; đồng thời tận dụng công cụ AI để tăng tốc việc đọc yêu cầu, phác thảo kiến trúc và tạo tài liệu kỹ thuật.

## 6. Cảm nhận cá nhân

Sự kiện mang lại nhiều ví dụ gần gũi về cách dùng AWS và Agentic AI để giải quyết các vấn đề cụ thể: điều phối đám đông, đặt món đa kênh, hỗ trợ Solution Architect và theo dõi tín hiệu doanh nghiệp. Tôi ấn tượng với tinh thần thử nghiệm, dám làm và sẵn sàng chia sẻ cả những khó khăn của các đội. Qua đó, tôi nhận ra một sản phẩm AI có giá trị không chỉ cần mô hình tốt mà còn cần bài toán đúng, dữ liệu và công cụ đáng tin cậy, kiến trúc phù hợp, cùng một demo rõ ràng cho người dùng.

## 7. Ảnh minh chứng

![Ảnh minh chứng tham gia sự kiện FCAJ × AABW](/images/4-EventParticipated/event-2-evidence.jpg)

Tài liệu trình bày được lưu trong hồ sơ sự kiện; website chỉ công bố ảnh minh chứng tham gia.
