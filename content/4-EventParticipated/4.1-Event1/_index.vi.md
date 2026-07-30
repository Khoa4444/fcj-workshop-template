---
title: "Event 1"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Báo cáo tham gia sự kiện “Cloud Architect”

## 1. Thông tin sự kiện

- **Tên sự kiện:** Cloud Architect
- **Thời gian:** 09:00 (tài liệu chưa cung cấp ngày tổ chức)
- **Địa điểm:** Tầng 26, Bitexco Tower, 02 Hải Triều, phường Sài Gòn, Thành phố Hồ Chí Minh
- **Vai trò tham gia:** Người tham dự (attendee)

## 2. Tổng quan

Sự kiện tập trung vào kiến thức và định hướng thực tế khi làm việc với nền tảng đám mây AWS. Ba phiên trình bày bổ trợ cho nhau: lộ trình chinh phục chứng chỉ AWS Cloud Practitioner, giám sát dịch vụ theo góc nhìn trải nghiệm người dùng và tăng cường bảo mật ứng dụng web bằng tác tử bảo mật AWS.

## 3. Nội dung nổi bật

### 3.1. Inside the Exam: AWS Cloud Practitioner

Diễn giả **Ngô Lê Tấn Huy** giới thiệu lộ trình chuẩn bị cho kỳ thi AWS Certified Cloud Practitioner (CLF-C02). Đây là chứng chỉ nền tảng, hướng đến khả năng hiểu bức tranh tổng quan về AWS thay vì yêu cầu lập trình hoặc cấu hình hệ thống chuyên sâu.

Nội dung thi được chia thành bốn nhóm: Cloud Concepts (24%), Security and Compliance (30%), Cloud Technology and Services (34%), và Billing, Pricing, and Support (12%). Phiên trình bày cũng giúp làm rõ các kiến thức cần nắm như sáu lợi ích của điện toán đám mây, AWS Well-Architected Framework, AWS Cloud Adoption Framework, Shared Responsibility Model, IAM, các dịch vụ hạ tầng toàn cầu, compute, storage, database, networking và các mô hình định giá EC2.

Những kinh nghiệm ôn thi hữu ích gồm:

- Học dịch vụ theo từ khóa và tình huống sử dụng thực tế, ví dụ SQS cho bài toán decouple/microservices.
- Phân tích kỹ các câu làm sai trong đề luyện, thay vì chỉ làm nhiều đề.
- Thực hành trên AWS Free Tier với EC2, S3 và IAM để hình dung kiến thức.
- Dùng phương pháp loại trừ, chú ý từ khóa như “Not”, “Least cost”, “Most scalable” và đánh dấu câu chưa chắc chắn để xem lại.

### 3.2. SLA and Monitoring: From SLA to Monitoring What Really Matters

Diễn giả **Nguyễn Huỳnh Sơn** trình bày về mối liên hệ giữa SLA, quản trị rủi ro và giám sát hệ thống. SLA là cam kết xác định mức dịch vụ kỳ vọng giữa nhà cung cấp và khách hàng; vì vậy, monitoring cần phát hiện sớm rủi ro trước khi nó trở thành khiếu nại của người dùng.

Điểm nhấn quan trọng là: **hạ tầng “xanh” chưa chắc người dùng đã có trải nghiệm tốt**. Một hệ thống có CPU thấp, bộ nhớ ổn định và health check thành công vẫn có thể khiến người dùng không đăng nhập được nếu kết nối cơ sở dữ liệu gặp lỗi. Vì thế, việc giám sát nên được tổ chức theo các tầng:

1. Trải nghiệm khách hàng: có đăng nhập, mua hàng hoặc thanh toán được không.
2. Chỉ số nghiệp vụ: tỷ lệ đăng nhập thành công, số đơn hàng, doanh thu.
3. Chỉ số ứng dụng: độ trễ, lỗi và request.
4. Chỉ số hạ tầng và dịch vụ AWS: CPU, memory, disk, network, EC2, RDS, ALB, S3.

