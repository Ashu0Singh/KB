
[Video](https://www.youtube.com/watch?v=ciGAVER_erw&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=5)

LSM Tree Indexes

- Another type of DB indexes developed some time after B-Trees
- In memory balanced binary search tree (Red Black, AVL, B-tree) → Writes are O(log n)
- Since in memory (RAM) → no durability → write ahead logs (to reformulate the LSM Tree) → still fast writes
- Also less space (as in other indexes, since we need to store all in RAM) → use space from disk when tree too big
- Reset the tree (purge of all nodes)
- Convert LSM tree to SSTable on disk: sorted in order with all the scores kept the same (immutable) → expensive? no, we use in-order traversal which is O(n)

*How SSTables are used for reads? O(log n)*

1. Look for a key in LSM Tree
2. If not found → check the most recent SSTable + second most recent → if the key is the same 👍 O(log n) since binary search

*How to delete a key? (Tombstone)*

Deleted key gets marked in most recent Table as a tombstone values that makes sure that our value is deleted. 

*LSM-Tree optimisations*

- Sparse index: As it say, the index has less values, kinda how range is. Keys locations from the SSTable are extracted and written on disk, faster binary search (does not take a lot space on disk).
- Bloom Filter (to be continued)
    - If key is present in a table → could be wrong
    - If key not present → definitely not present

*LSM main issue + solution:*

- wasted storage: no real deletion of keys (tombstone), update → adding a key again
- table compaction: merges SSTables in background and takes the more recent value  —> takes computing power 👎
- merging two sorted lists → O(n)

Summary:

- *used in **Cassandra**, **LevelDB**, **RocksDB**, **HBase*
- great for write heavy workloads