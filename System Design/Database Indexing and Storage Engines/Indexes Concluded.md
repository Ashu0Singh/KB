[Video](https://www.youtube.com/watch?v=QO7KTO-8RWM&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=6)

Indexing techniques:
1) Hash Index 
	- They are basic hashmaps in memory. (NOT disk - as we need random hashmap access instantly and not seek it)
	- Thus limited by memory space, expensive
	- Fast reads and writes
	- Bad for range queries
	- To add durability, we add WAL - write to disk as log (easy as pointer is always at the end) and then write to the hashmap

2) B-Trees
	- Self balancing tree, entirely kept on disk
	- Hence NO limit on size
	- Advantage having lesser concern over durability
	- Slower reads than “Hash index” technique as - disk vs memory speed.
	- Reads are fast - O(LogN) to retrieve, but slow writes
	- Good for range queries (as stored in tree structure)
	- Durability can be ensured by NOT updating tree in place, rather updating the pages/block separately file and then updating the reference later on.

3) LSM Tree + SSTable
	- In-memory tree table (AVL, red-black), self balanced
	- Little faster writes compared to B-Trees, but slower than hash index
	- Slower reads speeds than B-Trees, as it has to check all SStables (Also slower range queries)
	- Durability handled by WAL - which can be replayed later
	- Space concern of LSM trees as in-memory, However we have SStables which are outputted to disk
	- Hence No of keys limit not a concern (to store by space)
	- SSTable - sorted, immutable
	- Finding key - can go on taking time - it is first checked in tree (memtable) and only then across SSTable backwards from creation time
	- To delete, its implemented by tombstone value - indicating deleted. It is added to the latest SSTable entry

LSM Optimizations
1. Use Sparse index (Also known as index for SSTable) : Take “certain” keys of SSTable and create a sparse index with corresponding stored memory location. Can use binary search to find in-between keys
2. Bloom Filters : Can vaguely tell, if certain “key” present in the SSTable
3. Compaction 
	1. Merges SSTables in background - O(N) operation
	2. Cons is extra CPU processing in background could be bad

# LSM Tree Index

![[lsm_tree_write_path.svg]]

**1. Incoming write** Every write is stored in the Memtable (an in-memory, always-sorted structure) and simultaneously appended to the Write-Ahead Log (WAL) for crash durability.

**2. Memtable flush** When the Memtable hits its size threshold, it is frozen and a new empty Memtable takes over immediately. In the background, the frozen Memtable is flushed to disk as an immutable SSTable — writes are never blocked.

**3. SSTables accumulate** New writes go only into the active Memtable, never directly to disk. Over time, repeated flushes produce multiple SSTable files on disk.

**4. Compaction** Periodically, the LSM Tree merges multiple SSTables into fewer, larger ones — removing overwritten or deleted keys and rewriting everything to disk in sorted order. This keeps reads efficient and reclaims disk space.