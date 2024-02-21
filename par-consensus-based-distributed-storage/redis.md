# How Redis supports high availability with replication

- uses a leader-follower protocol(master-replica). Follower copies from the Master.
- the replica instances are *exact* copies of master instances.
- everytime there is a connection error between a replica and a master:
    - the replica tries to reconnect and tries to copy everything from the master
    - does not take into account the state of the master instance(*It may be corrupted too*)

### Three main mechanisms:

- **master and replica are well connected**: master constantly sends streams of commands to the replica to replicate the data in the master instance and also the changes taking place in it.

- **master and replica get disconnected**: replica tries a partial resync, i.e only the commands which were missed during the disconnect.

- **master and replica disconnected & partial resync is not possible**: master does a full resync, where master takes snapshot of the entire data and sends it to thereplica and continue sending the next commands.

Redis mainly does async replication, but synchronous can also be requested with the `WAIT` command.

The Redis master instance maintains a replication ID which is a pseudorandom string that determines the dataset version and how many replication has taken place.



