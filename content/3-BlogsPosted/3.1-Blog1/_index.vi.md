---
title: "Tối ưu chi phí cho web serverless trên AWS"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# Tối ưu chi phí cho web serverless trên AWS

Web application là một trong những trường hợp dùng serverless phổ biến nhất. Mô hình trả tiền theo mức sử dụng có thể hiệu quả, nhưng chi phí vẫn chịu ảnh hưởng trực tiếp từ những quyết định trong kiến trúc. Khi traffic tăng, một API chưa phù hợp, ảnh quá nặng hay Lambda cấu hình theo cảm tính đều có thể làm chi phí tăng không cần thiết.

## Chọn loại API theo nhu cầu

Amazon API Gateway có REST API, WebSocket API và HTTP API. Với nhiều web app, HTTP API đã đáp ứng các nhu cầu thường gặp như tích hợp Lambda, JWT authorization, CORS và custom domain, đồng thời có mô hình triển khai đơn giản hơn. AWS lưu ý HTTP API thường có chi phí thấp hơn REST API; do đó, chỉ nên dùng REST API khi ứng dụng thực sự cần những tính năng riêng của nó.

## Tối ưu lớp phân phối nội dung

CloudFront giúp phân phối HTML, CSS, JavaScript và ảnh tĩnh qua CDN, giảm độ trễ cho người dùng ở xa và giảm tải cho origin. Cần tối ưu asset trước khi đưa lên CDN: thu gọn bundle JavaScript, resize và nén ảnh, hoặc dùng WebP khi phù hợp. Với ảnh do người dùng tải lên, có thể lưu ảnh gốc trong S3 nhưng chỉ phân phối các phiên bản đã resize theo từng vị trí hiển thị. Ít dữ liệu truyền hơn thường đồng nghĩa tốc độ tốt hơn và chi phí truyền dữ liệu thấp hơn.

## Chọn đúng nơi lưu dữ liệu

Dữ liệu nhị phân như ảnh, video và tài liệu nên được tải trực tiếp lên Amazon S3 bằng presigned URL, thay vì đi qua API Gateway hoặc backend. Database chỉ cần lưu metadata và khóa tham chiếu tới object. Với dữ liệu ứng dụng, hãy chọn database theo access pattern: DynamoDB có thể phù hợp với các truy vấn key-value trả tiền theo mức dùng, còn RDS phù hợp với nhu cầu quan hệ dữ liệu nhưng có chi phí compute chạy liên tục.

## Đo Lambda thay vì phỏng đoán

Lambda được tính phí theo request và GB-second. Memory cao hơn cũng cấp thêm CPU, nên một cấu hình memory lớn hơn đôi khi làm hàm chạy nhanh hơn đến mức tổng chi phí lại thấp hơn. Hãy kiểm thử các cấu hình khác nhau với tải gần thực tế trước khi quyết định. Với workflow phức tạp, cũng nên so sánh Standard và Express Workflows của Step Functions theo đặc tính khối lượng công việc.

Tối ưu serverless không phải là cắt bỏ dịch vụ một cách máy móc. Đó là đặt đúng công việc vào đúng lớp: cache nội dung tĩnh, tối ưu asset, đưa file lớn vào object storage, chọn database theo kiểu truy cập và đo Lambda bằng dữ liệu thực tế.

## Hình ảnh minh họa

> **[PLACEHOLDER ẢNH 1]** Chèn sơ đồ kiến trúc web serverless: Browser → CloudFront → S3 (static assets) → API Gateway → Lambda → DynamoDB; nhánh upload ảnh đi thẳng vào S3.
>
> **Nên lấy ảnh ở đâu:** dùng sơ đồ trong bài AWS chính được tham khảo, hoặc dùng sơ đồ web application của AWS tại [AWS Serverless Multi-Tier Architectures](https://docs.aws.amazon.com/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/web-application.html).
>
> **Cách lấy:** mở trang AWS, cuộn đến sơ đồ kiến trúc, bấm vào ảnh để mở lớn (nếu có), sau đó lưu ảnh. Khi đăng/repo, ghi nguồn dưới ảnh: “Source: AWS Documentation”. Không dùng logo hoặc ảnh Google không rõ bản quyền.
>
> **Tên file đề xuất:** `serverless-web-cost-architecture.png`.
>
> **Chỗ chèn sau khi có file:** `![Sơ đồ web serverless tối ưu chi phí](serverless-web-cost-architecture.png)`

## Link bài đã đăng

> **[PLACEHOLDER LINK FACEBOOK]** Dán link bài đã đăng trong AWS Study Group vào đây.

## Nguồn tham khảo

- [Optimizing the cost of serverless web applications — AWS Compute Blog](https://aws.amazon.com/blogs/compute/optimizing-the-cost-of-serverless-web-applications/)
- [Building well-architected serverless applications: Optimizing application costs — AWS Compute Blog](https://aws.amazon.com/blogs/compute/building-well-architected-serverless-applications-optimizing-application-costs/)
- [Web application — AWS Serverless Multi-Tier Architectures](https://docs.aws.amazon.com/whitepapers/latest/serverless-multi-tier-architectures-api-gateway-lambda/web-application.html)
