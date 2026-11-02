# Apache Kafka for Beginners

This guide explains Apache Kafka from zero. You do not need any earlier knowledge of Kafka. Every new word is explained when it first appears, and there is a short glossary at the end.

---

## 1. What is Kafka?

Kafka is a tool that helps different programs **send data to each other**.

- One program writes data into Kafka.
- Other programs read that data from Kafka.
- Kafka keeps the data safe on disk for some time, so readers can read it now or later.

You can think of Kafka as a **big notice board** in an office:

- People who want to share news pin a note on the board (they write data).
- People who want to know the news come and read the notes (they read data).
- The writers and readers never need to meet each other.
- Notes stay on the board for some days, so someone who was absent can still read them.

---

## 2. What problem does it solve?

Imagine an online shop. When a customer places an order, many parts of the shop need to know about it:

- the payment system
- the email system (to send a confirmation)
- the warehouse system
- the analytics dashboard

**Without Kafka**, the order program must connect to each of these systems one by one. If you add a new system, you must change the order program again. If one system is slow or down, the order program is affected.

**With Kafka**, the order program just writes one message: "new order placed". Each other system reads that message when it is ready. To add a new system, you simply add a new reader. The order program is not changed.

So Kafka gives you:

- **Simple connections:** every program talks only to Kafka.
- **Safety:** if a reader is down, the data waits in Kafka until it comes back.
- **Speed:** Kafka can handle a very large number of messages every second.
- **Replay:** data is not removed after reading, so you can read it again.

---

## 3. The basic words (one by one)

### Event (or message, or record)

One piece of information. For example: "Customer 42 ordered a book at 10:30".

An event has:

- a **key** (optional), for example `customer-42`
- a **value**, the main data, for example `book`
- a **time**

### Topic

A **name for a group of events**. It is like a folder or a notice board section.

Examples: `orders`, `payments`, `page-views`.

### Producer

A program that **sends** events to a topic.

### Consumer

A program that **reads** events from a topic.

### Broker

A **Kafka server**. It stores the events and answers producers and consumers.

### Cluster

A **group of brokers** working together. Real systems use several brokers, so if one breaks, the others keep working.

### Partition

A topic is divided into smaller parts called partitions. We explain these in the next section.

### Offset

The **position number** of an event inside a partition: 0, 1, 2, 3, ... It works like a page number. A consumer uses it to remember where it stopped reading.

---

## 4. Partitions: how a topic is split

A topic can be very big, so Kafka splits it into **partitions**.

- Each partition is a list of events in order.
- New events are always added at the **end**. Old events are never changed.
- Different partitions can be on different brokers, so the work is shared.

Here is a topic called `orders` with 3 partitions:

```
orders
  Partition 0:  [0] [1] [2] [3] [4]  --> new events added here
  Partition 1:  [0] [1] [2]          --> new events added here
  Partition 2:  [0] [1] [2] [3]      --> new events added here
```

The numbers in brackets are the offsets.

### Why use partitions?

- More partitions means more programs can work at the same time. This makes Kafka fast.

### Important rule about order

- Kafka keeps the order of events **inside one partition**.
- It does **not** keep the order between different partitions.

### How to keep related events in order

- Give the events a **key**, for example the customer id.
- Kafka sends all events with the same key to the **same partition**.
- So all events of `customer-42` stay in the right order.

---

## 5. How it works: step by step

1. A **producer** sends an event to the topic `orders`.
2. Kafka picks a partition for it (using the key, if there is one).
3. The **broker** adds the event at the end of that partition and gives it an offset.
4. A **consumer** reads events from the partition, starting from its saved offset.
5. The consumer saves its new offset, so next time it continues from there.

Reading an event does **not** delete it. The event stays until the retention time is over (see section 8).

---

## 6. Consumer groups: sharing the work

Sometimes one consumer is too slow for all the events. So Kafka lets several consumers work together as a **consumer group**.

- Consumers get a **group name** (called `group.id`). Consumers with the same name belong to one group.
- Kafka divides the partitions among the consumers in the group.
- **One partition is read by only one consumer in the group** at a time. This avoids reading the same event twice inside the group.

