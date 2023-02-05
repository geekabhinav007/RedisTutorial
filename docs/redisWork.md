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

- Tried Load Method

```sh
redis-cli LOAD < /home/geek/Desktop/nb/dump.rdb
```

`Error`

```sh
(error) ERR unknown command `LOAD`, with args beginning with: 
```

- Restore Command

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

- Correction in Load Command

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

- Placing Dump File to Redis Working Directory.

I was surprised when I noticed that whenever I attempted to place a dump file in the Redis working directory and restart the Redis services, the actual file was always changed to a blank dump file. My Proferssor, Rai Sir, and I thought that the issue could be related to the Redis configuration file, but after checking, we found no evidence to support our assumption. We tried to verify the file size by using the command `ls -trlh`, but everything appeared normal. We even changed the owner and password of the dump file, but to no avail.

Finally, we came up with a plan to run the `start` and `stop` service of Redis one by one to analyze the problem. We first made a copy of the desired dump file and stopped the Redis service. To our `amazement`, the file was overwritten by a blank file. It was then that we realized the problem. Whenever the Redis service was stopped, the current instance of Redis was saved in the working directory, and the current instance was always blank.

Therefore, we decided to `stop` the `Redis-server`, copy the dump file, and then `start` the server, which worked perfectly. We learned that the order of commands or the sequence of events can have a significant impact.

### Success

#### Restore an RDB file

- If you have an RDB file dump.rdb that contains the data you want you can use this file to create a new database.

- Copy the dump.rdb file into the Redis working directory.

- If you do not know what it is folder you can run the command `CONFIG get dir` in `redis-cli` where your Redis instance is up and running.

- Start the Redis service with the redis-server.

- The file dump.rdb is automatically imported.

- Connect to the database using redis-cli or any other client, to check that data have been imported.

Note:- `You Must 1st Stop the Redis-Server then copt the dump file to the Redis working directory then Start the Redis-Server`

`Here Order matters alot`

### Converting key value to CSV

To find all unique keys in Redis, you can use the command "KEYS pattern" where pattern is a string that specifies a pattern for matching the keys you want to retrieve. For example, to get all keys in Redis, you can run "KEYS *". This will return an array of all keys in the database.

It's important to note that the KEYS command can be very slow for large databases and should be used with caution. A better alternative is to use the SCAN command which is a more efficient way of iterating through keys in Redis.

```sh
redis-cli --scan --pattern post:* |\
grep -e "^post:[^:]*$" |\
awk '{print "hmget " $0 " deleted editor timestamp edited reputation content pid uid tid votes"}' |\
redis-cli --csv > postCSVScript.csv meaning
```

- The redis-cli --scan --pattern post:*command retrieves a list of keys in the Redis database that match the pattern "post:*".

- The grep -e "^post:[^:]*$" command filters the list of keys to include only keys that exactly match the pattern "post:*".

- The `awk '{print "hmget " $0 " deleted editor timestamp edited reputation content pid uid tid votes"}'` command generates a Redis hmget command for each key in the list, which retrieves the values of multiple hash fields associated with the key. The fields being retrieved are: `"deleted", "editor", "timestamp", "edited", "reputation", "content", "pid", "uid", "tid", and "votes"`.

- The `redis-cli --csv` command retrieves the values of the hash fields from Redis and formats the output in CSV format.

The `> postCSVScript.csv` redirection writes the CSV output to a file named postCSVScript.csv.

`The purpose of this script is to extract information about posts from a Redis database and save it to a CSV file for further processing or analysis.`
