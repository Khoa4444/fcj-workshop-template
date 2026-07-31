---
title: "Tối ưu Hyperparameter với SageMaker Automatic Model Tuning"
date: 2026-07-30
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

## Thông tin bài viết

| Thông tin | Chi tiết |
|---|---|
| Ngày đăng | 31/07/2026 |
| Trạng thái | Đã đăng |
| Platform | AWS Study Group - Facebook Group |
| Liên kết Facebook | [Xem trên Facebook](https://www.facebook.com/share/p/1GvynuCYcp/) |

![Luồng huấn luyện mô hình với Amazon SageMaker](/images/3-BlogsPosted/sagemaker-automatic-model-tuning.png)

*Hình 1. Amazon SageMaker tạo Training Job từ notebook, dùng dữ liệu trên Amazon S3, lưu model artifact trên S3 và ghi log, metric lên Amazon CloudWatch.*

# Tối ưu Hyperparameter với Amazon SageMaker Automatic Model Tuning: để mô hình tự tìm “điểm ngọt”

Một mô hình machine learning tốt không chỉ đến từ dữ liệu sạch hay thuật toán phù hợp. Có một lớp thiết lập nhỏ nhưng ảnh hưởng rất lớn đến kết quả cuối cùng: **hyperparameter**.

Ví dụ, khi huấn luyện XGBoost, ta phải quyết định learning rate, độ sâu tối đa của cây, hệ số regularization, số vòng lặp huấn luyện… Đây không phải là các tham số mà mô hình tự học từ dữ liệu. Chúng là những “núm vặn” do người làm ML thiết lập trước khi quá trình học bắt đầu. Chọn chưa hợp lý, mô hình có thể học chậm, overfit hoặc cho độ chính xác không như mong muốn.

Vấn đề là: không gian kết hợp của các hyperparameter thường rất lớn. Thử tay từng cấu hình vừa mất thời gian, vừa khó lặp lại, lại nhanh chóng trở thành một công việc tốn kém nếu mỗi lần thử đều cần khởi tạo hạ tầng để huấn luyện.

Đó là lúc **Amazon SageMaker Automatic Model Tuning (AMT)** trở nên hữu ích.

## AMT làm gì?

Thay vì phải tự điều phối hàng chục lần chạy thử, người làm ML chỉ cần chuẩn bị ba thứ:

- Một training job.
- Chỉ số mục tiêu cần tối ưu, chẳng hạn validation accuracy.
- Khoảng giá trị muốn khám phá cho từng hyperparameter.

Sau đó, SageMaker AMT sẽ tạo và điều phối các training job, theo dõi metric, so sánh kết quả và tìm ra tổ hợp hyperparameter tốt hơn. Hạ tầng chạy huấn luyện, container, log, artifact của mô hình và lịch sử thử nghiệm đều được SageMaker quản lý.

## Một ví dụ với XGBoost

Trong bài thực hành của AWS, mô hình XGBoost được dùng để phân loại chữ số viết tay từ 0 đến 9. Dữ liệu train và validation được đưa lên Amazon S3; SageMaker lấy image XGBoost có sẵn, khởi tạo máy huấn luyện và lưu model sau khi chạy xong.

Ban đầu, ta có thể chạy một training job đơn lẻ để kiểm tra pipeline. Tiếp theo, thay vì cố định mọi giá trị, ta định nghĩa các khoảng cần tìm kiếm, ví dụ:

- `alpha`: từ 0,01 đến 0,5.
- `eta` (learning rate): từ 0,1 đến 0,5.
- `min_child_weight`: từ 0 đến 2.
- `max_depth`: số nguyên từ 1 đến 10.

AMT sẽ lấy mẫu những tổ hợp khác nhau trong không gian này, chạy mô hình và đo `validation:accuracy`. Với mục tiêu là tối đa hóa accuracy, mỗi lần chạy trở thành một thí nghiệm có dữ liệu rõ ràng thay vì một lần “đoán thông số”.

## Vì sao chiến lược Bayesian đáng chú ý?

Ví dụ này sử dụng chiến lược tìm kiếm **Bayesian**. Điểm hay của nó là các lần thử sau có thể tận dụng kết quả của các lần thử trước để ưu tiên những vùng có triển vọng trong không gian hyperparameter.

Trong bài demo, 50 trial được thực hiện với tối đa 3 job chạy song song. Trial tốt nhất đạt validation accuracy xấp xỉ **89,815%**. Nhưng giá trị quan trọng hơn không chỉ là “cấu hình tốt nhất”. Khi trực quan hóa tất cả trial, ta còn thấy được xu hướng:

- Giá trị `eta` gần mức cao trong khoảng đã thử cho kết quả tốt hơn các giá trị gần 0.
- `alpha` lại có xu hướng ngược lại.
- `max_depth` chỉ hoạt động tốt trong một số vùng giá trị nhất định.

Những quan sát này giúp đội ngũ ML không dừng lại ở một con số tối ưu tạm thời. Họ có thể thu hẹp hoặc mở rộng khoảng tìm kiếm cho vòng tối ưu tiếp theo, đồng thời hiểu rõ hơn mô hình nhạy với hyperparameter nào.

## Bài học thực tế

Hyperparameter tuning không nên được xem là bước phụ sau khi đã có mô hình. Đây là một phần của quá trình phát triển ML có kỷ luật:

1. Chọn metric phản ánh đúng mục tiêu kinh doanh hoặc kỹ thuật.
2. Bắt đầu với khoảng tìm kiếm dựa trên hiểu biết về thuật toán.
3. Theo dõi từng trial, chi phí và log huấn luyện.
4. Trực quan hóa kết quả để học từ cả vùng tốt lẫn vùng kém hiệu quả.
5. Tinh chỉnh lại không gian tìm kiếm ở các vòng sau.

SageMaker AMT không thay thế tư duy của người làm ML. Nó giảm phần việc vận hành và thử nghiệm lặp lại, để chúng ta tập trung vào các quyết định quan trọng hơn: dữ liệu có đủ tốt không, metric có đúng không, khoảng giá trị đặt ra có hợp lý không, và mô hình đang học được điều gì.

Nếu đang dùng AWS để xây dựng pipeline machine learning, đây là một cách đáng cân nhắc để biến việc “vặn núm” thủ công thành một quy trình có hệ thống, dễ theo dõi và có thể mở rộng.

## Nguồn tham khảo

- [Optimize hyperparameters with Amazon SageMaker Automatic Model Tuning — AWS](https://aws.amazon.com/blogs/machine-learning/optimize-hyperparameters-with-amazon-sagemaker-automatic-model-tuning/)
- [Explore advanced techniques for hyperparameter optimization with SageMaker AMT — AWS](https://aws.amazon.com/blogs/machine-learning/explore-advanced-techniques-for-hyperparameter-optimization-with-amazon-sagemaker-automatic-model-tuning/)
- [Perform Automatic Model Tuning with SageMaker — AWS Documentation](https://docs.aws.amazon.com/sagemaker/latest/dg/automatic-model-tuning.html)

---

[Quay lại Blogs Posted](../)
