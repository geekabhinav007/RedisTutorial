# Pub/Sub

Redis Pub/Sub is a messaging pattern in Redis that allows communication between multiple clients through channels. The Pub/Sub pattern consists of two parts:

1. Publishing: A client can publish messages to a channel.

1. Subscribing: Clients can subscribe to a channel to receive messages.

The main benefits of using Redis Pub/Sub are:

1. Scalability: Redis Pub/Sub allows for a highly scalable messaging architecture that can handle thousands of messages per second.

1. Real-time notifications: Redis Pub/Sub provides real-time notifications that can be used to build applications that require up-to-date information.

1. Easy to use: Redis Pub/Sub is a simple and easy-to-use messaging pattern that can be integrated into any Redis-based application.

To use Redis Pub/Sub, clients must first subscribe to a channel using the `SUBSCRIBE` command. Then, they can publish messages to that channel using the `PUBLISH` command. Subscribed clients will receive all messages published to the channel in real-time.

Subscrition

```sh
(base) geek@g3:~$ redis-cli
127.0.0.1:6379> SUBSCRIBE news
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "news"
3) (integer) 1
```

Publish

```sh
(base) geek@g3:~$ redis-cli
127.0.0.1:6379> PUBLISH news "breaking news: Redis Pub/Sub is now available."
(integer) 1

```

```sh
(base) geek@g3:~$ redis-cli
127.0.0.1:6379> SUBSCRIBE news
Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "news"
3) (integer) 1
1) "message"
2) "news"
3) "breaking news: Redis Pub/Sub is now available."
1) "message"
2) "news"
3) "breaking news: I am able to use pub/sub of redis"
```

```sh
(base) geek@g3:~$ redis-cli
127.0.0.1:6379> PUBLISH news "breaking news: Redis Pub/Sub is now available."
(integer) 1
127.0.0.1:6379> PUBLISH news "breaking news: I am able to use pub/sub of redis"
(integer) 1
127.0.0.1:6379> 

```
