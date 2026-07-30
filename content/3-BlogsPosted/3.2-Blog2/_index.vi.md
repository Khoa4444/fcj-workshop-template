---
title: "5 lỗi S3 phổ biến khiến dữ liệu dễ bị lộ"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

## Thông tin bài viết

| Thông tin | Chi tiết |
|---|---|
| Ngày đăng | Sẽ cập nhật |
| Trạng thái | Đã đăng |
| Platform | AWS Study Group - Facebook Group |
| Bài viết đã đăng | [Xem trên Facebook](https://www.facebook.com/share/p/1BhVcvncyh/) |

Amazon S3 thường là nơi lưu ảnh, file upload, backup và dữ liệu ứng dụng. Chính vì dễ dùng, S3 cũng dễ trở thành điểm rủi ro nếu quyền truy cập và khả năng phục hồi không được thiết kế từ đầu.

Dưới đây là 5 điểm nên kiểm tra trước khi đưa bucket vào production.

## 1. Vô tình để bucket public

Một bucket public có thể phù hợp khi lưu website tĩnh hoặc nội dung công khai, nhưng không nên là trạng thái mặc định. Hãy bật **S3 Block Public Access** ở cấp account, sau đó chỉ mở các bucket thực sự cần public. Cách này giúp ngăn một policy hoặc ACL cấu hình nhầm làm dữ liệu nội bộ bị lộ.

## 2. Cấp quyền quá rộng

Hai dấu hiệu cần tránh là `Principal: "*"` trong bucket policy và quyền `s3:*` trong IAM policy khi không cần thiết. Thay vào đó, hãy chỉ định rõ principal, action, resource và điều kiện truy cập cần thiết. Ví dụ, một service chỉ upload file thì không cần quyền đọc hoặc xóa toàn bộ bucket.

Chia quyền đọc, ghi và xóa theo đúng vai trò cũng giúp giảm thiệt hại nếu credential bị lộ hoặc một ứng dụng bị lỗi.

## 3. Không theo dõi các hoạt động bất thường

Chỉ cấu hình quyền là chưa đủ. Hãy bật log dữ liệu phù hợp để biết ai đã truy cập object nào và khi nào. CloudTrail data events có thể hỗ trợ điều tra sự cố; GuardDuty for S3 hỗ trợ phát hiện hành vi đáng ngờ, như truy cập từ vị trí bất thường hoặc thay đổi các lớp kiểm soát bảo vệ.

Mục tiêu không phải tạo thật nhiều log, mà là có tín hiệu đủ nhanh để phát hiện và xử lý sự cố.

## 4. Bỏ qua mã hóa dữ liệu

Dữ liệu trong S3 nên được mã hóa khi lưu trữ. Tùy yêu cầu, có thể dùng server-side encryption do S3 quản lý hoặc khóa trong AWS KMS. Với dữ liệu nhạy cảm, hãy xác định rõ ai được phép dùng khóa, ai được đọc object và quy trình kiểm tra quyền này.

Mã hóa không thay thế phân quyền, nhưng là một lớp bảo vệ quan trọng nếu dữ liệu hoặc bản sao dữ liệu bị truy cập sai cách.

## 5. Không chuẩn bị cho việc xóa nhầm hoặc bị sửa dữ liệu

Sự cố không chỉ đến từ tấn công: người dùng hoặc ứng dụng cũng có thể xóa/sửa nhầm file. Versioning giúp lưu các phiên bản object để có thể khôi phục. Với dữ liệu quan trọng hơn, có thể cân nhắc replication sang bucket hoặc account khác và xây dựng quy trình backup/recovery.

S3 an toàn không phải vì chỉ có một cài đặt đúng, mà vì có nhiều lớp bảo vệ hoạt động cùng nhau: chặn public access, quyền tối thiểu, giám sát, mã hóa và phục hồi dữ liệu. Đó là checklist nhỏ nhưng nên được rà lại mỗi khi tạo bucket mới.

## Nguồn tham khảo

- [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/)
- [Security best practices for Amazon S3 — AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
- [IAM Policies and Bucket Policies and ACLs! Oh, My! — AWS Security Blog](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)
- [Modern data protection architecture on Amazon S3 — AWS Storage Blog](https://aws.amazon.com/blogs/storage/modern-data-protection-architecture-on-amazon-s3-part-1/)


---

[Quay lại Blogs Posted](../)
