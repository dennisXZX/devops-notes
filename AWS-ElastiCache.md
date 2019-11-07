### ElastiCache

ElastiCache use cases:

- DB Cache

Applications queries data from ElastiCache first, if the data is not available, get from RDS and store in ElastiCache. This helps relieve load in RDS. Cache must have an invalidation strategy to make sure only the most current data is used in there.

- User Session Store

There are a bunch of applications running (Auto Scaling Group), user logs into any of the application. The application then writes the session data into ElastiCache. When the user hits another application, the application retrieves the session data from ElastiCache and the user is already logged in.

#### Cluster engine

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
