[Video](https://www.youtube.com/watch?v=oS60pr8H1e0&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=8)

- Databases are multithreaded so there read and write operations are concurrent. 
- No way to know the order of execution

Commit
- Commit a write → Happens after all writes to all rows of the table are done

**Race conditions types**

Dirty write:

| Transaction 1                            | Transaction 2                               |
| ---------------------------------------- | ------------------------------------------- |
| Write name buyer.name "Ashutosh"         |                                             |
|                                          | Write name buyer.name "Donald"              |
|                                          | Write address to buyer.address "whitehouse" |
| Write address to buyer.address "Lucknow" |                                             |
| Commit                                   | Commit                                      |
- Same row is overwritten and committed by two different operations
- Solution: Lock a row while writing
- Dead lock is an issue, use a deadlock detection to detect. Incase a deadlock is detected release the lock from one transaction.  

Dirty reads:
- An uncommitted write is red (fail of write or race condition) → invalid read
- Using locks for reads would be very expensive → as we remember reads are more important then writes
- Solution → store the old value of a row while there is an incoming write and then the database can return the old value until the incoming write is committed