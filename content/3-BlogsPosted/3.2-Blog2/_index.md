---
title: "Five Common S3 Mistakes That Can Expose Data"
date: 2026-07-29
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

## Post details

| Information | Details |
|---|---|
| Publication date | 29/07/2026 |
| Status | Published |
| Platform | AWS Study Group - Facebook Group |
| Published post | [View on Facebook](https://www.facebook.com/share/p/1BhVcvncyh/) |

Amazon S3 commonly stores images, uploaded files, backups, and application data. Because it is easy to use, S3 can also become a risk point when access and recovery are not designed from the beginning.

Here are five areas to check before putting a bucket into production.

## 1. Accidentally making a bucket public

A public bucket can be suitable for a static website or public content, but it should not be the default state. Enable **S3 Block Public Access** at the account level, then open only buckets that truly need public access. This helps prevent a misconfigured policy or ACL from exposing internal data.

## 2. Granting permissions that are too broad

Two warning signs are `Principal: "*"` in a bucket policy and `s3:*` in an IAM policy when they are unnecessary. Instead, specify the exact principal, action, resource, and required access conditions. For example, a service that only uploads files does not need permission to read or delete an entire bucket.

Separating read, write, and delete permissions by role also reduces damage if credentials are exposed or an application fails.

## 3. Not monitoring unusual activity

Access configuration alone is not enough. Enable suitable data logging so that you can identify who accessed which object and when. CloudTrail data events can support incident investigation, while GuardDuty for S3 can help detect suspicious behavior such as access from unusual locations or changes to protection controls.

The objective is not to produce as many logs as possible, but to receive signals quickly enough to detect and handle incidents.

## 4. Ignoring data encryption

S3 data should be encrypted at rest. Depending on the requirement, use S3-managed server-side encryption or keys in AWS KMS. For sensitive data, identify who may use the key, who may read the object, and how those permissions are reviewed.

Encryption does not replace authorization, but it is an important protection layer when data or data copies are accessed incorrectly.

## 5. Not preparing for accidental deletion or modification

Incidents do not come only from attacks: users or applications can delete or change files by mistake. Versioning preserves object versions so that they can be restored. For more important data, consider replication to another bucket or account and establish a backup and recovery process.

S3 is secure not because there is one correct setting, but because several protection layers work together: blocking public access, least privilege, monitoring, encryption, and data recovery. This is a small checklist that should be revisited whenever a new bucket is created.

## References

- [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/)
- [Security best practices for Amazon S3 — AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
- [IAM Policies and Bucket Policies and ACLs! Oh, My! — AWS Security Blog](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)
- [Modern data protection architecture on Amazon S3 — AWS Storage Blog](https://aws.amazon.com/blogs/storage/modern-data-protection-architecture-on-amazon-s3-part-1/)

---

[Back to Blogs Posted](../)
