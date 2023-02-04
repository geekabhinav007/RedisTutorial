# Transaction in Redis

Transactions in Redis allow you to execute multiple commands as a single, atomic operation. This means that either all the commands in the transaction will be executed, or none of them will, ensuring that your data remains in a consistent state.

To start a transaction in Redis, you can use the `MULTI` command, followed by one or more commands, and then the `EXEC` command to execute the transaction. The transaction will be executed as a single unit of work, and all the commands will be executed in a single pipeline.

If any of the commands within the transaction fail, for example because of a concurrent modification, the entire transaction will be discarded and none of the commands will be executed.

```sh
127.0.0.1:6379> multi
OK
127.0.0.1:6379> set year 3rd
QUEUED
127.0.0.1:6379> get year
QUEUED
127.0.0.1:6379> set intrest "Data Science"
QUEUED
127.0.0.1:6379> get intrest
QUEUED
127.0.0.1:6379> exec
1) OK
2) "3rd"
3) OK
4) "Data Science"
127.0.0.1:6379> 
```
