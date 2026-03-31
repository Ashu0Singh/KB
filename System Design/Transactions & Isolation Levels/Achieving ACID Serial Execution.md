[Video](https://www.youtube.com/watch?v=kN_rOaNZBng&list=PLjTveVh7FakLdTmm42TMxbN8PvVn5g4KJ&index=11)

This video explains Actual Serial Execution as a database concurrency control technique, focusing on how databases like VoltDB achieve high performance and ACID compliance by avoiding multi-threading bottlenecks (0:26).

# Key Concepts

Single-Threaded Execution: To achieve full serialisability without complex locking, the system runs all transactions serially—one after another—on a single CPU core.

Performance Trade-offs: While simple, this approach is bottlenecked by the speed of reads and writes. Running on a single core necessitates optimisations to prevent system slowdowns.

# Performance Optimisations

In-Memory Database: To maximize speed, data should be kept in RAM rather than on slow disk storage. While fast, this raises challenges regarding data durability if power is lost.
Network Bottlenecks: Network latency is a major limiting factor. Sending large SQL queries over the network slows down execution.
Stored Procedures: Instead of sending full SQL scripts, developers should use stored procedures. By pre-loading functions onto the database and only sending small parameters over the network, bandwidth usage is minimized.

# Pros and Cons of Stored Procedures

Pros: Significantly reduces data sent over the network, allowing faster execution on the single thread.
Cons: Can be difficult for developers to maintain, version control, and deploy across database replicas.
