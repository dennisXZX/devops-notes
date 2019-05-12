### S3 (Simple Storage Service)

- S3 is object based, which allows you to upload files (up to 5TB per file)

- A bucket is just like a folder, which needs to be unique globally. Each bucket you create would have a URL.

- When you upload a file to S3, you will receive an HTTP 200 code if the upload was successful.

- Read after Write consistency for PUTS of new objects, eventual consistency for overwrite PUTS and DELETES (can take some time to propagate)

#### S3 storage Classes

- S3 Standard: stored redundantly across multiple devices in multiple faciities, and is designed to sustain the loss of 2 facilities concurrently.

- S3 - IA (Infrequently Accessed): For data that is accessed less frequently, but requires rapid access when needed. Lower fee than S3, but you are charged a retrieval fee.

#### Cross Region Replication

- Versioning must be enabled on both the source and destination buckets

- Files in an existing bucket are not replicated automatically. You need to copy them using command line `aws s3 cp --recursive s3://testbucket-by-dennis-versioning s3://test-by-dennis-replication-sydney`. All subsequent updated files will be replicated automatically

- Delete markers are NOT replicated

#### Lifecycle Management

- Can be used in conjunction with versioning

- Can be applied to current versions and previous versions

- Transition to the Standard - Infrequent Access (IA) Storage Class 30 days after creation date, archive to Glacier Storage Class 30 days after IA.
