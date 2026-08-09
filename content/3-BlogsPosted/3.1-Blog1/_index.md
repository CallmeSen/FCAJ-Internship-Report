---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# OPTIMIZING AMAZON S3 STORAGE COSTS: STORAGE CLASSES AND LIFECYCLE POLICIES

When I first started learning AWS, I thought Amazon S3 was simply a place to upload files and download them when needed. In practice, S3 also provides a storage tiering model that can significantly reduce operating costs when it is matched to the lifecycle of the data.

This post introduces two features that are especially useful for that purpose: **S3 Storage Classes** and **S3 Lifecycle Policies**.

## The problem: not every file has the same value over time

Consider an S3 bucket that stores application logs, user-uploaded images, and database backups:

* This week's logs may be accessed frequently while debugging.
* Last month's logs may only be needed occasionally.
* Logs from six months ago may be rarely accessed, but still have to be retained for audit purposes.

Keeping every object in S3 Standard for its full lifetime means paying the highest hot-storage rate even when most data is no longer actively used. Understanding the data lifecycle is therefore an important part of controlling cloud costs.

## Main S3 Storage Classes

1. **S3 Standard** is intended for frequently accessed data that needs low latency, such as website assets and active application data.
2. **S3 Standard-Infrequent Access (Standard-IA)** retains fast access while lowering storage cost. It is appropriate for backups and disaster recovery data, but retrieval fees apply.
3. **S3 One Zone-IA** stores data in a single Availability Zone. It costs less than Standard-IA but should only be used for data that can be recreated elsewhere.
4. **S3 Glacier Instant Retrieval** is low-cost storage for infrequently accessed data that still needs millisecond retrieval, such as medical images or media records.
5. **S3 Glacier Flexible Retrieval** offers lower-cost archival storage with retrieval times ranging from minutes to hours, making it suitable for periodic backups.
6. **S3 Glacier Deep Archive** is the lowest-cost option for long-term retention data that is rarely retrieved and can tolerate retrieval times of up to twelve hours.

## Automating data movement with Lifecycle Policies

Objects do not need to be moved manually between storage classes. An S3 Lifecycle Policy can transition them automatically based on age, prefix, or object tags.

A practical rule can look like this:

* Days 0-30: keep objects in S3 Standard for frequent access.
* Days 30-90: transition them to S3 Standard-IA.
* Days 90-180: transition them to S3 Glacier Flexible Retrieval.
* After 365 days: transition them to S3 Glacier Deep Archive.
* After seven years: expire and delete them according to the retention requirement.

This can be configured once in the S3 console or defined as infrastructure as code with Terraform or CloudFormation. No scheduled job or Lambda function is required for the transitions themselves.

## Important considerations

* Each transition has a request cost, so rules should not transition small objects too frequently.
* Objects smaller than 128 KB may not benefit from transitions to IA or Glacier because of minimum billable object sizes.
* Standard-IA and Glacier classes have minimum storage durations. Deleting objects before that duration can still incur charges.
* Lifecycle rules can target prefixes or tags, allowing separate retention rules for paths such as `logs/` and `backups/` in the same bucket.

Amazon S3 is more than a file store. Treating it as tiered storage and designing around the actual lifecycle of data can reduce a significant hidden operating cost before any application code needs to be optimized.

## References

* [Original post on AWS Study Group VN](https://www.facebook.com/share/p/14k93SJMxK5/)
* [Amazon S3 Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html)
* [Managing the lifecycle of objects](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html)
* [S3 Lifecycle configuration elements](https://docs.aws.amazon.com/AmazonS3/latest/userguide/intro-lifecycle-rules.html)
* [Amazon S3 pricing](https://aws.amazon.com/s3/pricing/)
