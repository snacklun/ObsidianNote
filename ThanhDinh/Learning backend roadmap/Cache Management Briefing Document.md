## 1. Overview of Cache Replacement Policies

Cache replacement policies, also known as cache algorithms, are crucial for optimizing computer program and hardware performance by managing cached information. Caching stores frequently used or recent data in faster memory locations, reducing access time to main memory. When a cache is full and new data needs to be stored, an algorithm must decide which existing items to discard.

The effectiveness of a cache is measured by two primary metrics: **latency** (how quickly an item is returned) and **hit ratio** (how often a requested item is found in the cache). "More efficient replacement policies track more usage information to improve the hit rate for a given cache size. The latency of a cache describes how long after requesting a desired item the cache can return that item when there is a hit." Each policy represents a compromise between these two factors.

### ✅ Correct Formula for **Average Memory Access Time (AMAT)**

T=Th+m×Tm+ET = T_h + m \times T_m + E

T=Th+m×Tm+E

where:

- ThT_hTh = **cache hit time** (time to access data if it's in the cache)
- mmm = **miss ratio** =1−hit ratio= 1 - \text{hit ratio}=1−hit ratio
- TmT_mTm = **miss penalty** (additional time to fetch from main memory or next level)
- EEE = **secondary effects** (queuing, contention, etc.)

---

### 🧠 Intuitive Explanation

- On a **hit**, you only pay the cache access time ThT_hTh.
- On a **miss**, you pay the cache access time **plus** the miss penalty TmT_mTm.
- Averaging over all accesses gives:

T=Th+m×TmT = T_h + m \times T_m

T=Th+m×Tm

And if there are additional factors (e.g., queuing delays, bus contention), you add EEE:

T=Th+m×Tm+ET = T_h + m \times T_m + E

T=Th+m×Tm+E

## 2. Key Cache Management Considerations

Beyond replacement policies, several other factors are essential for designing robust cache architecture:

### 2.1. Cache Size Estimation

Before implementation, it is vital to estimate the required cache memory. The "80/20 rule" is a common heuristic, suggesting that "20% of objects are used 80% of the time." This implies caching 20% of data can significantly improve request latency. For example, "if there were 10M daily active users in the system and each user’s metadata provided to fronted is 500k, then the size of our cache is about 500k * 10M * 0.2 = 100G".

### 2.2. Cache Clustering for Scalability

If a single server cannot hold all cached data, a **cache cluster** is necessary. Simple hash functions can map requests to cache nodes. However, "if we add one cache node to the cluster, then the data distribution will become like this," potentially requiring significant data migration. **Consistent hashing** is introduced to "minimize the number of data migration after cache cluster resizes."

### 2.3. Update Policies

Determining how to update cached data is critical for consistency and performance. Three main policies exist:

1. **Write-through**: "Update DB and cache at the same time." This ensures strong consistency but "would increase loading while writing data and is not recommended for the write-heavy scenario."
2. **Write around**: "While writing data we only update DB and invalid cache data." The cache is updated on subsequent reads. The "disadvantage is that there may be several cache misses at the very beginning of reading."
3. **Write back**: "While writing data we only update cache and write back to DB after an interval of time." This improves latency and throughput for write-heavy scenarios but carries the "obvious" risk of data loss "if the system crash before writing back."

## 3. Cache Replacement Policies in Detail

The core of cache management lies in its replacement policies, which dictate what to evict when the cache is full.

### 3.1. Optimal but Impractical: Bélády's Algorithm

The theoretical "most efficient caching algorithm would be to discard information which would not be needed for the longest time; this is known as Bélády's optimal algorithm, optimal replacement policy, or the clairvoyant algorithm." However, "since it is generally impossible to predict how far in the future information will be needed, this is unfeasible in practice."

### 3.2. Simple Queue-Based Policies

- **First In, First Out (FIFO)**: "The cache behaves like a FIFO queue; it evicts blocks in the order in which they were added, regardless of how often or how many times they were accessed before." FIFO is a common method in computing and electronics for organizing data structures, analogous to a "first-come, first-served (FCFS) basis." It can be implemented with hardware shift registers, circular buffers, or linked lists.
- **Last In, First Out (LIFO)**: "The cache evicts the block added most recently first, regardless of how often or how many times it was accessed before." This behaves like a stack.
- **SIEVE**: "designed specifically for web caches," SIEVE uses "lazy promotion and quick demotion." It uses a single FIFO queue with a "moving hand" and a single bit of metadata to quickly evict "one-hit-wonder" objects.

### 3.3. Simple Recency-Based Policies

- **Least Recently Used (LRU)**: "Discards least recently used items first." This is a widely used algorithm, requiring tracking "age bits" for cache lines. LRU is "a family of caching algorithms, that includes 2Q by Theodore Johnson and Dennis Shasha and LRU/K by Pat O'Neil, Betty O'Neil and Gerhard Weikum."
- **Time-aware, Least-Recently-Used (TLRU)**: A variant for content with a "valid lifetime," introducing "TTU (time to use)" to manage content usability based on locality and publisher.
- **Segmented LRU (SLRU)**: Divides the cache into probationary and protected segments. Hits move to the protected segment, giving items accessed twice a better chance of retention.
- **LRU Approximations (e.g., Pseudo-LRU (PLRU), Clock-Pro)**: For high associativity caches where true LRU is expensive, PLRU "needs only one bit per cache item" and offers similar performance with lower overhead. Clock-Pro is an approximation of LIRS, "as complex as Clock, and is easy to implement at low cost." The Linux buffer-cache combines LRU and Clock-Pro.
- **Most Recently Used (MRU)**: "discards the most-recently-used items first." This policy is effective for "looping sequential reference pattern[s]" and "random access patterns and repeated scans over large datasets," where "the older an item is, the more likely it is to be accessed."

### 3.4. Simple Frequency-Based Policies

- **Least Frequently Used (LFU)**: "counts how often an item is needed; those used less often are discarded first." This involves assigning a counter to each cache block, incrementing it on access, and evicting the block with the lowest count when the cache is full.
- **Problems with LFU**: LFU can keep "an item in memory which is referenced repeatedly for a short period of time and is not accessed again for an extended period of time," leading to cache pollution. Also, "new items that just entered the cache are subject to being removed very soon again, because they start with a low counter." Due to these issues, pure LFU is uncommon, with hybrids often preferred.
- **Least Frequent Recently Used (LFRU)**: Combines LFU and LRU benefits, dividing the cache into privileged (LRU) and unprivileged (approximated LFU) partitions.
- **LFU with Dynamic Aging (LFUDA)**: "uses dynamic aging to accommodate shifts in a set of popular objects." It adds a cache-age factor to reference counts to prevent once-popular but now-unpopular items from staying in the cache too long.
- **S3-FIFO**: A 2023 algorithm using "three FIFO queues: a small queue occupying 10% of cache space, a main queue that uses 90% of the cache space, and a ghost queue that only stores object metadata." It filters one-hit wonders, stores popular objects, and tracks potentially popular evicted objects.

### 3.5. Policies Approximating Bélády's Algorithm

These policies attempt to predict future reuse patterns to mimic the optimal Bélády's algorithm.

- **Re-Reference Interval Prediction (RRIP)**: A flexible Intel policy that assigns a "re-reference prediction value (RRPV)" to each cache line, correlating with its expected reuse time. Lines with high RRPV are evicted first.
- **Static RRIP (SRRIP)**: Inserts lines with the maximum RRPV, making them most likely to be evicted.
- **Bimodal RRIP (BRRIP)**: Addresses cache thrashing when the working set is larger than the cache by occasionally inserting lines with a slightly lower RRPV, causing them to "stick."
- **Dynamic RRIP (DRRIP)**: "uses set dueling" to adaptively choose between SRRIP and BRRIP based on performance.
- **Hawkeye**: "attempts to emulate Bélády's algorithm by using past accesses by a PC to predict whether the accesses it produces generate cache-friendly (used later) or cache-averse accesses (not used later)." It feeds this prediction into an RRIP backend. Hawkeye won the CRC2 cache championship in 2017.
- **Mockingjay**: Aims to improve on Hawkeye with "more fine-grained decisions" and updates "estimated time of reuse (ETR)" based on sampled accesses and temporal difference learning. It has "results which are close to the optimal Bélády's algorithm."

### 3.6. Other Advanced Policies

- **Low Inter-reference Recency Set (LIRS)**: Achieves better performance than LRU by using "recency to evaluate inter-reference recency (IRR) to make a replacement decision."
- **Adaptive Replacement Cache (ARC)**: "constantly balances between LRU and LFU to improve the combined result." It adaptively adjusts segment sizes based on evicted items.
- **Clock with Adaptive Replacement (CAR)**: Combines ARC and Clock, offering comparable performance to ARC and outperforming LRU and Clock without user-specified parameters.
- **Multi-Queue (MQ)**: Developed for second-level buffer caches, it uses "an _m_ number of LRU queues" with different lifetimes.
- **Pannier**: A "container-based flash caching mechanism" that ranks containers by "survival time," which is proportional to live data.

## 4. Static Analysis of Cache Behavior

**Static analysis** is used to predict cache hits or misses, which helps determine the worst-case execution time of a program. For LRU caches, this involves assigning an "age" to each block and computing intervals for possible ages. However, "LRU static analysis does not extend to pseudo-LRU policies," and "static-analysis problems posed by pseudo-LRU and FIFO are in higher complexity classes than those for LRU."