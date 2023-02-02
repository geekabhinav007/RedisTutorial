# Redis Basic

## Is redis is No SQL?

Yes, Redis is considered a NoSQL database. Unlike traditional relational databases, which use a structured query language (SQL) to manage and manipulate data stored in tables with fixed columns and rows, NoSQL databases like Redis use a key-value data model and can store data in various formats, including hashes, lists, sets, and sorted sets.

Redis offers flexibility and scalability, allowing you to store and retrieve data quickly and easily without the need to define a schema upfront. Additionally, Redis supports complex data structures and operations, making it suitable for a wide range of use cases, from caching and real-time analytics to message queuing and pub/sub communication.

## Redis Store Data on Ram unlike other databases

Redis is an in-memory database, which means that it stores data in RAM instead of on disk. This provides several benefits and drawbacks compared to other databases that primarily store data on disk, such as relational databases and other NoSQL databases.

### Benefits of using Redis as an in-memory database

1. Speed: Since Redis stores data in RAM, accessing and manipulating data is extremely fast compared to disk-based databases. This makes Redis well-suited for applications that require low latency, such as real-time analytics, leaderboards, and gaming.

1. Scalability: Redis is highly scalable and can handle a large amount of data. It can also easily handle high-concurrency workloads due to its multithreaded architecture.

1. Flexibility: Redis supports a wide range of data structures and operations, making it suitable for a variety of use cases, including caching, message queuing, pub/sub communication, and more.

### Drawbacks of using Redis as an in-memory database and Advantage of Redis.

1. Cost: Since Redis stores all data in RAM, it can be more expensive than disk-based databases, especially for large datasets.

1. Limitations on data size: The amount of data that can be stored in Redis is limited by the amount of available RAM. If you have a large dataset, you may need to shard your data across multiple Redis instances or consider using a disk-based database.

1. Persistence: By default, Redis does not persist data to disk, which means that if the Redis instance crashes or is restarted, all data stored in RAM will be lost. However, Redis provides several options for persistence, such as snapshots and AOF (Append-Only File), to mitigate this issue.

