### S3 (Simple Storage Service)

- S3 is object based, which allows you to upload files (up to 5TB per file). S3 is a universal namespace, which means names must be unique globally.

- A bucket is just like a folder, which needs to be unique globally. Each bucket you create would have a URL.

- When you upload a file to S3, you will receive an HTTP 200 code if the upload was successful.

- Read after Write consistency for PUTS of new objects, eventual consistency for overwrite PUTS and DELETES (can take some time to propagate)

#### S3 storage Classes

- S3 Standard: stored redundantly across multiple devices in multiple faciities, and is designed to sustain the loss of 2 facilities concurrently.

- S3 - IA (Infrequently Accessed): For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.

- S3 One Zone - IA: For where you want a lower-cost option for infrequently accessed data, but do not require the multiple Availability Zone data resilience.

- S3 - Intelligent Tiering: Designed to optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead.

- S3 Glacier: S3 Glacier is a secure, durable and low-cost storage class for data archiving. You can reliably store any amount of data at costs that are competitive with or cheaper than on-premises solutions. Retrieval times configurable from minutes to hours.

- S3 Glacier Deep Archive: S3 Glacier Deep Archive is Amazon's S3's lowest-cost storage class where a retrieval time of 12 hours is acceptable.

#### Encryption

Encryption in Transit is achieved by SSL/TLS. (TLS is the new name for SSL)

Encryption At Rest (Server Side) is provided by AWS.

#### Versioning

- Stores all versions of an object (including all writes and even if you delete an object)

- Versioning's MFA Delete capability, which uses multi-factor authentication

#### Cross Region Replication

Cross region replication means you want to copy the content of a bucket in one region to another one.

- Versioning must be enabled on both the source and destination buckets

- Files in an existing bucket are not replicated automatically. You need to copy them using command line `aws s3 cp --recursive s3://testbucket-by-dennis-versioning s3://test-by-dennis-replication-sydney`. All subsequent updated files will be replicated automatically

- Delete markers are NOT replicated

#### Lifecycle Management

- Can be used in conjunction with versioning

- Can be applied to current versions and previous versions

- Transition to the Standard - Infrequent Access (IA) Storage Class 30 days after creation date, archive to Glacier Storage Class 30 days after IA.