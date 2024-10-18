---
id: architecture
title: HySDS Architecture
---

# HySDS Architecture Overview

## Key Components

1. **GRQ (Geospatial Data Management)**: Provides faceted search and data flow management through production rules and actions.
2. **Mozart (Job Management)**: Manages jobs, queues, and production rules.
3. **Verdi Workers**: Distributed compute nodes that scale automatically for high throughput data processing.
4. **Metrics**: Real-time monitoring of job and worker metrics.
5. **Factotum**: Keeps workers "hot" for low-latency processing.

This architecture allows scalable, fault-tolerant processing across AWS, HECC, and on-premise environments.
  
