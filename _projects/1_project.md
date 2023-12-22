---
layout: page
title: Query-Driven Compactions
description: Range Query-Driven Compactions in Log-Structured Merge (LSM) Trees
img:
importance: 1
category: Ongoing
---

LSM-trees are central to several modern NoSQL data stores due to their superior ingestion performance. However, this benefits from poor range query performance and increased write amplification. This project introduces a new family of compaction strategies triggered by range queries. The objective is to reduce data movement and lower I/O costs for future range queries.