[Video](https://www.youtube.com/watch?v=I1wQsY-Nh_k&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=3)

Why we need indexes (notes from previous videos):
1. Improve the reading speed (better than O(n))
2. We have to go through the whole table to get our value (thats bad)

Hash indexes (are based on hash maps)
→ use hash function (abstract method)
→ takes key (memory location) and returns a value back (is O(1) for reads and writes)

Two keys may produce the same hash index. That’s called a collision
It can be handled with 
- chaining (create a list)
- probing (find next possible slot)

Point of index easily scan for certain key

Jordan → place on disc O(1) for writing or reading 

Issues:

- Hash Maps are bad on disc → all hash indexes (keys) are kept on memory
- Ram is expensive → less data can be stored
- Ram is not durable
- No range queries : Since hash map only works when you have the key, and not having the keys will force you to go through the entire set of keys, which is again an O(n) operation.

Solution

- write ahead log → before writing to the hash map change is first written on HDD
- crash happens → we replay the logs
	1. on restart the db checks the log
	2. committed but not applied operations are read
	3. operations are re-applied to the in-memory hash map
	4. the system resumes