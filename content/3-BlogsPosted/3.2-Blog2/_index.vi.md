---
title: "5 lỗi S3 phổ biến khiến dữ liệu dễ bị lộ"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
# 5 lỗi S3 phổ biến khiến dữ liệu dễ bị lộ

Amazon S3 thường là nơi lưu ảnh, file upload, backup và dữ liệu ứng dụng. Vì dễ dùng, S3 cũng dễ trở thành điểm rủi ro nếu quyền truy cập và khả năng phục hồi không được thiết kế từ đầu. Dưới đây là năm điểm cần kiểm tra trước khi đưa bucket vào production.

## 1. Vô tình để bucket public

Bucket public có thể phù hợp cho website tĩnh hoặc nội dung công khai, nhưng không nên là trạng thái mặc định. Hãy bật **S3 Block Public Access** ở cấp account, sau đó chỉ mở các bucket thực sự cần public. Cách này giúp ngăn policy hoặc ACL cấu hình nhầm làm lộ dữ liệu nội bộ.

## 2. Cấp quyền quá rộng

Hai dấu hiệu cần tránh là `Principal: "*"` trong bucket policy và quyền `s3:*` trong IAM policy khi không cần thiết. Hãy chỉ định rõ principal, action, resource và điều kiện truy cập. Một service chỉ upload file, chẳng hạn, không cần quyền đọc hoặc xóa toàn bộ bucket. Chia quyền đọc, ghi và xóa theo đúng vai trò cũng giảm thiệt hại nếu credential bị lộ hoặc ứng dụng gặp lỗi.

## 3. Không theo dõi hoạt động bất thường

Cấu hình quyền thôi là chưa đủ. CloudTrail data events có thể hỗ trợ biết ai đã truy cập object nào và khi nào. GuardDuty for S3 có thể hỗ trợ phát hiện những dấu hiệu bất thường như truy cập từ vị trí lạ hoặc thay đổi các lớp bảo vệ. Mục tiêu không phải là tạo càng nhiều log càng tốt, mà là có tín hiệu đủ nhanh để điều tra và xử lý sự cố.

## 4. Bỏ qua mã hóa dữ liệu

Dữ liệu trong S3 nên được mã hóa khi lưu trữ. Tùy yêu cầu, có thể sử dụng server-side encryption do S3 quản lý hoặc khóa trong AWS KMS. Với dữ liệu nhạy cảm, cần xác định rõ ai được phép dùng khóa, ai được đọc object và cách kiểm tra quyền này. Mã hóa không thay thế phân quyền, nhưng là một lớp bảo vệ quan trọng.

## 5. Không chuẩn bị cho việc xóa hoặc sửa nhầm

Sự cố không chỉ đến từ tấn công: người dùng hay ứng dụng cũng có thể xóa hoặc sửa nhầm file. Versioning giúp lưu các phiên bản object để có thể khôi phục. Với dữ liệu quan trọng hơn, có thể cân nhắc replication sang bucket hoặc account khác và xây dựng quy trình backup/recovery.

S3 an toàn nhờ nhiều lớp bảo vệ hoạt động cùng nhau: chặn public access, quyền tối thiểu, giám sát, mã hóa và phục hồi dữ liệu. Đây là checklist nhỏ nhưng nên được rà lại mỗi khi tạo bucket mới.

## Hình ảnh minh họa

> **[PLACEHOLDER ẢNH 2]** Chèn infographic gồm một S3 bucket ở giữa, bao quanh bởi 5 lớp: Block Public Access, least privilege, logging/monitoring, encryption và versioning/recovery.
>
> **Nên lấy ảnh ở đâu:** ưu tiên hình trong [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/), hoặc tự dựng sơ đồ bằng các [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/).
>
> **Cách lấy:** nếu dùng ảnh AWS Blog, mở bài nguồn và lưu đúng figure cần dùng, giữ dòng attribution “Source: AWS”. Nếu tự dựng, tải bộ AWS Architecture Icons từ trang AWS, dùng biểu tượng S3, IAM, KMS, CloudTrail và GuardDuty, sau đó xuất PNG. Không lấy infographic từ blog bên thứ ba không nêu license.
>
> **Tên file đề xuất:** `s3-security-checklist.png`.
>
> **Chỗ chèn sau khi có file:** `![Checklist bảo mật Amazon S3](s3-security-checklist.png)`

## Link bài đã đăng

> **[PLACEHOLDER LINK FACEBOOK]** Dán link bài đã đăng trong AWS Study Group vào đây.

## Nguồn tham khảo

- [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/)
- [Security best practices for Amazon S3 — AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
- [IAM Policies and Bucket Policies and ACLs! Oh, My! — AWS Security Blog](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)
