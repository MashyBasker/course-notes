# What is Bayou used for

Used for non-real time but collaborative systems. Such as shared calendars, emails, collaborative research paper writing software(eg. overleaf -> can be both real-time and non-real time).

## Bayou's System Model

- each time data is updated(collected), full replication is performed in a number of servers. Applications which use Bayou act as clients which interact with the servers through Bayou API. 

- The API supports only read and write. Read is for fetching the data and write is for updating(insert, delete, modify, etc) the data. 

The client needs to have access to only one server. The servers can propagate the read and write command to the other. If there is only one client-server pair:

- CLIENT <-(read/write)-> SERVER

Multiple servers:
- CLIENT <-(read/write)-> SERVER1 <-> SERVER2 <-> SERVER3

## Replication Model

Bayou has weak consistency model for replication. The replicas containing data items are not updated in unison(creates discrepency between data which requires special kind of programming to curb). 
