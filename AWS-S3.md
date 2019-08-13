### S3 (Simple Storage Service)

- S3 is object based, which allows you to upload files (up to 5TB per file). S3 is a universal namespace, which means S3 bucket names must be unique globally.

- A bucket is just like a folder, which needs to be unique globally. Each bucket you create would have a URL.

- When you upload a file to S3, you will receive an `HTTP 200 status code` if the upload was successful.

- You can turn on `MFA Delete`, so user cannot accidentally delete files in an S3 bucket.

- Read after Write consistency for PUTS of new objects, eventual consistency for overwrite PUTS and DELETES (can take some time to propagate)

- You are charged for S3 by `storage`, `requests`, `storage management pricing` (different storage tiers), `data transfer pricing`, `transfer acceleration` and `cross region replication pricing`.

#### S3 storage Classes

- S3 Standard: stored redundantly across multiple devices in multiple facilities, and is designed to sustain the loss of 2 facilities concurrently.

- S3 - IA (Infrequently Accessed): For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.

- S3 One Zone - IA: For where you want a lower-cost option for infrequently accessed data, but do not require the multiple Availability Zone data resilience.

- S3 - Intelligent Tiering: Designed to optimize costs by automatically moving data to the most cost-effective access tier, without performance impact or operational overhead.

- S3 Glacier: S3 Glacier is a secure, durable and low-cost storage class for data archiving. You can reliably store any amount of data at costs that are competitive with or cheaper than on-premises solutions. Retrieval times configurable from minutes to hours.

- S3 Glacier Deep Archive: S3 Glacier Deep Archive is Amazon's S3's lowest-cost storage class where a retrieval time of 12 hours is acceptable.

#### Encryption

Encryption in Transit is achieved by SSL (Secure Sockets Layer) or TLS (Transport Layer Security). TLS is the new name for SSL.

Encryption At Rest (Server Side Encryption) is provided by AWS.

#### Versioning

- Stores all versions of an object (including all writes and even if you delete an object)

- Once enabled, versioning cannot be disabled, only suspended

- Versioning's MFA Delete capability, which uses multi-factor authentication to add additional layer of security

#### Lifecycle Management

- Automate moving your objects between different storage tiers

- Can be used in conjunction with versioning

- Can be applied to current versions and previous versions

#### Cross Region Replication

Cross region replication means you want to copy the content of a bucket in one region to another one.

- Versioning must be enabled on both the source and destination buckets

- Files in an existing bucket are not replicated automatically. You need to copy them using command line `aws s3 cp --recursive s3://originBucketName s3://replicationBucketName`. All subsequent updated files will be replicated automatically

- Delete markers are NOT replicated
