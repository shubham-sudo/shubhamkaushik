---
layout: page
title: FluidLSM
description: An Adaptive LSM-Tree for Dynamically Shifting Workloads
img:
importance: 1
category: Ongoing
---

Log-Structured Merge (LSM) trees are the backbone of many modern NoSQL key-value data stores — powering systems like RocksDB, LevelDB, and Cassandra. They offer excellent write throughput, but their performance is highly sensitive to configuration: leveled LSM-trees favor read-heavy workloads, while tiered designs perform best under write-heavy conditions.

The problem is that real-world workloads are not static. They exhibit **dynamic, diurnal, and bursty patterns** — and a single fixed configuration cannot deliver consistently optimal performance across all phases.

## The Problem

Reconfiguring an LSM-tree today requires restarting or reorganizing the storage engine, which introduces downtime, operational overhead, and significant disruption. For workloads that shift daily or hourly, this is impractical.

Beyond restarts, the LSM design space is enormous. Parameters include size ratios, compaction policies, file-picking strategies, per-level compression settings, and various memtable implementations. Finding an optimal configuration through trial and error is time-consuming and largely infeasible for production systems.

## Introducing FluidLSM

**FluidLSM** is an adaptive LSM-tree that continuously monitors workload characteristics and dynamically transitions between internal LSM shapes — without requiring database restarts.

FluidLSM adjusts the following parameters at each level, at runtime:

- **Size ratios** — tuned per level based on current read/write pressure
- **Number of runs** — controlling the leveled-to-tiered spectrum
- **Compaction and file-picking policies** — switched dynamically to match access patterns
- **Compression settings** — adapted to balance CPU and I/O trade-offs
- **Memtable implementation and size** — varied to optimize ingest throughput vs. read latency

### The Learning Component

A key challenge is determining the right configuration for unseen or unpredictable workloads. Traditional rule-based tuning cannot capture the high-dimensional LSM design space.

FluidLSM addresses this by learning which LSM-state transitions and parameter choices yield lower latency and lower amplification under various workload conditions. Through both exploration and exploitation, FluidLSM becomes increasingly effective at optimizing for diverse and evolving workloads.

### Hybrid Layouts

FluidLSM can select and combine hybrid data layouts — such as i-leveling — whenever they offer better trade-offs for the active workload phase. This allows FluidLSM to move smoothly along the spectrum between leveled, tiered, and hybrid designs.

## Goals

By fluidly adapting to changing workload conditions, FluidLSM aims to:

- Provide **more stable performance** across workload shifts
- Reduce **write amplification** during ingestion bursts
- Improve **read efficiency** during query-intensive periods
- Eliminate **operational downtime** caused by reconfiguration

---
