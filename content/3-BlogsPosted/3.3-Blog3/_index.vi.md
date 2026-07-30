---
title: "Model đạt metric tốt chưa đủ: vì sao ML vẫn cần quy trình phê duyệt?"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

## Thông tin bài viết

| Thông tin | Chi tiết |
|---|---|
| Ngày đăng | Sẽ cập nhật |
| Trạng thái | Đã đăng |
| Platform | AWS Study Group - Facebook Group |
| Bài viết đã đăng | Sẽ cập nhật liên kết Facebook |

Một model có accuracy cao không đồng nghĩa với việc nên được đưa thẳng vào production. Với những hệ thống tác động đến người dùng hoặc quyết định có rủi ro, đội ngũ còn cần biết: model có đạt ngưỡng chất lượng đã đặt ra không, có dấu hiệu thiên lệch không, feature quan trọng có hợp lý không, và endpoint sau khi triển khai có hoạt động đúng trong môi trường gần production hay không.

Nếu mọi kiểm tra này đều làm thủ công, quy trình sẽ nhanh chóng trở thành nút thắt. Model càng nhiều, người duyệt càng ít thời gian, còn tiêu chuẩn đánh giá dễ không đồng nhất giữa các team. Hướng tiếp cận tốt hơn là biến các tiêu chuẩn đó thành code và chạy chúng tự động mỗi khi có model version mới.

## Tách “model được duyệt” và “endpoint được duyệt”

Một ý quan trọng trong kiến trúc MLOps là model và endpoint là hai đối tượng cần được xem xét riêng.

Model chỉ nên được duyệt khi vượt qua các kiểm tra về chất lượng, bias và feature importance theo ngưỡng của tổ chức. Nhưng kể cả model đã được duyệt, endpoint vẫn cần được xác nhận ở môi trường giống production: khả năng tích hợp, hành vi runtime, quyền truy cập và các yêu cầu vận hành.

Tách hai bước này tránh việc coi một metric tốt trong notebook là bằng chứng đủ cho toàn bộ hệ thống.

## Luồng phê duyệt tự động với SageMaker

Một luồng tham chiếu có thể bắt đầu khi data scientist commit code. SageMaker Pipelines chạy build, training và các processing job; Amazon SageMaker Clarify tạo các báo cáo về model quality, bias và explainability, rồi các artifact được lưu trong Amazon S3. Model mới được đăng ký vào SageMaker Model Registry với trạng thái `PendingManualApproval`.

Từ đây, kiến trúc event-driven tiếp quản:

`Model Registry → EventBridge → Lambda → SageMaker approval pipeline`

EventBridge nhận sự kiện khi một model package ở trạng thái chờ phê duyệt. Lambda khởi chạy approval pipeline. Pipeline đọc báo cáo đã lưu, đối chiếu với các threshold đã định nghĩa và xuất kết quả kiểm tra. Nếu tất cả điều kiện đạt, pipeline cập nhật model package thành `Approved`; nếu không, chuyển thành `Rejected` và ghi rõ lý do.

Điểm hay của cách làm này là reviewer không cần lặp lại các kiểm tra định lượng quen thuộc. Con người có thể tập trung vào các trường hợp ngoại lệ, chính sách và rủi ro mà rule tự động chưa mô tả hết.

## Vì sao nên có tài khoản governance riêng?

Trong mô hình nhiều AWS account, các artifact và cơ chế phê duyệt có thể được đặt trong một AI/ML governance account tách với môi trường phát triển. Artifact từ development account được chuyển sang bucket kiểm soát ở governance account, nơi pipeline xác thực chạy với quyền truy cập hạn chế hơn.

Thiết kế này giúp tách trách nhiệm giữa team xây model và team đặt/chấp thuận tiêu chuẩn phát hành. Nó cũng tạo audit trail rõ hơn: model version nào đã được kiểm tra, kiểm tra theo ngưỡng nào và được duyệt hay từ chối vì điều gì.

## Áp dụng cho hệ thống AI Agent Risk Scorer

Với một model chấm điểm rủi ro cho AI coding agent, quality gate không nên chỉ nhìn accuracy. Ví dụ, có thể đặt điều kiện về risky recall để hạn chế bỏ sót trajectory nguy hiểm, đồng thời kiểm tra false-negative rate và dữ liệu/feature dùng để đánh giá. Khi model đạt ngưỡng, nó vẫn nên nằm ở `PendingManualApproval` để reviewer xem lại dữ liệu, artifact và policy trước khi promotion.

Sau khi endpoint được triển khai, monitoring tiếp tục là phần bắt buộc. Model production có thể gặp distribution khác, feature drift hoặc hành vi mới từ agent mà dữ liệu huấn luyện chưa phản ánh. Approval là một cổng kiểm soát quan trọng, không phải điểm kết thúc của MLOps.

Tự động hóa phê duyệt không nhằm loại bỏ con người khỏi quy trình. Mục tiêu là tự động hóa các kiểm tra lặp lại, nhất quán và đo được; từ đó dành thời gian của con người cho những quyết định có bối cảnh và trách nhiệm cao hơn.

## Nguồn tham khảo

- [Automate the machine learning model approval process with Amazon SageMaker Model Registry and Amazon SageMaker Pipelines — AWS](https://aws.amazon.com/blogs/machine-learning/automate-the-machine-learning-model-approval-process-with-amazon-sagemaker-model-registry-and-amazon-sagemaker-pipelines/)
- [Build an Amazon SageMaker Model Registry approval and promotion workflow with human intervention — AWS](https://aws.amazon.com/blogs/machine-learning/build-an-amazon-sagemaker-model-registry-approval-and-promotion-workflow-with-human-intervention/)
- [Improve governance of your machine learning models with Amazon SageMaker — AWS](https://aws.amazon.com/blogs/machine-learning/improve-governance-of-your-machine-learning-models-with-amazon-sagemaker/)


---

[Quay lại Blogs Posted](../)
