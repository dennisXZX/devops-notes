### RDS (Amazon Relational Database Service)

OLTP (Online Transaction Processing) - for example, you retrieve or insert a row of data such as name, date and address. RDS falls under this category.

OLAP (Online Analytics Processing) - for example, calculating the net profit for a region.

There are two different types of backups, automated backups and database snapshots. Automated backups allows you to recover your database to any point in time within a retention period. DB snapshots are done manually. They are stored even after you delete the original RDS instance, unlike automated backups.

Encryption at rest is done using AWS Key Management Service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshots. SSL certificates can be used to encrypt data to RDS in flight.

Read replica (asynchronous replication, so reads are eventually consistent ) is for scaling, while multi-AZ (synchronous replication) is for disaster recovery. When you enable RDS Multi AZ, your application will always communicate with your RDS via one DNS name, when the RDS Master DB instance fails, it would automatically switch to a standby RDS DB instance. No manual intervention is required.
