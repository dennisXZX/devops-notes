### ElastiCache

ElasticCache is a managed in-memory database with high performance and low latency. ElasticCache is helpful for read-heavy application (social networks, gaming, media sharing, Q&A portals), as well as compute-intensive workloads (recommendation engines).

ElastiCache use cases:

- DB Cache

Applications queries data from ElastiCache first, if the data is not available in ElasticCache, the app gets the data from RDS and writes it to ElastiCache. This helps relieve load in RDS. Cache must have an invalidation strategy to make sure only the most current data is used in there.

- User Session Store

There are a bunch of applications running in multiple EC2 instances (within Auto Scaling Group). User logs into any of the application, the application then writes the session data into ElastiCache. When the user hits another application, the application retrieves the session data from ElastiCache to check whether the user is already logged in.

__Cache strategies__

Lazy Loading

App first queries the ElastiCache, if it's a cache hit, we get the data. If it's a cache miss, the app will read the data from database, then writes the data to ElastiCache.

Pros: 

- Only requested data is cached (cache isn't filled up with unused data)
- ElastiCache node failures are not fatal

Cons:
- cache miss penalty that results in 3 round trips, noticeable delay for that request
- stale data could exist, data can be updated in database and outdated in the cache

Write Through

App will first write data to database, then also to ElastiCache.

Pros: 

- Data in cache is never stale

Cons:
- write penalty (each write requires 2 calls)
- missing data until it's added/updated in the database
- a lot of data will never be read in cache

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
