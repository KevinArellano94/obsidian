---
tags:
  - aws
  - service
---
When you create a SageMaker notebook instance, training job, or other SageMaker resource that involves the storage of data, you can **specify that an AWS KMS key be used for encrypting the data at rest**. SageMaker automatically uses the specified AWS KMS key to encrypt the data before storing it on the underlying storage media.