
1. [[What is Systems Design?]]
2. Database Indexing and Storage Engines
	1. [[Database Indexes What do they do?]]
	2. [[How do Hash Indexes work?]]
	3. [[How do B-Tree Indexes work?]]
	4. [[LSM Tree + SSTable Database Indexes]]
	5. [[Indexes Concluded]]
3. Transactions & Isolation Levels
	1. [[Intro to ACID Database Transactions]]
	2. [[Read Committed Isolation]]
	3. [[Snapshot Isolation]]
	4. [[Write Skew and Phantom Writes]]
	5. [[Achieving ACID Serial Execution]]
	6. [[Database Internals Two Phase Locking]]
	7. [[Serialisable Snapshot Isolation]]
4. Storage Models & Data Formats
	1. Column Oriented Storage (with Parquet!)
	2. Data Serialization Frameworks - You Should Be Using Them
5. Replication Techniques
	1. Intro to Replication
	2. Dealing with Stale Reads
	3. Single Leader Replication - how it works
	4. Multi Leader Replication - chaos
	5. Dealing with Write Conflicts - What do you do?
	6. CRDTs - Stop Worrying About Write Conflicts
	7. Leaderless Replication Introduction
	8. Quorums - Leaderless Replication Continued
	9. Replication Summarized in 9 Minutes
6. Partitioning and Distributed Systems
	1. Introduction to Partitioning
	2. Two Phase Commit - Distributed Transactions
	3. Consistent Hashing - Rebalancing Partitions
	4. Linearizable Databases
	5. Distributed Consensus - Raft Leader Election
	6. Distributed Consensus - Raft Writes
	7. What is ZooKeeper? - Coordination Services
7. SQL vs NoSQL and Database Comparisons
	1. SQL vs NoSQL - Who Wins?
	2. MySQL vs PostgreSQL - Who Wins?
	3. What's VoltDb and Why Do We Care About It?
	4. Is Google Spanner the BEST Database?
	5. MongoDB vs. Apache Cassandra - Who Wins?
	6. WTF is Hadoop?
	7. What's HBase and how does it compare to Cassandra?
8. Batch and Stream Processing
	1. WTF is MapReduce?
	2. The Right Way to do Batch Job Data Joins
	3. You Should Be Using Spark, Not MapReduce
	4. What's Stream Processing + When Do We Use It?
	5. Kafka vs. RabbitMQ - who wins and why?
	6. Stop messing up your stream processing joins!
	7. Apache Flink - A Must-Have For Your Streams
9. Search and Time Series Databases
	1. Search Indexes - Why do we need them?
	2. What's ElasticSearch Used For?
	3. How are Time Series Databases SO FAST?
	4. How are Graph Databases So Fast?? (Neo4j)
	5. GeoSpatial Indexes - Why You Need Them
10. Caching and Content Delivery
	1. Introduction to Distributed Caching
	2. Distributed Cache Writes: What You Have To Know
	3. Cache Evictions: Don't Mess Them Up
	4. Redis vs. Memcached - Who Wins?
	5. Content Delivery Networks - You Need Them
11. Object Storage and Networking
	1. What Are Object Stores Used For? [S3]
	2. Load Balancing - The Right Way To Do It
	3. TCP vs. UDP in 12 minutes
	4. Long Polling, Websockets, Server Sent Events - Who Wins?
12. System Architecture Paradigms
	1. Monolith Vs. Microservices + Docker + Kubernetes