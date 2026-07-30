---
title: "Tự đánh giá"
date: 2026-07-30
weight: 6
chapter: false
pre: " <b> 6. </b> "
---

## Tổng quan

Trong thời gian thực tập từ **01/06/2026 đến 23/08/2026** tại **Công ty TNHH Amazon Web Services Viet Nam**, tôi tham gia chương trình **Workforce Bootcamp – First Cloud AI Journey**. Trọng tâm công việc là xây dựng và hoàn thiện dự án **AI Coding Agent Risk Scorer**: hệ thống ghi nhận trajectory của coding agent, trích xuất đặc trưng, đánh giá mức rủi ro bằng mô hình ML và áp dụng policy để đưa ra quyết định cho phép, yêu cầu kiểm tra hoặc chặn.

Quá trình thực hiện giúp tôi kết nối kiến thức Khoa học máy tính với thực hành AWS và MLOps. Tôi đã hoàn thiện worklog tám tuần, proposal, workshop kỹ thuật, các bài blog chuyên môn, báo cáo sự kiện và bộ tài liệu song ngữ cho dự án. Tôi cũng hiểu rõ hơn rằng một hệ thống AI có giá trị không chỉ cần model có metric tốt mà còn cần dữ liệu phù hợp, quy trình đánh giá, governance, monitoring, kiểm soát chi phí và sự tham gia của con người ở các quyết định rủi ro cao.

## Kết quả và kỹ năng đạt được

- Xây dựng được luồng dữ liệu cho AI Coding Agent Risk Scorer từ trajectory JSON/JSONL, feature engineering, chia dữ liệu đến huấn luyện và đánh giá XGBoost.
- Hiểu rõ hơn cách sử dụng Amazon S3, SageMaker Processing, Training, HPO, Pipelines, Model Registry, Endpoint, Lambda, API Gateway, CloudWatch và Model Monitor trong một ML workflow.
- Rèn luyện tư duy thiết kế có governance: quality gate, manual approval, decision policy, kiểm soát false negative và phân biệt model đã đăng ký với model đã được deploy.
- Cải thiện kỹ năng đọc tài liệu AWS, phân tích kiến trúc, viết tài liệu kỹ thuật, tổng hợp evidence và trình bày nội dung song ngữ.
- Củng cố kỹ năng tự học qua các chủ đề AWS Cloud Practitioner, SLA/monitoring, bảo mật web application, Agentic AI và các dự án thực hành được chia sẻ trong sự kiện.

## Tự đánh giá theo tiêu chí

| STT | Tiêu chí | Tự đánh giá | Cơ sở đánh giá |
| --- | --- | --- | --- |
| 1 | Kiến thức và kỹ năng chuyên môn | Tốt | Vận dụng Python, ML/XGBoost, AWS và MLOps để hoàn thiện workflow có dữ liệu, huấn luyện, đánh giá, governance và monitoring. |
| 2 | Khả năng học hỏi | Tốt | Chủ động tìm hiểu dịch vụ AWS, kiến thức MLOps và các giới hạn của dữ liệu synthetic trong thời gian thực tập. |
| 3 | Tính chủ động | Tốt | Hoàn thiện tài liệu dự án, workshop, blog và evidence; chủ động rà lỗi liên kết, ảnh và nội dung báo cáo. |
| 4 | Tinh thần trách nhiệm | Tốt | Theo dõi công việc qua worklog, duy trì cấu trúc tài liệu và cleanup các tài nguyên demo có thể phát sinh chi phí. |
| 5 | Kỷ luật và quản lý thời gian | Khá | Hoàn thành các mốc chính; cần tiếp tục cải thiện việc ước lượng thời gian cho kiểm thử, tài liệu và rà soát cuối. |
| 6 | Tư duy giải quyết vấn đề | Tốt | Phân tích vấn đề theo evidence, tách nguyên nhân kỹ thuật với giới hạn dữ liệu và ưu tiên giải pháp có thể kiểm chứng. |
| 7 | Giao tiếp và trình bày | Khá | Có thể tổng hợp nội dung kỹ thuật thành proposal, workshop và blog; cần rèn luyện thêm trình bày ngắn gọn trước nhóm hoặc hội đồng. |
| 8 | Hợp tác và tiếp nhận phản hồi | Khá | Tham gia các hoạt động FCAJ, tiếp thu chia sẻ từ diễn giả và điều chỉnh tài liệu theo yêu cầu báo cáo. |
| 9 | Ý thức bảo mật và chi phí | Tốt | Nhận thức về least privilege, quản lý secrets, manual approval, cleanup endpoint/API và không diễn giải quá mức metric synthetic. |
| 10 | Đóng góp vào dự án | Tốt | Hoàn thiện bộ báo cáo có thể theo dõi từ worklog, proposal, workshop, blog đến evidence và tài liệu kỹ thuật. |
| 11 | Tổng thể | Tốt | Đạt mục tiêu học hỏi và xây dựng sản phẩm thử nghiệm có quy trình MLOps rõ ràng; vẫn cần mở rộng dữ liệu thực tế và kinh nghiệm production. |

## Điểm cần cải thiện

1. **Dữ liệu và đánh giá thực tế:** Dataset hiện tại chủ yếu là synthetic. Tôi cần học thêm về thu thập dữ liệu đại diện, gán nhãn độc lập, đánh giá distribution shift và thiết kế thí nghiệm đáng tin cậy hơn.
2. **Triển khai production và bảo mật:** Tôi cần đào sâu về least-privilege IAM, quản lý đa tài khoản, CI/CD, quan sát hệ thống và tối ưu chi phí khi vận hành dịch vụ lâu dài.
3. **Giao tiếp kỹ thuật:** Tôi cần luyện thêm kỹ năng trình bày kiến trúc, giải thích trade-off và bảo vệ các quyết định kỹ thuật một cách ngắn gọn, rõ ràng cho cả đối tượng kỹ thuật lẫn không kỹ thuật.

## Định hướng tiếp theo

Sau chương trình, tôi sẽ tiếp tục phát triển kiến thức cloud và AI/ML bằng các bài thực hành AWS, củng cố nền tảng system design và triển khai các dự án nhỏ có monitoring, security và cost awareness ngay từ đầu. Với AI Coding Agent Risk Scorer, bước tiếp theo là bổ sung trajectory thực tế có human label, đánh giá lại model trên dữ liệu đại diện hơn và chỉ đưa model sang production sau khi hoàn thành governance phù hợp.
