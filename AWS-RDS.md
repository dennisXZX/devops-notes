### RDS (Amazon Relational Database Service)

OLTP (Online Transaction Processing) - pulls up or insert a row of data such as name, date and address.

OLAP (Online Analytics Processing) - calculates the net profit for a region.

There are two different types of backups, automated backups and database snapshots. Automated backups allows you to recover your database to any point in time within a retention period. DB snapshots are done manually. THey are stored even after you delete the original RDS instance, unlike automated backups.

Encryption at rest is done using AWS Key Management Service. Once your RDS instance is encrypted, the data stored at rest in the underlying storage is encrypted, as are its automated backups, read replicas and snapshots.

Read replica (asynchronous replication) is for scaling, while multi-AZ (synchronous replication) is for disaster recovery.