Phiên demo minh họa cách theo dõi metric đăng nhập thất bại, thiết lập CloudWatch Alarm theo ngưỡng và gửi cảnh báo qua SNS để đội ngũ có thể phản ứng theo quy trình xử lý sự cố.

### 3.3. Securing Your Web Apps With AWS Security Agent

Diễn giả **Nguyễn Tuấn Thịnh** giới thiệu AWS Security Agent như một hướng tiếp cận tự động hóa bảo mật ứng dụng web. Tác tử này được trình bày với khả năng hỗ trợ toàn bộ vòng đời bảo mật: rà soát thiết kế, kiểm tra mã nguồn và kiểm thử xâm nhập đối với ứng dụng đang chạy.

- **Design Security Review:** kiểm tra tài liệu Markdown hoặc mã Terraform theo các bộ yêu cầu như PCI DSS, NIST CSF và AWS Well-Architected.
- **Code Security Review:** tích hợp vào pull request GitHub/GitLab, nhận diện lỗ hổng và secrets, đồng thời đề xuất bản vá.
- **Automated Pentesting:** thực hiện các chuỗi khai thác nhiều bước, xác thực như người dùng thực và cung cấp bằng chứng kiểm tra.

Phần trình bày cũng nêu rõ các giới hạn cần cân nhắc: MFA, biometric hoặc mTLS có thể chặn tác tử; lỗi logic nghiệp vụ đòi hỏi nhiều ngữ cảnh hơn; chi phí task-hour có thể tăng nhanh với ứng dụng phức tạp. Vì vậy, cần theo dõi mức sử dụng, xác thực kết quả và kết hợp công cụ với quy trình bảo mật của đội ngũ.

## 4. Kiến thức và kinh nghiệm thu nhận được

- Có cái nhìn hệ thống về các khái niệm, dịch vụ và cách học hiệu quả cho chứng chỉ AWS Cloud Practitioner.
- Hiểu Shared Responsibility Model: AWS chịu trách nhiệm về bảo mật **của** đám mây, còn khách hàng chịu trách nhiệm về bảo mật **trong** đám mây.
- Nhận thức rằng giám sát cần bám sát hành trình người dùng và chỉ số nghiệp vụ, không chỉ dựa vào chỉ số hạ tầng.
- Biết cách kết nối custom metric, CloudWatch Alarm và SNS để cảnh báo trước khi SLA bị ảnh hưởng.
- Nắm được vai trò của AI agent trong rà soát thiết kế, code review và pentesting; đồng thời hiểu các giới hạn và yêu cầu kiểm soát chi phí.

## 5. Khả năng áp dụng

Từ nội dung sự kiện, tôi có thể xây dựng lộ trình học và thực hành AWS theo từng nhóm dịch vụ, bắt đầu bằng các bài thực hành Free Tier. Với các dự án web, tôi có thể bổ sung chỉ số theo hành trình người dùng như tỷ lệ đăng nhập hoặc thanh toán thành công, sau đó cấu hình cảnh báo CloudWatch và SNS cho các ngưỡng rủi ro. Về bảo mật, việc đưa rà soát thiết kế, kiểm tra secrets và code review vào sớm trong quy trình phát triển sẽ giúp phát hiện vấn đề trước khi triển khai.

## 6. Cảm nhận cá nhân

Sự kiện mang lại góc nhìn cân bằng giữa kiến thức nền tảng, vận hành hệ thống và bảo mật ứng dụng trên AWS. Tôi ấn tượng nhất với thông điệp rằng một hệ thống chỉ thực sự hoạt động tốt khi người dùng hoàn thành được hành trình của họ, không chỉ khi dashboard hạ tầng hiển thị trạng thái bình thường. Các phiên chia sẻ cũng giúp tôi hình dung rõ hơn cách kết hợp kiến thức AWS, monitoring và bảo mật vào công việc thực tế.

## 7. Ảnh minh chứng

![Ảnh minh chứng tham gia sự kiện Cloud Architect](/images/4-EventParticipated/event-1-evidence.jpg)

Tài liệu trình bày được lưu trong hồ sơ sự kiện; website chỉ công bố ảnh minh chứng tham gia.
