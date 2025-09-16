---
tags:
  - aws
  - service
---
Amazon S3 offers three server-side encryption options:

- **Amazon S3 managed encryption keys (SSE-S3)**: Amazon S3 manages the encryption keys and automatically encrypts and decrypts your data.
- **AWS KMS managed encryption keys (SSE-KMS)**: Leverage customer managed keys or AWS managed keys from AWS KMS to encrypt your S3 objects.
- **Customer-provided encryption keys (SSE-C)**: Encrypt Amazon S3 data by using customer generated encryption keys. This option provides the customer more control over the key management process.