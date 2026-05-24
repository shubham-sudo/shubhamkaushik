---
layout: page
title: "Tectonic+"
description: A Benchmarking Framework aims to Replace YCSB for Key-Value Stores
importance: 1
category: Ongoing
---

Key-value stores are evaluated against benchmarks that were never designed to reflect how modern production systems actually behave today.
**YCSB**, **KVBench**, and **db_bench** generate static, uniform workloads — fixed operation mixes, random keys, and benchmark one database at a time. 
Real production traffic __shifts over time__, uses structured keys with skewed access patterns, and mixes operations that don't fit neatly into any of YCSB's six labeled workloads.

**Tectonic+** is the next generation of the [Tectonic](../tectonic/) benchmarking framework — rebuilt from the ground up as a benchmarking system to become the default suite for key-value stores.

## The Gap Tectonic+ Closes

YCSB was designed for a different era. It has no model of:

- **Shifting Workloads**: The production traffic shifts dynamically; state-of-the-art misses this entirely.
- **Skewed Access**: The composite keys and biased distributions are normal in modern applications.
- **Mixed Operation**: State-of-the-art benchmarks ignores generation of various types of operations.
- **Side-by-side Evaluation**: Comparing storage engines requires a unified framework.

## Architecture

Tectonic+ is structured as three tightly integrated layers:

**Workload Generator (`tectonic`)**: A Rust-based workload generator that expects JSON specification input file. Workloads are expressed as a hierarchy of _sections_ (isolated key spaces) and _groups_ (interleaved operation sets), giving precise control over when operations share keys and when they don't.

**Database Layer (`db-layer`)**: A unified abstraction over multiple storage backends, compiled in as optional features. Currently supports:
- RocksDB
- Apache Cassandra
- Redis
- ScyllaDB

**CLI (`tectonic-cli`)**: Three composable commands:
- `generate`: produces a reproducible workload file from a spec
- `execute`: replays a workload file against any supported database
- `benchmark`: generates and executes in one step for fast iteration

Separating generation from execution means the exactly same workload can be replayed across different storage engines, database configurations, or hardware — __a property that YCSB cannot guarantee__.

## Workload Expressiveness
Tectonic+ supports a wide range of operation and operation-specific distribution for generating realistic workloads and benchmarking multiple key-value data store.

### Key & Value Generation
Keys and values are specified as composable `StringExpr`s:
- **Uniform**: random alphanumeric strings of variable length
- **Constant**: fixed values for controlled experiments
- **Segmented**: structured composite keys (e.g., `usertable:user1234`)
- **Weighted**: probabilistic mix of any other generators (e.g., 30% `user`, 40% `post`, 30% `userfeed`)
- **HotRange**: biased prefix generation to simulate skewed tenant or partition access

## Multi-Phase Workloads
The sections/groups model enables workloads that change over time without any code:

```json
"sections": [
  { "groups": [{ "inserts": { "op_count": 900000 }, "point_queries": { "op_count": 100000 } }] },
  { "groups": [{ "inserts": { "op_count": 100000 }, "point_queries": { "op_count": 900000 } }] },
  { "groups": [{ "range_queries": { "op_count": 500000 }, "updates": { "op_count": 100000 } }] }
]
```

This spec models a three-phase workload: write-heavy preload, then a read-heavy query phase, then a mixed range-query and update phase — the kind of traffic pattern that is common in real systems and completely absent from YCSB.

## Goal

Tectonic+ is being built to be the benchmark that the key-value store research community can converge on — one that generates reproducible, multi-database, workload-realistic experiments and makes YCSB's limitations a thing of the past.

---

#### Resources
- 🐙 [GitHub Repository](https://github.com/SSD-Brandeis/tectonic)
