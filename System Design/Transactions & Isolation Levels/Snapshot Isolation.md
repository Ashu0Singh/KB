[Video](https://www.youtube.com/watch?v=Tgpa9TrxsfU&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=9)

Situation:
- Total balance across accounts must always be 1 million $
- Balance is transferred between accounts only (A → B → C → D).
- A long read transaction checks balances in sequence
- Meanwhile, another transaction transfers money from E to A
- Result: the reader sees inconsistent data (e.g., A has new balance, others are old) → 100,000 $ discrepancy

Cause:

- Under snapshot isolation, each transaction sees a snapshot of the DB at start time
- Updates by other transactions during the read are not visible, leading to partial states being read

Solution: write ahead log

- Every write is first logged → ensures durability and atomicity
- Each transaction gets a monotonic ID
- Data is versioned: values are stored along with their transaction ID
- Readers see only data committed before their transaction started → consistent snapshot

In few words: we read snapshots instead of db table for reads