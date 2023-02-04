# Redis Script

Redis Script is a feature in Redis that allows you to execute Lua scripts on the Redis server. Lua is a lightweight, multi-paradigm programming language designed primarily for embedded systems and clients.

Redis Scripts are used to perform complex operations atomically and in a single round trip, which makes them ideal for use cases that require a large number of commands to be executed as a single transaction.

Here's an example of a simple Redis Script that increments the value of a key:

```sh
127.0.0.1:6379> EVAL "return redis.call('incr', KEYS[1])" 1 count
(integer) 1
```

In this example, the `EVAL` command is used to execute the Lua script. The first argument is the script itself, and the second argument is the number of keys used in the script (in this case, only one key, `count`).

You can also use Redis Scripts to create custom commands, perform complex operations on multiple keys, and manage transactions.
