---
layout: page
title: Range Deletes
description: Range Deletes in Log-Structured Merge (LSM) Trees
img: 
redirect: 
importance: 2
category: Ongoing
---

Out-of-place data structures, like LSM-trees, perform data deletion logically without physically deleting the target data objects. This project, introduces a range delete filter to avoid unnecessary I/Os to storage by keeping a minimal metadata structure in memory. The objective is to reduce the number of I/Os and improve the performance of range deletes.