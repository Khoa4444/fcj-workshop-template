---
title: "Tuning hyperparameter thủ công mãi? Thử SageMaker Automatic Model Tuning"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

## Thông tin bài viết

| Thông tin | Chi tiết |
|---|---|
| Ngày đăng | Đang chờ duyệt |
| Trạng thái | Đang chờ duyệt |
| Platform | AWS Study Group - Facebook Group |
| Liên kết Facebook | Đang chờ duyệt |

![Luồng huấn luyện mô hình với Amazon SageMaker](/images/3-BlogsPosted/sagemaker-automatic-model-tuning.png)

*Hình 1. Amazon SageMaker tạo Training Job từ notebook, dùng dữ liệu trên Amazon S3, lưu model artifact trên S3 và ghi log, metric lên Amazon CloudWatch.*

Làm machine learning có một đoạn rất dễ “mất thời gian vô tận”: model đã train được, dữ liệu cũng ổn, nhưng chưa biết nên đặt learning rate, max depth, regularization thế nào để kết quả tốt hơn.

Thử tay vài bộ thì dễ. Nhưng khi số hyperparameter tăng lên, số tổ hợp có thể thử sẽ tăng rất nhanh. Lúc đó, chạy từng lần rồi ghi chép lại không chỉ tốn công mà còn khó biết mình đã bỏ lỡ cấu hình tốt nào.

Amazon SageMaker Automatic Model Tuning (AMT) sinh ra để xử lý phần này.

Thay vì tự tạo nhiều training job, mình chỉ cần chuẩn bị ba thứ:

* **Training job:** model hoặc thuật toán muốn train, ví dụ XGBoost.
* **Objective metric:** chỉ số muốn tối ưu, ví dụ `validation:accuracy`, macro F1 hoặc risky recall.
* **Search space:** khoảng giá trị cho những hyperparameter cần thử.

Sau đó SageMaker AMT sẽ tự tạo nhiều trial. Mỗi trial là một SageMaker Training Job với một cấu hình hyperparameter khác nhau. Khi hoàn tất, mình có thể xem trial nào tốt nhất, model nào tạo ra nó, log ra sao và các giá trị hyperparameter đã được dùng.

## Ví dụ search space với XGBoost

Với XGBoost, có thể cho AMT khám phá các khoảng như:

* `eta` (learning rate): từ 0.1 đến 0.5.
* `alpha` (L1 regularization): từ 0.01 đến 0.5.
* `max_depth`: từ 1 đến 10.
* `min_child_weight`: từ 0 đến 2.

Điểm quan trọng là đừng chỉ lấy “best trial” rồi kết thúc. Phần thú vị hơn là nhìn toàn bộ kết quả.

Nếu những trial có `eta` gần 0.5 thường cho metric tốt hơn, có thể lần chạy sau nên mở rộng vùng này để khám phá tiếp. Nếu `max_depth` chỉ tốt ở một vài mức, ta có thể thu hẹp search space để tránh tốn trial vào những cấu hình kém hiệu quả. HPO vì vậy không chỉ chọn một bộ số tốt, mà còn giúp hiểu model nhạy với hyperparameter nào.

Trong SageMaker, các trial có thể xem ngay trên console như các training job thông thường: hyperparameter, input data, thời gian chạy, CloudWatch logs và metric đều có lịch sử. Điều này tiện khi cần so sánh hoặc giải thích vì sao một model được chọn.

## Áp dụng cho AI Agent Risk Scorer

Với project AI Agent Risk Scorer, đây là điểm rất đáng chú ý: không nên tối ưu chỉ theo accuracy. Nếu mục tiêu là hạn chế bỏ sót trajectory nguy hiểm, `risky recall` hoặc risky false-negative rate sẽ phản ánh rủi ro tốt hơn. Chọn đúng objective metric quan trọng không kém việc chạy nhiều trial.

Cuối cùng, HPO cũng có chi phí vì mỗi trial là một training job. Nên bắt đầu bằng search space có cơ sở, giới hạn số trial bằng `max_jobs`, theo dõi kết quả, rồi chạy vòng tiếp theo với phạm vi tinh gọn hơn. Sau khi chọn model tốt, vẫn cần evaluation, model registry, approval và monitoring trước khi đưa lên production.

Tóm lại, SageMaker AMT không thay thế tư duy ML, nhưng giúp biến việc “thử từng bộ hyperparameter” thành một quy trình có hệ thống, đo được và dễ lặp lại hơn.

## Nguồn tham khảo

- [Optimize hyperparameters with Amazon SageMaker Automatic Model Tuning — AWS](https://aws.amazon.com/blogs/machine-learning/optimize-hyperparameters-with-amazon-sagemaker-automatic-model-tuning/)
- [Explore advanced techniques for hyperparameter optimization with SageMaker AMT — AWS](https://aws.amazon.com/blogs/machine-learning/explore-advanced-techniques-for-hyperparameter-optimization-with-amazon-sagemaker-automatic-model-tuning/)
- [Perform Automatic Model Tuning with SageMaker — AWS Documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning.html)

---

[Quay lại Blogs Posted](../)
