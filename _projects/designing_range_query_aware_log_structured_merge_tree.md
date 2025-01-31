---
layout: page
title: Range Reduce
description: A Range Query-Driven Compactions in Log-Structured Merge Trees
img: assets/img/range_reduce_3.png
importance: 1
category: Ongoing
---

<div class="row justify-content-sm-center">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/range_reduce_1.png" title="cyber" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.html path="assets/img/range_reduce_2.png" title="path traversal" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

Log-structured merge (LSM) trees are the backbone of modern databases, powering high-ingestion workloads in systems like RocksDB, Cassandra, and LevelDB. However, they suffer from poor range query performance due to high read amplification, redundant merging, and excessive compactions.  

## **Problem: Excessive Reads & Merging**  
LSM-trees store data in multiple sorted runs across hierarchical levels. While this design optimizes writes, it creates inefficiencies for range queries:  

- **High Read Amplification:** Queries must scan and merge multiple sorted runs, leading to excessive disk I/O and CPU usage.  
- **Redundant Work:** Repeated queries must reprocess and merge the same data, wasting resources.  
- **Compaction Overhead:** Frequent updates and deletes generate "logically invalid" entries, which persist until removed by costly compactions.  

## **Introducing RangeReduce**  
RangeReduce is a novel optimization that **piggybacks on range queries** to improve future performance by proactively compacting data. Instead of repeatedly reading and merging duplicate entries, RangeReduce:  

1. **Sort-merges data once** during a range query.  
2. **Writes back only valid entries** at a higher level in the LSM-tree.  
3. **Reduces read and space amplification** for subsequent queries.  

<center>
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.html path="assets/img/range_reduce_3.png" title="path traversal" class="img-fluid rounded z-depth-1" %}
    </div>
</center>

By eliminating duplicate entries early and delaying unnecessary compactions, RangeReduce speeds up range queries and reduces database bloat.  

## **The Trade-Off**  
While RangeReduce improves query performance, it comes with a slight increase in write amplification since it writes data during range queries. However, this trade-off is balanced by fewer overall compactions and better resource utilization.  

## **Real-World Impact**  
Implemented on RocksDB, RangeReduce shows significant improvements in range query performance, reducing read amplification and compaction overhead. For workloads with frequent updates and deletes, it ensures databases remain fast and efficient.  

<center>
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.html path="assets/img/range_reduce_4.png" title="path traversal" class="img-fluid rounded z-depth-1" %}
    </div>
</center>

## **Conclusion**  
RangeReduce represents a **new approach to LSM-tree optimization**, tackling one of its biggest challenges—slow range queries. By leveraging existing reads to optimize future queries, it brings **better space utilization, lower read amplification, and fewer compactions** to modern storage engines.

---

#### For more details, check out:
- 📄 [View the Poster](https://nedbday.github.io/2025/download/posters/RangeReduce_Range_Query_Driven_Compactions_in_LSM-Engine.pdf)  
- 🐙 [GitHub Repository](https://github.com/SSD-Brandeis/LSMQueryDrivenCompaction)