# CAP Theorem
#### Any distributed data system can provide any two of three guarantees-
- Consistency
- Availability
- Partition Tolerance

Data should be consistent through out all the read requests, it must be available for all the non-failed nodes. The system should continue to operate despite any number of failures.

No system is safe from network failures. Hence, one must choose between CP and AP to keep it going.

In case of network partition failures-
1. Cancel the operation to ensure the consistency, risking availability
2. Proceed with the operation to ensure availability, risking consistency
   e.g., RDBMS chooses consistency over availability while NoSQL chooses availability over consistency.

## PACELC
If Partition (P) happens then there is a trade-off between Availability (A) and Consistency (C), Else (E) there is trade-off between Latency (L) and Consistency (C).

Note: Trade-off means letting go one desirable thing to gain another, involving a compromise where improving one means sacrificing another.


## Consistency Models:
### 1. Eventually Consistent: 
It allows temporary data inconsistencies as updates propagate, prioritizing high availability, low latency, and massive scale.
### 2. Strongly Consistent:
It guarantees all users see the absolute latest data immediately, ensuring accuracy but sacrificing speed and scalability.

## MCQ:
1. Why is Partition Tolerance considered mandatory in CAP?
   - Because network partitions cannot be prevented.

2. CAP theorem tradeoffs apply primarily:
   - During network partitions

3. Which component in an agentic runtime most clearly requires strong consistency?
   - Execution ownership / lease

4. Why is eventual consistency acceptable for an agent registry?
   - Metadata staleness does not break correctness

5. Why is "use strong consistency everywhere" a bad idea?
   - It increases latency and reduces availability during failures

#### During network partitions, we choose availability for most components and apply strong consistency only where correctness would otherwise break