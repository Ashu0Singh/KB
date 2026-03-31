[Video](https://www.youtube.com/watch?v=oGmxzUBCYtY&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=7)

## Atomicity
A transaction is all or nothing - if any part of the transaction fails, the whole transaction (when transferring money from one account to another - either both the debit and credit happen or neither does)

## Consistency
A transaction brings the database from one valid state to another - no invariants (after a transaction, no foreign key constraints are violated)

## Isolation
Concurrent transactions do not interfere with each other. No race conditions (two people buy a concert seat and they are not both getting the same one)

## Durability
Once a transaction is committed, it's permanently saved even if the system crashes (after a purchase confirmation, the record stays even after a power outage)