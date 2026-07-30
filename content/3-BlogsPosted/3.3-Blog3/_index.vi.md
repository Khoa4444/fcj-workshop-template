---
title: "Blog 3"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---
# Model đạt metric tốt chưa đủ: vì sao ML vẫn cần quy trình phê duyệt?

Một model có accuracy cao không đồng nghĩa với việc nên được đưa thẳng vào production. Với những hệ thống tác động đến người dùng hoặc đưa ra quyết định có rủi ro, đội ngũ còn cần biết: model có đạt ngưỡng chất lượng không, có dấu hiệu thiên lệch không, feature quan trọng có hợp lý không, và endpoint sau khi triển khai có hoạt động đúng trong môi trường gần production hay không.

Nếu mọi kiểm tra đều làm thủ công, quy trình sẽ nhanh chóng thành nút thắt. Model càng nhiều, người duyệt càng ít thời gian và tiêu chuẩn đánh giá càng dễ không đồng nhất. Hướng tiếp cận tốt hơn là biến các tiêu chuẩn đó thành code, chạy chúng tự động mỗi khi có model version mới.

## Tách “model được duyệt” và “endpoint được duyệt”

Model nên được duyệt khi vượt qua các kiểm tra về model quality, bias và feature importance theo ngưỡng của tổ chức. Nhưng kể cả model đã được duyệt, endpoint vẫn cần được xác nhận ở môi trường giống production: khả năng tích hợp, hành vi runtime, quyền truy cập và các yêu cầu vận hành. Tách hai bước này giúp tránh coi một metric tốt trong notebook là bằng chứng đủ cho toàn bộ hệ thống.

## Luồng phê duyệt tự động với SageMaker

Một luồng tham chiếu có thể bắt đầu khi data scientist commit code. SageMaker Pipelines chạy build, training và processing job; Amazon SageMaker Clarify tạo báo cáo về model quality, bias và explainability; artifact được lưu trong Amazon S3. Model mới được đăng ký vào SageMaker Model Registry với trạng thái `PendingManualApproval`.

Sau đó, kiến trúc event-driven tiếp quản:

`Model Registry → EventBridge → Lambda → SageMaker approval pipeline`

EventBridge nhận sự kiện khi model package đang chờ phê duyệt. Lambda khởi chạy approval pipeline. Pipeline đọc các report, đối chiếu với threshold đã định nghĩa và xuất kết quả kiểm tra. Nếu tất cả điều kiện đạt, pipeline cập nhật model package thành `Approved`; nếu không, chuyển thành `Rejected` và ghi rõ lý do.

Reviewer vì thế không cần lặp lại các kiểm tra định lượng quen thuộc. Con người có thể tập trung vào các trường hợp ngoại lệ, chính sách và rủi ro mà rule tự động chưa mô tả hết.

## Vì sao nên có governance account riêng?

Trong mô hình nhiều AWS account, artifact và cơ chế phê duyệt có thể được đặt trong một AI/ML governance account tách với môi trường phát triển. Artifact từ development account được chuyển sang bucket kiểm soát ở governance account, nơi pipeline xác thực chạy với quyền truy cập hạn chế hơn.

Thiết kế này tách trách nhiệm giữa team xây model và team đặt/chấp thuận tiêu chuẩn phát hành, đồng thời tạo audit trail rõ hơn: model version nào đã được kiểm tra, theo ngưỡng nào và được duyệt hay từ chối vì điều gì.

## Áp dụng cho AI Agent Risk Scorer

Với model chấm điểm rủi ro cho AI coding agent, quality gate không nên chỉ nhìn accuracy. Có thể đặt điều kiện về risky recall để hạn chế bỏ sót trajectory nguy hiểm, kết hợp false-negative rate và đánh giá dữ liệu/feature. Ngay cả khi model vượt ngưỡng, trạng thái `PendingManualApproval` vẫn hữu ích để reviewer xem lại artifact và policy trước khi promotion.

Sau khi endpoint được triển khai, monitoring vẫn là phần bắt buộc. Model production có thể gặp distribution khác, feature drift hoặc hành vi mới từ agent mà dữ liệu huấn luyện chưa phản ánh. Approval là một cổng kiểm soát quan trọng, không phải điểm kết thúc của MLOps.

## Hình ảnh minh họa

> **[PLACEHOLDER ẢNH 3]** Chèn sơ đồ workflow: Development account/S3 → Model Registry (`PendingManualApproval`) → EventBridge → Lambda → SageMaker approval pipeline → `Approved` hoặc `Rejected`; thêm governance account ở phía kiểm tra.
>
> **Nên lấy ảnh ở đâu:** dùng sơ đồ “solution architecture using SageMaker Pipelines to automate model approval” trong [bài AWS gốc](https://aws.amazon.com/blogs/machine-learning/automate-the-machine-learning-model-approval-process-with-amazon-sagemaker-model-registry-and-amazon-sagemaker-pipelines/).
>
> **Cách lấy:** mở bài AWS, tìm phần **Solution overview**, bấm/lưu hình kiến trúc được đặt ngay dưới phần này. Giữ attribution “Source: AWS”. Nếu cần sơ đồ có tiếng Việt, dùng [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/) để vẽ lại theo đúng flow trên và xuất PNG; không chỉnh sửa ảnh AWS rồi xóa attribution.
>
> **Tên file đề xuất:** `sagemaker-model-approval-workflow.png`.
>
> **Chỗ chèn sau khi có file:** `![Luồng phê duyệt model tự động bằng SageMaker](sagemaker-model-approval-workflow.png)`

## Link bài đã đăng

> **[PLACEHOLDER LINK FACEBOOK]** Dán link bài đã đăng trong AWS Study Group vào đây.

## Nguồn tham khảo

- [Automate the machine learning model approval process with Amazon SageMaker Model Registry and Amazon SageMaker Pipelines — AWS](https://aws.amazon.com/blogs/machine-learning/automate-the-machine-learning-model-approval-process-with-amazon-sagemaker-model-registry-and-amazon-sagemaker-pipelines/)
- [Build an Amazon SageMaker Model Registry approval and promotion workflow with human intervention — AWS](https://aws.amazon.com/blogs/machine-learning/build-an-amazon-sagemaker-model-registry-approval-and-promotion-workflow-with-human-intervention/)
- [Improve governance of your machine learning models with Amazon SageMaker — AWS](https://aws.amazon.com/blogs/machine-learning/improve-governance-of-your-machine-learning-models-with-amazon-sagemaker/)
