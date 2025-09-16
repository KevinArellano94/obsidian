---
tags:
  - aws
  - service
---
If your machine learning workflow involves storing data in a relational database, you can use Amazon RDS to protect your data at rest. You can use customer managed keys or AWS managed keys to encrypt your database instances, automated instances, and read replicas.

**Enabling RDS encryption** allows all new data written to the underlying storage to be encrypted. Existing unencrypted data can be encrypted by performing a point-in-time restore to a new, encrypted DB instance.