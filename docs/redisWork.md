# Simple Table in Redis

Redis is a NoSQL database and does not support traditional table structures like SQL databases. However, you can use Redis data structures such as Hashes, Lists, Sets, and Sorted Sets to create a simple key-value mapping, similar to a table.

```sh
127.0.0.1:6379> HSET Student_Record name0 "Kumar Abhinav"
(integer) 1
127.0.0.1:6379> HSET Student_Record roll0 "2004825"
(integer) 1
127.0.0.1:6379> HMSET Student_Record name1 "Ram Kumar" roll1 "2004896" name2 "Shyam Kumar" roll2 "7894561" name3 "Sita Kumari" roll3 "45672398"
```

```sh
127.0.0.1:6379> HGETALL Student_Record
 1) "name0"
 2) "Kumar Abhinav"
 3) "roll0"
 4) "2004825"
 5) "name1"
 6) "Ram Kumar"
 7) "roll1"
 8) "2004896"
 9) "name2"
10) "Shyam Kumar"
11) "roll2"
12) "7894561"
13) "name3"
14) "Sita Kumari"
15) "roll3"
16) "45672398"
127.0.0.1:6379> 

```

## How to Convert Redis Db to CSV

To convert Redis database to CSV (Comma Separated Values), We can use one of the following methods:

1. `Redis-cli`: You can use the redis-cli command line tool to extract data from Redis and then save it to a CSV file. To do this, you can use the redis-cli dump command to create a Redis dump file and then use a scripting language like Python or Perl to parse the data and write it to a CSV file.

1. `Third-party tools`: There are several third-party tools available that can convert Redis database to CSV, including redis-dump-to-csv, redis-rdb-tools, and others. These tools provide a more automated solution for converting Redis database to CSV.

1. `Custom scripts`: You can also write your own custom scripts in a programming language of your choice to extract data from Redis and write it to a CSV file. This approach gives you more control over the output format and allows you to automate the process if needed.

### HOW to load Dump file in Redis

#### Efforts

1. Tried Load Method

```sh
redis-cli LOAD < /home/geek/Desktop/nb/dump.rdb
```

`Error`

```sh
(error) ERR unknown command `LOAD`, with args beginning with: 
```

2. Restore Command

```php
redis-cli RESTORE <key> <ttl> <dumpfile>
```

```sh
redis-cli RESTORE backup 0 /home/geek/Desktop/nb/dump.rdb
```

`Error`

```sh
(base) geek@g3:~$ redis-cli RESTORE backup 0 /home/geek/Desktop/nb/dump.rdb
(error) ERR DUMP payload version or checksum are wrong
```

3. Correction in Load Command

```sh
(base) geek@g3:~/Desktop/nb$ redis-cli LOAD < `/home/geek/Desktop/nb/dump.rdb`
/home/geek/Desktop/nb/dump.rdb: line 1: $'REDIS0009\372': command not found
/home/geek/Desktop/nb/dump.rdb: line 2: $'!\0061\a': command not found
/home/geek/Desktop/nb/dump.rdb: line 2: $'\035\0031\a\360\240\300\035\0052\a\vShy\300\037\r': command not found
/home/geek/Desktop/nb/dump.rdb: line 2: $'redis-bits\300@\372\005ctime\302\030\323\335c\372\bused-mem\302\320O\r\372\faof-preamble\300\376\373\001\r\016Student_Record\303@s@\214\004\214\205': command not found
bash: `/home/geek/Desktop/nb/dump.rdb`: ambiguous redirect
(base) geek@g3:~/Desktop/nb$ cd 
(base) geek@g3:~$ redis-cli
127.0.0.1:6379> keys *
(empty array)
127.0.0.1:6379> 

```

#### Success
