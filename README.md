
# Concurrent Extendible Hash Table

## Authors: Shivang Dalal (shivangd), Ashwin Rao (arao2)  

**URL:** [https://sdtheslayer.github.io/Concurrent-Extendible-Hash-Table/](https://sdtheslayer.github.io/Concurrent-Extendible-Hash-Table/)

**Final Report:** [https://github.com/SDTheSlayer/Concurrent-Extendible-Hash-Table/blob/main/618%20Final%20Report.pdf](https://github.com/SDTheSlayer/Concurrent-Extendible-Hash-Table/blob/main/618%20Final%20Report.pdf)

**Presentation:** [https://github.com/SDTheSlayer/Concurrent-Extendible-Hash-Table/blob/main/618%20Presentation.pdf](https://github.com/SDTheSlayer/Concurrent-Extendible-Hash-Table/blob/main/618%20Presentation.pdf)

---

## Summary
We aim to develop a concurrent extendible hash table optimized for high-performance parallel operations, focusing on the needs of hash tables in high-performance database systems. Our implementation will emphasize efficient resizing and use compare-and-swap (CAS) atomic operations to create a scalable, concurrent hash table. This approach eliminates the overhead typically associated with lock-based schemes while maintaining data consistency in multi-threaded environments. Additionally, we will investigate the performance benefits of SIMD in the context of parallel key lookups.

---
## Background
Hash tables play a crucial role in database management systems (DBMS), particularly for joins and indexing. Traditional lock-based implementations often suffer from contention when multiple threads attempt to access the data structure simultaneously. Our lock-free design addresses these limitations by enabling parallel access without explicit synchronization mechanisms. We will also implement and compare performance with fine-grained and coarse-grained locking implementations.

### Limitations of the Locking Approach:
- Lock-based implementations create contention points.
- Traditional resizing mechanisms block concurrent access.
- Performance degradation under high parallel loads.

### Industry Applications of Extendible Hashing:
- Database indexing systems.
- In-memory caching and in-memory databases.
- High-frequency trading platforms.
- Real-time analytics systems.

---
## Technical Challenges

### Concurrency Management
- Coordinating multiple thread operations without explicit locks.
- Handling race conditions during resize operations, including managing memory allocation and deallocation in a multi-threaded environment.
- Maintaining consistency during concurrent inserts and deletes.

### Performance Optimization
Our implementation must address several critical challenges:
- Managing the overhead of CAS operations during high contention scenarios, due to the potential for a large number of continuous retries per thread.
- Balancing the benefits of parallelism with the overhead required to maintain multiple threads, finding the optimal level of parallelization for maximum performance.
- Ensuring efficient memory usage during dynamic resizing.

---
## Resources
We will draw inspiration from the following research papers on lock-free extendible hash tables:
- [Shalev and Shavit, "Split-ordered lists: Lock-free extensible hash tables," Journal of the ACM, 2006](https://ldhulipala.github.io/readings/split_ordered_lists.pdf).
- [Fatourou, Kallimanis, and Ropars, "An Efficient Wait-free Resizable Hash Table," 2018](https://tropars.github.io/downloads/pdf/publications/spaa2018-FKR-WF_ext_hashing.pdf).

---
## Project Goals and Deliverables

### Core Objectives
The project aims to achieve the following key deliverables:
- A fully functional lock-free extendible hash table implementation in C++/OpenMP, supporting concurrent insert and resize operations with atomic operations.
- Efficient resize functionality (involving memory allocation and freeing) that performs well under contention.
- Benchmarks and performance metrics to demonstrate scalability with the number of threads, focusing on metrics such as throughput and latency for each operation.
- Comparison of our implementation with traditional fine-grained and coarse-grained lock-based implementations.
- **Poster Session Demonstration**: Present scalability comparisons across implementations, workload benchmark results, and performance metrics under varied configurations.

### Extended Objectives
- Exploring the performance benefits of SIMD parallelization for concurrent key lookups and other hash table operations.

### Evaluation Criteria
- Performance comparison with traditional locking-based implementations, focusing on throughput and latency.
- Scalability testing under varying loads and different thread counts.
- Memory efficiency measurements.

---
## Platform Choice
We chose OpenMP for CPU-based implementations, leveraging its simplicity and support for parallelism. For SIMD, we will use ISPC due to our familiarity with its usage. C++ is well-suited for the task due to its support for high-performance data structures and low-level memory management. Additionally, most widely-used open-source databases, such as PostgreSQL, are written in C/C++.

---
## Schedule
- **11/7 - 11/13**: Research and finalize project proposal. Conduct a literature review on the current state of research.
- **11/14 - 11/20**: Implement hash table with coarse-grained and fine-grained locks.
- **11/21 - 11/27**: Begin implementation of the lock-free version and draft milestone report.
- **11/28 - 12/4**: Complete the lock-free version, validate, and benchmark against locked versions. Start SIMD optimizations for lookups.
- **12/5 - 12/13**: Consolidate results, fine-tune implementation, and prepare poster and final report.

---


# Milestone Report

## Project Status Summary

The implementation of the Concurrent Extendible Hash Table project is progressing according to schedule. We have completed the initial research phase and have implemented the coarse-grained locking version of the hash table (with testing for inserts, retrievals, and deletes). 

We are currently working on two parallel implementations:
- Fine-grained locking version of the concurrent hash table and corresponding test suite
- A lock-free implementation of the extendible hash table based on a concurrent linked list

## Completed Work

- Comprehensive literature review of the lock-free extendible hash table
- Implementation of baseline hash table with coarse-grained locking
- Testing the coarse-grained locking implementation with inserts, retrievals and deletes
- Initial attempt of fine-grained locking version, pending bug fixes

## Pending Work

- Complete implementing and testing the fine-grained implementation
- Continue implementing the concurrent linked list and lock-free extendible hash table
- Benchmark and compare the performance of each

## Goals and Deliverables Status

**On Track:**
- Basic hash table implementation
- Coarse-grained and fine-grained locking versions

**In Progress:**
- Lock-free implementation using CAS operations
- Performance benchmarking framework

**Stretch Goals:**
- Efficient resize operations for the lock-free extendible hash table
- SIMD optimization research

## Updated Schedule

**Week of December 2-8:**
- Ashwin: Complete lock-free implementation
- Shivang: Finish fine-grained locking and benchmarking framework

**Week of December 9-13:**
- Both: Performance optimization and benchmarking
- Both: Poster and final report preparation

## Poster Session Plans

Our poster session will showcase comprehensive visual representations of our concurrent hash table's performance characteristics through:
- Comparing throughput scaling across different thread counts for all three implementations
- Latency distribution charts for all three implementations
- Memory utilization graphs

## Preliminary Results

Initial results show correct behavior of coarse-grained locking implementation in both single-threaded and multi-threaded environments. The fine-grained locking implementation and benchmark suite are in progress.

## Technical Concerns

**Current Challenges:**
- Memory errors in fine-grained locking
- Sparse errors in multithreaded inserts into the coarse-grained locking implementation

**Other Challenges:**
- Ensuring correctness of CAS operations during resize operations
- Optimizing SIMD implementation for key lookups
- Memory management in concurrent scenarios

No major blockers have been identified, and the project remains on track for successful completion by the deadline.