Example: a topic with 4 partitions and a group of 2 consumers:

```
Partition 0  -->  Consumer A
Partition 1  -->  Consumer A
Partition 2  -->  Consumer B
Partition 3  -->  Consumer B
```

Good to know:

- If a consumer **crashes**, Kafka gives its partitions to the others. This is called a **rebalance**.
- If you have **more consumers than partitions**, the extra consumers do nothing.
- **Different groups are independent.** If the "email" group and the "analytics" group both read `orders`, each gets **every** event.

---

## 7. Replication: what if a server breaks?

A single server can fail. To protect the data, Kafka keeps **copies** of each partition on different brokers.

- The number of copies is the **replication factor**. A common choice is **3**.
- One copy is the **leader**. Producers and consumers talk to the leader.
- The other copies are **followers**. They copy everything from the leader.
- If the leader's broker breaks, one follower becomes the new leader. Nothing is lost.

A safe setup used in many companies:

- replication factor = **3**
- producer setting `acks=all` (the producer waits until all in-sync copies have the event)
- `min.insync.replicas` = **2** (at least 2 copies must have the event before it counts as saved)

With this setup, one broker can fail and you still lose no data.

---

## 8. How long does Kafka keep data?

Kafka stores events on disk. It does not delete an event after reading. It uses rules:

- **Time rule:** delete events older than some time. The default is **7 days**.
- **Size rule:** delete the oldest events when the partition gets too big.
- **Compaction (optional):** keep only the **latest event for each key**. This is useful when you only care about the newest value, like the current address of a user.

---

## 9. Why is Kafka fast?

- It **only appends** to the end of files. Writing in order is much faster than jumping around the disk.
- It uses the computer's memory cache of the operating system.
- It sends data from disk to the network **without extra copying** (called zero-copy).
- It sends events in **batches**, and can **compress** them.

---

## 10. ZooKeeper and KRaft (you may see these words)

Kafka must remember details about itself: which topics exist, which broker is the leader, and so on.

- **Old Kafka** used a separate program called **ZooKeeper** for this.
- **New Kafka** does this itself using **KRaft**.
- Since **Kafka 4.0**, ZooKeeper is removed. Only KRaft is used.

If you read an old tutorial that says "start ZooKeeper first", that tutorial is for old Kafka versions.

---

## 11. Delivery guarantees (what if something fails?)

When a program crashes in the middle of work, an event might be lost or processed twice. Kafka has three levels of promise:

| Name | What it means | Simple example |
|------|---------------|----------------|
| At-most-once | An event may be **lost**, but is never repeated | Save the position first, then process |
| At-least-once | An event is **never lost**, but may be **repeated** | Process first, then save the position |
| Exactly-once | The event counts **exactly one time** | Needs special settings (transactions) |

- **At-least-once** is the most common choice. Your program should be ready to handle the same event twice.
- **Exactly-once** works for Kafka-to-Kafka work. If you write to an outside system, like a database, you need extra care.

---

## 12. Try it yourself

### Step 1: Start Kafka with Docker

You need Docker installed. Then run:

```bash
docker run -d --name kafka -p 9092:9092 apache/kafka:latest
```

