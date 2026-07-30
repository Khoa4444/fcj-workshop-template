---
title: "Five Common S3 Mistakes That Can Expose Data"
date: 2026-07-30
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Five Common S3 Mistakes That Can Expose Data

Amazon S3 commonly stores images, uploads, backups, and application data. Because it is easy to use, it can also become a risk point when access and recovery are not designed from the beginning. Here are five checks to make before placing a bucket in production.

## 1. Accidentally making a bucket public

A public bucket can be appropriate for a static website or public content, but it should not be the default. Enable **S3 Block Public Access** at the account level and then open only buckets that genuinely need public access. This helps prevent an incorrect policy or ACL from exposing internal data.

## 2. Granting permissions that are too broad

Two warning signs are `Principal: "*"` in a bucket policy and `s3:*` in an IAM policy when they are not necessary. Specify the principal, action, resource, and access conditions precisely. A service that only uploads files, for example, does not need permission to read or delete an entire bucket. Separating read, write, and delete privileges by role also reduces damage if credentials are exposed or an application fails.

## 3. Not monitoring unusual activity

Access configuration alone is not enough. CloudTrail data events can show who accessed which object and when. GuardDuty for S3 can help identify unusual signals such as access from unfamiliar locations or changes to protection layers. The objective is not to create as many logs as possible; it is to have signals quickly enough to investigate and respond.

## 4. Ignoring encryption

S3 data should be encrypted at rest. Depending on requirements, use S3-managed server-side encryption or keys in AWS KMS. For sensitive data, identify who may use the key, who may read the object, and how those permissions are reviewed. Encryption does not replace authorization, but it is an important protection layer.

## 5. Not preparing for accidental deletion or modification

Incidents do not come only from attacks: users and applications can delete or change files by mistake. Versioning preserves object versions so they can be recovered. For more critical data, consider replication to another bucket or account and establish a backup and recovery process.

S3 is secure when multiple layers work together: block public access, least privilege, monitoring, encryption, and data recovery. This is a small checklist, but it should be revisited whenever a new bucket is created.

## Illustrative image

> **[IMAGE PLACEHOLDER 2]** Insert an infographic with an S3 bucket in the center and five layers around it: Block Public Access, least privilege, logging/monitoring, encryption, and versioning/recovery.
>
> **Suggested source:** [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/) or a diagram created with [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/).
>
> **Suggested filename:** `s3-security-checklist.png`.
>
> **Insertion point after adding the file:** `![Amazon S3 security checklist](s3-security-checklist.png)`

## Published-post link

> **[FACEBOOK LINK PLACEHOLDER]** Paste the AWS Study Group post link here.

## References

- [Top 10 security best practices for securing data in Amazon S3 — AWS Security Blog](https://aws.amazon.com/blogs/security/top-10-security-best-practices-for-securing-data-in-amazon-s3/)
- [Security best practices for Amazon S3 — AWS Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
- [IAM Policies and Bucket Policies and ACLs! Oh, My! — AWS Security Blog](https://aws.amazon.com/blogs/security/iam-policies-and-bucket-policies-and-acls-oh-my-controlling-access-to-s3-resources/)
