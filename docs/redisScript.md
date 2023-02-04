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

Example

```sh
127.0.0.1:6379> eval "redis.call('set', KEYS[1] , ARGV[1])" 1 name Kumar 
(nil)
127.0.0.1:6379> eval "redis.call('set', KEYS[1] , ARGV[1], KEYS[2], ARGV[2])" 2 name Kumar last_name Abhinav
(error) ERR Error running script (call to f_3ecc8802000bc23a3612b00e753a4489e0565e21): @user_script:1: ERR syntax error
127.0.0.1:6379> eval "redis.call('mset', KEYS[1] , ARGV[1], KEYS[2], ARGV[2])" 2 name Kumar last_name Abhinav
(nil)
127.0.0.1:6379> get name
"last_name"
127.0.0.1:6379> eval "redis.call('mset', KEYS[1] , ARGV[1], KEYS[2], ARGV[2])" 2 name last_name Kumar Abhinav
(nil)
127.0.0.1:6379> get name
"Kumar"
127.0.0.1:6379> get last_name 
"Abhinav"
127.0.0.1:6379> 
```