This starts one Kafka server on port 9092. (You can also download Kafka from https://kafka.apache.org/downloads and follow the "Quickstart" on the same site.)

### Step 2: Create a topic

```bash
docker exec -it kafka /opt/kafka/bin/kafka-topics.sh --create --topic orders --partitions 3 --bootstrap-server localhost:9092
```

- `--topic orders` is the name.
- `--partitions 3` splits it into 3 partitions.
- `--bootstrap-server localhost:9092` tells the tool where Kafka is.

### Step 3: Send some events

```bash
docker exec -it kafka /opt/kafka/bin/kafka-console-producer.sh --topic orders --bootstrap-server localhost:9092
```

Type a few lines, press Enter after each line. Press Ctrl+C when you are done.

### Step 4: Read the events

Open another terminal and run:

```bash
docker exec -it kafka /opt/kafka/bin/kafka-console-consumer.sh --topic orders --from-beginning --bootstrap-server localhost:9092
```

You will see the lines you typed. `--from-beginning` means "start from the first event".

### Step 5: Stop Kafka

```bash
docker stop kafka
docker rm kafka
```

---

## 13. A small Python example

Install the library:

```bash
pip install confluent-kafka
```

### Producer (sends one event)

```python
from confluent_kafka import Producer

producer = Producer({"bootstrap.servers": "localhost:9092"})

producer.produce("orders", key="customer-42", value="book")
producer.flush()
```

What each part does:

- `Producer({...})` connects to Kafka at `localhost:9092`.
- `produce("orders", key=..., value=...)` sends one event to the topic `orders`.
- `flush()` waits until the event is really sent. Without it, the program may stop before sending.

### Consumer (reads events)

```python
from confluent_kafka import Consumer

consumer = Consumer({
    "bootstrap.servers": "localhost:9092",
    "group.id": "billing",
    "auto.offset.reset": "earliest",
})
consumer.subscribe(["orders"])

while True:
    message = consumer.poll(1.0)
    if message is None:
        continue
    print(message.key(), message.value())
```

What each part does:

- `group.id` is the name of the consumer group.
- `auto.offset.reset: earliest` means: if this group has never read before, start from the oldest event.
- `subscribe(["orders"])` says which topic to read.
- `poll(1.0)` asks Kafka for a new event and waits up to 1 second.
- If `poll` returns `None`, there was nothing new, so the loop tries again.
- `print(...)` shows the key and value of the event.

Run the consumer in one terminal and the producer in another. You will see the event appear in the consumer.

---

## 14. Where is Kafka used?

- Sending events between different services of an application
- Collecting logs and metrics from many machines
- Live dashboards and alerts
- Copying changes from a database to other systems
- Processing data in real time
- Connecting many systems through one central place

Companies like LinkedIn, Netflix and Uber are known to use Kafka.

---

## 15. Other parts of the Kafka family (just to know)

- **Kafka Connect:** moves data between Kafka and other systems like databases, without writing code.
- **Kafka Streams:** a Java library to process events, for example count or join them.
- **Schema Registry:** keeps the format of messages so writers and readers agree. This is a separate tool, not part of core Kafka.

---

## 16. When should I NOT use Kafka?

- You only have a tiny app with very few messages. A simple tool may be enough.
- You need to run complex searches or reports on the data. Use a database for that.
- You want to send very large files. Store the file elsewhere and send only its link through Kafka.
- You do not want to manage servers. Consider a hosted (managed) Kafka service.

---

## 17. Kafka vs a normal message queue

- **Normal queue (like RabbitMQ):** a message is usually removed after one program takes it.
- **Kafka:** events stay for some days. Many programs can read them, and they can read them again.
- Choose Kafka when you need **replay**, **high volume** and **many readers**.

---

## 18. Glossary

- **Event / message / record:** one piece of data.
- **Topic:** a named group of events.
- **Partition:** one ordered part of a topic.
- **Offset:** the position number of an event in a partition.
- **Producer:** a program that writes events.
- **Consumer:** a program that reads events.
- **Consumer group:** consumers sharing the work of reading a topic.
- **Broker:** a Kafka server.
- **Cluster:** a group of brokers.
- **Leader / follower:** the main copy and the backup copies of a partition.
- **Replication factor:** how many copies of each partition exist.
- **Retention:** how long Kafka keeps events.
- **Rebalance:** Kafka re-dividing partitions among consumers.
- **Consumer lag:** how many events a consumer is behind.
- **KRaft:** the way new Kafka manages itself, without ZooKeeper.

---

## 19. Summary

- Kafka is a notice board for data: programs write events and other programs read them.
- Topics are split into partitions. Order is kept inside one partition.
- Consumer groups share the reading work.
- Replication keeps your data safe if a server breaks.
- Events stay for some time and can be read again.
- Kafka is fast because it writes in order and sends data in batches.

---

## References

- Apache Kafka documentation: https://kafka.apache.org/documentation/
- Apache Kafka quickstart: https://kafka.apache.org/quickstart
- Kreps, Narkhede, Rao. *Kafka: a Distributed Messaging System for Log Processing.* NetDB, 2011.
