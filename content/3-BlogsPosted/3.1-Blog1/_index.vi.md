---
title: "Tối ưu chi phí cho web serverless trên AWS"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

## Thông tin bài viết

| Thông tin | Chi tiết |
|---|---|
| Ngày đăng | Sẽ cập nhật |
| Trạng thái | Đã đăng |
| Platform | AWS Study Group - Facebook Group |
| Bài viết đã đăng | [Xem trên Facebook](https://www.facebook.com/share/p/18deroGCqx/) |

Web application là một trong những trường hợp dùng serverless phổ biến nhất. Mô hình trả tiền theo mức sử dụng có thể rất hiệu quả, nhưng chi phí vẫn chịu ảnh hưởng trực tiếp từ những quyết định trong kiến trúc. Khi traffic tăng, một API chưa phù hợp, ảnh quá nặng hay Lambda cấu hình theo cảm tính đều có thể làm chi phí tăng không cần thiết.

Dưới đây là những điểm nên kiểm tra khi tối ưu một web app serverless.

## Chọn loại API theo nhu cầu

Amazon API Gateway có REST API, WebSocket API và HTTP API. Với nhiều web app, HTTP API đã có những khả năng thường cần như tích hợp Lambda, JWT authorization, CORS và custom domain, đồng thời có mô hình triển khai đơn giản hơn. AWS cho biết HTTP API thường có chi phí thấp hơn REST API; vì vậy, trước khi dùng REST API, hãy xác định ứng dụng có cần các tính năng đặc thù của REST API hay không.

## Tối ưu lớp phân phối nội dung

CloudFront giúp phân phối nội dung qua CDN, giảm độ trễ cho người dùng ở xa và giảm tải cho các thành phần phía sau. Với các ứng dụng một trang như React hoặc Vue, các file HTML, CSS, JavaScript và ảnh tĩnh rất phù hợp để được phân phối qua CDN.

Tuy nhiên, cần tối ưu chính các asset trước khi đưa lên CDN. Bundle JavaScript có thể được thu gọn; ảnh có thể được resize, nén hoặc chuyển sang định dạng hiệu quả hơn như WebP khi phù hợp. Công cụ như Lighthouse có thể giúp tìm những ảnh quá lớn cho giao diện.

Với ảnh do người dùng tải lên, đây càng là điểm cần lưu ý. Ảnh từ điện thoại có thể 3–9 MB nhưng không cần hiển thị với độ phân giải đó trong web app. Một hướng hợp lý là giữ ảnh gốc trong S3, tạo các phiên bản đã resize cho từng vị trí hiển thị, rồi chỉ phân phối phiên bản cần thiết. Ít dữ liệu truyền hơn giúp giảm cả chi phí truyền dữ liệu lẫn chi phí CloudFront.

## Chọn đúng nơi lưu dữ liệu

S3 thường phù hợp và tiết kiệm hơn database cho dữ liệu nhị phân như ảnh, video và tài liệu. Thay vì cho file đi qua API Gateway hoặc backend, ứng dụng có thể dùng presigned URL để upload thẳng vào S3. Nếu dùng DynamoDB, hãy lưu object lớn trong S3 và chỉ lưu khóa hoặc tham chiếu đến object trong bảng.

Với dữ liệu ứng dụng, lựa chọn database nên xuất phát từ cách dữ liệu được truy cập. DynamoDB tính phí theo mức sử dụng và lưu trữ, nên có thể phù hợp với nhiều web app. RDS vẫn phù hợp cho nhu cầu quan hệ dữ liệu, nhưng chi phí gồm cả compute instance hàng tháng. Không có lựa chọn nào luôn rẻ hơn: access pattern mới là yếu tố quyết định.

## Tối ưu logic và workflow

Lambda được tính phí theo số request và GB-second — tức thời gian chạy nhân với dung lượng memory cấp cho hàm. Memory cao hơn đồng thời cấp thêm CPU, vì vậy một cấu hình memory lớn hơn đôi khi làm hàm chạy nhanh đến mức tổng chi phí lại thấp hơn. Hãy đo với các cấu hình khác nhau thay vì chỉ chọn mức memory thấp nhất. AWS Lambda Power Tuning có thể hỗ trợ so sánh chi phí và thời gian chạy giữa các mức memory.

Nếu ứng dụng có workflow phức tạp, AWS Step Functions giúp điều phối các bước thay vì tự viết nhiều đoạn code điều phối. Standard Workflows tính theo state transition, còn Express Workflows tính theo request và duration. Với luồng sự kiện có khối lượng lớn và thời gian xử lý ngắn, Express Workflows có thể là phương án đáng so sánh về chi phí.

Serverless tiết kiệm nhất khi kiến trúc phù hợp với loại tải: chọn API đúng nhu cầu, phân phối và tối ưu asset hiệu quả, để file lớn vào S3, chọn database theo access pattern và đo Lambda trước khi chốt cấu hình. Tối ưu ở từng lớp nhỏ sẽ tạo khác biệt rõ rệt khi lượng người dùng tăng lên.

![Kiến trúc web serverless trên AWS](/images/3-BlogsPosted/serverless-cost-architecture.png)

*Hình 1. Các lớp chính của một web application serverless trên AWS.*

## Nguồn tham khảo

- [Optimizing the cost of serverless web applications — AWS Compute Blog](https://aws.amazon.com/blogs/compute/optimizing-the-cost-of-serverless-web-applications/)
- [Building well-architected serverless applications: Optimizing application costs — AWS Compute Blog](https://aws.amazon.com/blogs/compute/building-well-architected-serverless-applications-optimizing-application-costs/)
- [Understanding techniques to reduce AWS Lambda costs in serverless applications — AWS Compute Blog](https://aws.amazon.com/blogs/compute/understanding-techniques-to-reduce-aws-lambda-costs-in-serverless-applications/)
- [Web application — AWS Serverless Multi-Tier Architectures](https://docs.aws.amazon.com/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/web-application.html)


---

[Quay lại Blogs Posted](../)
