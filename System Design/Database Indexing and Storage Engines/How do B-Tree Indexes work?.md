[Video](https://www.youtube.com/watch?v=Z2OaqmxiH20&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=4)

B-Trees are a type of database index stored on disk. The structure is a balanced tree where each node can hold up to 256MB of data. Finding a record requires traversing multiple nodes from the root down to the relevant leaf, following references at each step. The tree must remain balanced (similar depth on all branches) to guarantee efficient lookups.

**Writing new elements**

When inserting a new element, if the target node has space, the element is added and a reference is updated. If the node is full, it must be split. A split can cascade upward each parent may also be full and require splitting all the way up to the root if necessary. This cascading split is what keeps the tree balanced after insertions.

**Crash recovery (when B-Trees "die")**

If a write is interrupted mid-split, the tree can end up in an inconsistent state. The standard solution is a _write-ahead log_ (WAL) changes are recorded sequentially to a log before being applied to the tree itself, so recovery is possible after a crash. Another technique is maintaining a shadow copy of the tree during writes.

**B-Trees vs. Hash indexes — summary**

|Property|B-Tree|
|---|---|
|Storage|Self-balancing tree on disk|
|Memory use|Caches upper levels; buffers reads/writes and WAL|
|Read performance|Good|
|Dataset size|Unlimited — not all keys need to fit in RAM|
|Range queries|Supported|
|Trade-off|Slower than hash indexes, but far more flexible|


![[btree_structure.svg]]

The diagram shows the three levels: a root node at the top, internal nodes in the middle that hold key ranges for routing, and leaf nodes at the bottom that store the actual data rows. The green arrows along the leaf level illustrate how leaves are linked in sorted order — this is exactly what makes range queries (`WHERE age BETWEEN 20 AND 40`) efficient on B-Trees, whereas hash indexes can't do this at all.