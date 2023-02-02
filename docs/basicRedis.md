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

### Drawbacks of using Redis as an in-memory database and Advantage of Redis

1. Cost: Since Redis stores all data in RAM, it can be more expensive than disk-based databases, especially for large datasets.

1. Limitations on data size: The amount of data that can be stored in Redis is limited by the amount of available RAM. If you have a large dataset, you may need to shard your data across multiple Redis instances or consider using a disk-based database.

1. Persistence: By default, Redis does not persist data to disk, which means that if the Redis instance crashes or is restarted, all data stored in RAM will be lost. However, Redis provides several options for persistence, such as snapshots and AOF (Append-Only File), to mitigate this issue.

## Basic Redis Commands that I used for intial learning

```bash
$ SET name "Kumar Abhinav"
OK

$ GET name
"Kumar Abhinav"

```

The GETRANGE command in Redis is used to retrieve a substring of a string value stored at a specified key:

```bash
$ GETRANGE key start end

127.0.0.1:6379> getrange email 0 6

"example"
```

`start end both inclusive`

`THE MGET and MSET` commands in Redis are used to set multiple key-value pairs and retrieve the values of multiple keys, respectively.

```bash
127.0.0.1:6379> MSET age 21 domain IT
OK
127.0.0.1:6379> MGET name email age 
1) "Kumar Abhinav"
2) "example@gmail.com"
3) "21"
```

The Redis STRLEN command returns the length of the string value stored at a specified key.

If the key is not present it will give you length `0`.

```bash
127.0.0.1:6379> strlen email
(integer) 17
```

The `INCR`, `INCRBY`, `DECR`, and `DECRBY` commands in Redis are used to increment and decrement the value of a key that holds a string representing a number.

The `INCR` command increments the value of a key by 1. `If the key does not exist, it is set to 0 before the increment operation is performed.`

The `INCRBY` command increments the value of a key by a specified increment value. If the key does not exist, it is set to 0 before the increment operation is performed.

Similar for `DECR` and `DECRBY`

```bash
127.0.0.1:6379> set count 1
OK
127.0.0.1:6379> get count
"1"
127.0.0.1:6379> incr count
(integer) 2
127.0.0.1:6379> incrby count 5
(integer) 7
127.0.0.1:6379> get count
"7"
127.0.0.1:6379> decr count
(integer) 6
127.0.0.1:6379> decrby count 5
(integer) 1
127.0.0.1:6379> get count
"1"
127.0.0.1:6379> incr newcount
(integer) 1
127.0.0.1:6379> get newcount
"1"
127.0.0.1:6379> 

```

Handling Float Value

```bash
127.0.0.1:6379> set PI 3.14
OK
127.0.0.1:6379> get PI 
"3.14"
127.0.0.1:6379> incr PI
(error) ERR value is not an integer or out of range
127.0.0.1:6379> incrfloat pi 0.1
(error) ERR unknown command `incrfloat`, with args beginning with: `pi`, `0.1`, 
127.0.0.1:6379> incrfloat pi 
(error) ERR unknown command `incrfloat`, with args beginning with: `pi`, 
127.0.0.1:6379> incrfloat PI
(error) ERR unknown command `incrfloat`, with args beginning with: `PI`, 
127.0.0.1:6379> incrbyfloat PI 0.1
"3.24"
127.0.0.1:6379> get PI
"3.24"
127.0.0.1:6379> 
```

The `EXPIRE` command in Redis is used to set a time-to-live (`TTL`) for a key, after which the key will automatically be deleted. The `TTL` is specified in seconds.

```bash
127.0.0.1:6379> set a 15
OK
127.0.0.1:6379> get a
"15"
127.0.0.1:6379> expire a 10
(integer) 1
127.0.0.1:6379> get a
(nil)
127.0.0.1:6379> TTL a
(integer) -2

127.0.0.1:6379> set a 20
OK
127.0.0.1:6379> get a
"20"
127.0.0.1:6379> expire a 15
(integer) 1
127.0.0.1:6379> TTL a
(integer) 12
127.0.0.1:6379> TTL a
(integer) 8
127.0.0.1:6379> TTL a
(integer) 7
127.0.0.1:6379> TTL a
(integer) -2
127.0.0.1:6379> TTL a
(integer) -2
127.0.0.1:6379> 


```
