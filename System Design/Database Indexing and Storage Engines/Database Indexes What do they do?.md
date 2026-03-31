[Video](https://www.youtube.com/watch?v=LzNdvuj3a5M&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=2)

Important stuff from vid before:  
1. Data should be stored persistently  
2. Data should be stored on a hard drive and not in RAM
3. Data is stored in HDD  

New stuff:  
- Data allocation (position on the hard drive) defines the reading speed
	- If the data is store next to each other the shaft wouldn't have to move much in order to get some data from the disk so it would be faster. 
- Data stored on an array: key-value type of storage  

When you want to find some info with the key/word "Jordan" you need to run through the whole table to get the item  
→ O(n) time complexity, same for writing (find → write)

Idea for writing:  
Instead of overwriting the older field we add the changed key value/item to the bottom of the table and make read operations from the bottom, since we keep the pointer (read it up) on the bottom of the disc  
→ O(1) for writing → nice ✅  
→ O(n) read time, but table more rows, so more of the n → not so good in real cases ❌

Most of the time we care more for reading speed  
→ we use indexes 📚
→ finding a row by a key
→ make a range query: show rows with names between A-B

Indexes:
for better read speed you pay with writing speed → still a win
→ for other info check next vid


O(n) → time complexity depends on the amount of items in the table/array  
10 items with db reading speed of 1 sec will get you the 10th item in 10 seconds (worst case) ⏱