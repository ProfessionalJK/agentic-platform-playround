Day 3 - Leader Election & Distributed Locks

## Leader Election
- In distributed computing it is a process of designating a single process as the organizer of some task distributed among several computers (nodes). Before the task begun, all network nodes are either unaware which node will serve as the leader of the task or unable to communicate with the current leader.
- After leader election algorithm has been run, however, each node throughout the network recognizes a particular, unique node as the task leader.
- It is required to ensure coordination, consistency and fault tolerance among multiple nodes.
- When a leader fails, the system must detect the outage and transition to a new leader to maintain availability and consistency.
- Leader election process must be repeatable to ensure continuous availability and fault tolerance.


## Distributed Lock Manager
- DML runs on every machine in a cluster, with an identical copy of a cluster-wide lock database.
- DLM provides software applications which are distributed across a cluster on multiple machines with a means to synchronize their accesses to shared resources.

### Mutual Exclusion in Distributed Systems
- It ensures only one process accesses a shared resource (critical section) at a time, crucial for preventing data corruption (race conditions) without shared memory or a global clock, relying instead on message passing.
- In distributed systems, local locks (such as mutexes or semaphores) fail to provide mutual exclusion because they are restricted to a single machine's memory space and process.


### Lease-Based locks
- In Distributed Systems, a leased-based lock is a time bound version of a standard mutual exclusion lock (mutex).
- Unlike traditional locks, which remain held until explicitly released, a lease automatically expires after a set period.
- It prevents the deadlock after crashes by breaking the No Preemption condition - one of the four fundamental requirements for a deadlock to exist.


## MCQ:
1. Why is leader election required in Distributed Systems?
- To coordinate actions that must be done by only one node
2. Why are leases preferred over permanent lock?
- They avoid deadlock when the lock holders crashes
3. What is a split-brain scenario?
- When multiple nodes believe they are the leader
4. Why can't a JVM level or process level lock be used in distributed systems?
- It doesn't coordinates across machines
5. What is the most important property of a distributed lock used for correctness?
- Mutual exclusion under failures


### Hands-On
```python
 
lease = None
 
def acquire_lease(worker_id):
	global lease
	now = time.time()
	if lease is None or lease["expiry"] < now:
		lease = {
			"owner": worker_id,
			"expiry": now + 30
		}
		return True
	return False
 
def renew_lease(worker_id):
	global lease
	if lease and lease["owner"] == worker_id:
		lease["expiry"] = time.time() + 30
```