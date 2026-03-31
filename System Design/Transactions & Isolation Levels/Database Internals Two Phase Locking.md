[Video](https://www.youtube.com/watch?v=gB7qazeSD3k&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=12)

# Two-Phase Locking (2PL)

## What it is

Two-phase locking is a concurrency control method used to achieve **serializability** — making concurrent transactions appear as if they ran one at a time. It was the dominant approach in traditional SQL databases before CPUs were fast enough for actual serial execution.

---

## The two lock modes

Unlike a simple exclusive lock, 2PL introduces two modes on the same lock:

- **Reader lock (shared)** — multiple transactions can hold this simultaneously
- **Writer lock (exclusive)** — only one transaction can hold this; must wait for all readers to release first

This matters for the read-modify-update pattern: while a transaction holds a reader lock on a row, no one can upgrade to a writer lock, so the data it read can't change underneath it. The predicate stays valid.

---

## The deadlock problem

![[Pasted image 20260330162114.png]]

The biggest weakness of 2PL. Even when transactions grab locks in the same order, deadlocks can still occur.The example: Jordan and Snoop both want to copy each other's shopping cart items. Both grab reader locks on both rows simultaneously. Now neither can upgrade to a writer lock — each is waiting for the other to release. The system must detect this, abort one transaction, and retry. This kills concurrency and is expensive.

---

## The phantom problem

2PL doesn't fully solve phantoms. Example: two users both try to join a class capped at 3 people, with 2 already enrolled. Both run `SELECT COUNT(*)` (grabbing read locks), both see 2 < 3, and both insert a new row — bringing total to 4. Since the new rows didn't exist yet, there were no locks to contend with.

**The core issue:** you need to lock rows that don't exist yet.

---

## Solutions for phantoms

### Predicate locks

Lock all rows matching a condition (e.g. `WHERE class_name = 'flexibility' AND class_time = '6pm'`). Any future row that would match that predicate is also covered. The downside: evaluating the predicate query can be slow, especially without a perfect index.

### Index range locking

A practical alternative — instead of running the precise predicate query, lock a superset of rows using an available index. If there's an index on `class_name`, just lock all rows for `'flexibility'` regardless of time. This is faster (O(log n) index lookup) but blocks more rows than strictly needed, potentially slowing down unrelated queries.

The trade-off: precision vs. speed. Locking a superset is often worth it. Locking the whole table never is.

---

## Summary of 2PL trade-offs

| Property          | Detail                                                                    |
| ----------------- | ------------------------------------------------------------------------- |
| Goal              | Serializability via shared/exclusive locks                                |
| Strength          | Allows concurrent reads; safe read-modify-update                          |
| Weakness          | Deadlocks require detection + abort + retry                               |
| Also slow because | Lock acquisition overhead; defensive locking                              |
| Phantom fix       | Predicate locks (precise but slow) or index range locks (fast but coarse) |