# Apache Kafka: A Technical Overview

*A short technical paper written in simple language*

## 1. Introduction

Companies produce a lot of data every second. Users click buttons, make payments, and sensors send readings. Each of these is called an event, and it needs to be moved and used quickly.

Apache Kafka is an open-source platform made for this job. It stores and moves streams of events between different programs.

Kafka was built at LinkedIn around 2010 to collect activity data from their website. It became an open-source Apache project in 2011 and is now used by thousands of companies.

The main idea is simple. One program writes events to Kafka. Other programs read them whenever they want. The two sides never talk to each other directly.

## 2. Main Parts of Kafka

- **Producer:** a program that sends events into Kafka, such as a shopping site sending an event for each order.
- **Consumer:** a program that reads events from Kafka, such as a billing system.
- **Topic:** a named stream of events, like "orders" or "payments".
- **Partition:** a topic is split into partitions, which are ordered lists of events. They can live on different machines, so the work is shared. Order is only guaranteed inside one partition.
- **Broker:** a single Kafka server. A group of brokers is called a cluster.
- **Offset:** a number given to each event in a partition. A consumer remembers its offset so it can continue from the same place after a restart.
- **Consumer group:** consumers that share the work of reading a topic. Each partition goes to only one consumer in the group.

Producers and consumers do not know about each other. This makes big systems much easier to change.

## 3. How Kafka Stores and Moves Data

In a normal queue, a message is removed after it is read. In Kafka, the message stays.

Kafka saves each partition as a log file on disk. New events are only added at the end, and old events are never changed. Writing to disk in order is very fast, and this is a main reason why Kafka is quick.

Events are kept for a set time, for example seven days. After that, old data is deleted. Because events stay, a consumer can read old data again. This is called replaying. It is useful if a program had a bug, or if a new service needs to catch up on past events.

Kafka also uses these ideas to stay fast:

- It sends data in batches instead of one event at a time.
- It can compress the batches.
- It uses the operating system's memory cache.

For delivery, Kafka offers three levels: at most once (may be lost), at least once (may be repeated), and exactly once (one time only). Exactly once is the safest but a little slower.

## 4. Staying Safe When Machines Fail

In big systems, machines break often. Kafka is built with this in mind.

Each partition is copied to more than one broker. A common choice is three copies. One copy is the leader, and all reads and writes go through it. The other copies are followers that keep copying from the leader.

If the leader's broker stops working, Kafka picks a follower as the new leader. The system keeps running.

A producer can also choose how sure it wants to be, using the acks setting:

- **acks=0:** do not wait. Fastest, but least safe.
- **acks=1:** wait for the leader only.
- **acks=all:** wait for all up-to-date copies. Safest.

Older Kafka versions needed a tool called ZooKeeper to manage the cluster. Newer versions use a built-in system called KRaft, which is simpler to run.

## 5. Uses, Strengths and Limits

Kafka is commonly used for:

- Moving data between systems, such as from a database to a data warehouse
- Real-time dashboards and fraud detection
- Letting microservices share events
- Collecting logs from many servers

**Strengths:** it is very fast, it grows easily by adding more machines, it keeps data safe, and many programs can read the same data.

**Limits:** it is hard to learn at first, it takes effort to run well, and it is too large for small projects where a simple queue is enough.

**Conclusion:** Kafka lets companies react to events as they happen instead of working in big daily batches. It is not right for every problem, but when there is a lot of data and many systems that need it, Kafka is one of the best choices today.
