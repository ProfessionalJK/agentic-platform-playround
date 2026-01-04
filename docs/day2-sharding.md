Day 2 - Sharding, Replication & Partitioning

## Sharding
- It is horizontal partitioning of the data in a database or search engine. Each shard may be held on a separate database server instance to spread load.
- Some data in a database remains present in all shards, but some appears only in a single shard. Each shard acts as the single source for this subset of data.

### Horizontal vs Vertical Sharding
- In horizontal sharding the data is splitted row wise while in Vertical sharding the data is splitted column wise.

#### Pros-
- As the data is horizontally partitioned and stored on multiple shards across multiple regions, it improves the indexing helping the improvement of search performance.
- It enables the distribution of data based on the conditions which helps to speed up the query results.

#### Cons-
- Sharding the DB before optimization causes premature complexity.
- Sharding should be used only when other options of optimizations are inadequate.

## Replication
Replication in computing can refer to
- Data Replication, where the same data is stored on multiple storage devices.
- Computation replication, where the same computing task is executed many times. Computational tasks may be-
    - Replicated in space, where tasks are executed on separate devices.
    - Replicated in time, where tasks are executed repeatedly on a single device.

#### Active replication, which is performed by processing the same request at every replica
#### Passive replication, which involves processing every request on a single replica and transferring the result to the other replicas.

### Leader-Follower Replication
- It is a data distribution model where one primary node (the leader) handles all the write operations, and then copies (replicates) those changes to one or more secondary nodes (the followers or replicas).

- Writes: All data modifications (inserts, updates, deletes) go to the single leader node.
- Replication: The leader streams these changes to followers, often using a replication log or message queue like kafka.
- Reads: Followers serve read requests, distributing the load, and improving performance.
- Consistency:
    - Asynchronous: Leader commits quickly, followers might be slightly behind (potential data loss on leader failure)
    - Synchronous: Leader waits for followers acknowledgement before committing (slower writes, no data loss
    - Semi-Synchronous: A compromise, waiting for subset of followers.

#### Benefits:
- Avoids conflicts by having a single source of truth for writes
- Read-heavy workloads scale by adding more followers
- If the leader fails, a follower can be promoted (failover)

#### Challenges:
- Managing failover and ensuring data consistency during leader loss is complex.
- Asynchronous replication can lead to inconsistencies between leader and followers.

e.g, Amazon DynamoDB provides auto partitions. The table is partitioned using the Partition Key (Primary Key). The write requests take the partition key and determines the partition in which the data will be stored. Similarly, the read requests takes the partition key to determine the partition from which the data will be read.

### Hot Partitioning:
- A performance bottleneck in distributed databases where a single data partition receives disproportionately high traffic (reads/writes) compared to others, overhelming its capacity and causing throttling, slow performance, or failures, usually due to a poorly chosen partition key that concentrates data and requests on a few physical partitions instead of spreading them evenly.

### MCQ:
1. What problem does sharding primarily solve?
- Horizontal Scalability

2. What problem does replication primarily solve?
- Availability and fault tolerance

3. Why is "sharding by tenant ID" risky in multi-tenant systems?
- Some tenants may generate disproportionate load

4. What is a hot partition?
- A partition receiving disproportionate traffic

5. Why does replication not automatically give linear read scalability?
- Because reads may still hit the leader