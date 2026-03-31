[Video](https://www.youtube.com/watch?v=eym48yrObhY&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=10)

Write Skew 1
- locks are useful to prevent race condition (as we know)
- but what happens if the objects are not impacted by each others locks? (during write skew)
- we grab only locks of single objects and not both
Solution: we need to grab the locks, where a defined condition is met

Write Skew 2 (Phantom Writes)

- two transactions execute concurrently and attempt to insert new rows that conflict with each other
- since the conflicting data doesn’t exist yet, no locks are held leading to a phantom problem
- the transactions do not see each other’s uncommitted changes and believe their inserts are valid
- as a result, both insert new rows that, together, violate a constraint (e.g., uniqueness or a business rule)
- this happens because constraints are based on data that was not yet present at the time of each write


Solution: Materialize Conflicts

- populate rows in a table with items where could be a conflict → we can use locks
- race condition will still happen since two transactions want same row/object but lock fixes phantom write
- how to know what null row should be created → think in advance (ex. create all available meeting rooms before making them open to be booked)