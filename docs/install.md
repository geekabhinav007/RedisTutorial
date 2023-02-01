# Redis

Redis is an open source, in-memory data structure store, used as a database, cache, and message broker. It supports a wide variety of data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries. Redis is known for its high performance, flexibility, scalability, and wide language support.

## What is the Use Of Redis?

Redis is used for a variety of use cases including:

1. Caching: Redis can be used as a cache to store frequently accessed data for fast retrieval, improving application performance.

1. Database: Redis can be used as a primary database to store structured data such as user profiles, product information, etc.

1. Message Broker: Redis can be used as a message broker to implement communication between microservices, transmit real-time notifications, or implement task queues.

1. Session Management: Redis can be used to store user session data, improving web application performance by avoiding the overhead of reading and writing session data to a database on each request.

1. Real-time Analytics: Redis can be used to perform real-time analytics on large amounts of data by storing it in memory.

1. Leaderboard: Redis can be used to implement leaderboards and high score tables in gaming applications.

These are some of the common use cases, but Redis can be used in many other scenarios where fast, in-memory data storage and retrieval is required.

## Installtion of Redis on Un=buntu 22.04

```bash
sudo apt update
sudo apt install redis-server
sudo nano /etc/redis/redis.conf
```

Inside the file, find the supervised directive. This directive allows you to declare an init system to manage Redis as a service, providing you with more control over its operation. The supervised directive is set to no by default. Since you are running Ubuntu, which uses the systemd init system, change this to systemd:

```bash
sudo systemctl restart redis.service
```

Testing Redis After Installtion

```bash
sudo systemctl status redis
```

Output

```bash
Output
● redis-server.service - Advanced key-value store
   Loaded: loaded (/lib/systemd/system/redis-server.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2018-06-27 18:48:52 UTC; 12s ago
     Docs: http://redis.io/documentation,
           man:redis-server(1)
  Process: 2421 ExecStop=/bin/kill -s TERM $MAINPID (code=exited, status=0/SUCCESS)
  Process: 2424 ExecStart=/usr/bin/redis-server /etc/redis/redis.conf (code=exited, status=0/SUCCESS)
 Main PID: 2445 (redis-server)
    Tasks: 4 (limit: 4704)
   CGroup: /system.slice/redis-server.service
           └─2445 /usr/bin/redis-server 127.0.0.1:6379
. . .
```

Use Redis CLI

```bash
redis-cli
```

In the prompt that follows, test connectivity with the ping command:

```bash
127.0.0.1:6379>  ping
```

```bash
Output
PONG
```

This output confirms that the server connection is still alive. Next, check that you’re able to set keys by running:

```bash
127.0.0.1:6379> set test "It's working!"
```

```bash
Output
OK
```

Retrieve the value by typing:

```bash
127.0.0.1:6379>  get test
```

Assuming everything is working, you will be able to retrieve the value you stored:

```bash
Output
"It's working!"
```

After confirming that you can fetch the value, exit the Redis prompt to get back to the shell:

```bash
127.0.0.1:6379>  exit
```

As a final test, we will check whether Redis is able to persist data even after it’s been stopped or restarted. To do this, first restart the Redis instance:

```bash
sudo systemctl restart redis
```

Then connect with the command-line client once again and confirm that your test value is still available:

```bash
redis-cli
```

```bash
127.0.0.1:6379> get test
```

The value of your key should still be accessible:

```bash
Output
"It's working!"
```

Exit out into the shell again when you are finished:

```bash
127.0.0.1:6379> exit
```

## Exploering Redis
