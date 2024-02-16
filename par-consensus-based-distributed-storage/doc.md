Paper for reference: https://dl.acm.org/doi/pdf/10.1145/3241062

## RSM based storage systems

An RSM based system stores identical states in a *state machine* data structure in each node by executing certain commands.

How command execution in state machines work:

- The client nodes send the commands to the leader which writes them to its own disk logs
- The logs are replicated and sent to all the client nodes(ensures durability through redundancy)
- When majority of the clients have sent the acknowledgement of receiving the logs, the leader executes the commands sequentially from its logs.

The logs are kept consistent with the help of a consensus protocol. Eg. Paxos, Raft, etc.

Periodically a snapshot of the log is taken and stored in the in-memory disk(helps to reduce garbage. After a failure in a node occurs, the node reads the logs from the snaphot logs and restores itself. The node gets its metadata from a `metainfo` data structure. 

> **_NOTES:_** The above method does not correctly recover from a storage fault.

## Approaches during a storage fault

There are 2 broad categories:
1. Protocol oblivious
2. Protocol aware

### 1. NoDetecion

The simplest reaction to storage failure is no reaction at all. Some systems do not use checksums for their on-disk data or their log snapshots. This is a big security failure. The data sent to the clients are not verified at all. 

### 2. Crash

Another method is to maintain checksums and handle IO error and if a node is faulty/corrupted, the system crashed the node so that the fault does not spread.

Crash is better than NoDetection, but it is still suffers from unavailability(node is gone).

### 3. Truncate

Works with the philosophy that if a node is faulty, it is better to discard the faulty data than getting rid of the entire node(better availability). Sounds good, except that it contains a safety violation.






