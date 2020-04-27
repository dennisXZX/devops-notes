### ElastiCache

ElasticCache is a managed in-memory database with high performance and low latency.

ElastiCache use cases:

- DB Cache

Applications queries data from ElastiCache first, if the data is not available in ElasticCache, the app gets the data from RDS and writes it to ElastiCache. This helps relieve load in RDS. Cache must have an invalidation strategy to make sure only the most current data is used in there.

- User Session Store

There are a bunch of applications running in multiple EC2 instances (within Auto Scaling Group). User logs into any of the application, the application then writes the session data into ElastiCache. When the user hits another application, the application retrieves the session data from ElastiCache to check whether the user is already logged in.

#### Cluster engine

__memcached__ (doesn't support multi-AZ)

Use cases:
  - object caching is your primary goal, for example, to offload your database
  - you are interested in a simple caching model

__redis__ (supports multi-AZ)

Use cases:
  - you are looking for more advanced data types, such as lists, hashes and sets
  - sorting and ranking datasets in memory, such as leaderboards
  - cache survive reboots (persistence of your in-memory)
  - you want to run in multiple AWS Availability Zones with failover
