### ElastiCache

__memcached__ (doesn't support multi-AZ)

Use cases:
  - object caching is your primary goal, for example, to offload your database
  - you are interested in a simple caching model
  - you are planning on running large cache nodes and require multithreaded performance with utilization of multiple cores
  - you want the ability to scale your cache horizontally as you grow

__redis__ (supports multi-AZ)

Use cases:
  - you are looking for more advanced data types, such as lists, hashes and sets
  - sorting and ranking datasets in memory help you, such as leaderboards
  - persistence of your in-memory key store is important
  - you want to run in multiple AWS Availability Zones with failover
