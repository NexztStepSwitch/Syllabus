# 6 — Databases (Relational & NoSQL)

> **Module rating:** ★★★★★ (Mandatory) · **Difficulty:** Intermediate → Advanced · **Est. effort:** 2 weeks · **Depth target:** Interview + Production
> **Prerequisites:** [Core Java](2_core_java.md); pairs with [Spring Data JPA](3_spring_and_spring_boot.md).
> **Nav:** [◀ Microservices](5_microservices_distributed_systems.md) · [Next ▶ API/Security](7_api_security_networking.md) · **Related:** [System Design](4_system_design.md), [Performance](10_performance_profiling_reliability.md)

---

## Why this module

Databases are where correctness and performance are won or lost. The two highest-ROI real skills — **transaction/isolation reasoning** and **indexing + query tuning** — are also perennial interview topics, and **"database selection"** is now a named axis in system-design rubrics. Fintech interviews probe ACID and concurrency hard.

---

## Core (Interview + Production)

### Transactions, ACID, isolation, locking — ★★★★★ · Advanced · 3 days
- **Why:** correctness under concurrency; the source of subtle production bugs.
- **What exactly:** ACID; isolation levels (Read Uncommitted → Serializable) and the anomalies each prevents (dirty/non-repeatable/phantom reads); MVCC (Postgres); optimistic vs pessimistic locking; deadlocks (causes + avoidance); lost updates.
- **How deeply:** Interview + Production — pick the right isolation level and reason about anomalies.
- **Interview Qs:** "difference between Repeatable Read and Serializable?"; "what anomaly does Read Committed still allow?"; "optimistic vs pessimistic locking — when each?"; "how do two transactions deadlock and how do you prevent it?"
- **Red flags:** defaulting to Serializable everywhere (throughput death); ignoring lost updates on read-modify-write; long transactions holding locks across network calls.
- **Misconception:** "higher isolation is always better" — it trades throughput and can increase deadlocks.

### Indexing + `EXPLAIN` + query tuning — ★★★★★ · Intermediate → Advanced · 3 days
- **Why:** the single most impactful performance skill; the fix for most slow endpoints.
- **What exactly:** B-tree indexes, composite index column order (leftmost-prefix), covering indexes, selectivity/cardinality, when an index *hurts* (write amplification), reading `EXPLAIN`/`EXPLAIN ANALYZE` (seq scan vs index scan, estimated vs actual rows), N+1 at the SQL level.
- **Interview Qs:** "this query is slow — how do you diagnose?" (EXPLAIN → check for seq scan/bad plan → add/adjust index); "composite index `(a,b)` — which queries use it?"; "why can too many indexes hurt?"
- **Red flags:** adding indexes blindly; wrong composite column order; `SELECT *`; functions on indexed columns preventing index use.
- **Related:** [N+1 in JPA](3_spring_and_spring_boot.md), [Performance](10_performance_profiling_reliability.md).

### SQL fluency — ★★★★★ · Intermediate · 2 days
- **What exactly:** joins (inner/outer/self), GROUP BY + HAVING, subqueries, **window functions** (ROW_NUMBER, RANK, running totals), **CTEs** (incl. recursive), set ops.
- **Interview Qs:** "top-N per group" (window functions); "second-highest salary"; "running total"; "find duplicates."
- **Red flags:** cartesian joins; aggregating without understanding grouping; N+1 from app instead of a join.

### Schema design & normalization — ★★★★☆ · Intermediate · 1 day
- **What exactly:** normalization (1NF–3NF) vs deliberate **denormalization** for read performance, choosing keys, constraints, when to store JSON columns.
- **Interview Qs:** "when do you denormalize?"; "trade-offs of a JSON column vs normalized tables?"

### Sharding & replication — ★★★★☆ · Advanced · 1 day
- **What exactly:** leader/follower replication + lag, read replicas, sharding (hash/range/geo), resharding, cross-shard queries, hotspots.
- **Interview Qs:** "how do you scale reads?" (replicas + cache); "how do you scale writes?" (sharding); "downsides of read replicas?" (staleness).
- **Related:** [System Design replication/sharding](4_system_design.md).

### NoSQL selection — ★★★★☆ · Intermediate · 2 days
- **Why:** "which database and why" is a core design question — the skill is *matching store to access pattern*.
- **What exactly (decision table):**

| Store | Model | Use when | Watch out for |
|-------|-------|----------|---------------|
| **PostgreSQL/MySQL** | relational | transactions, joins, strong consistency | scaling writes |
| **Redis** | in-memory KV | cache, rate limiter, locks, leaderboards | durability, memory limits |
| **MongoDB** | document | flexible schema, nested docs | multi-doc transactions, joins |
| **Cassandra** | wide-column | massive write throughput, time-series, AP | query flexibility, tombstones |
| **DynamoDB** | KV/doc (managed) | serverless scale, predictable latency | access-pattern-first modeling, cost |
| **Elasticsearch** | search index | full-text search, analytics | source of truth (don't) |

- **Interview Qs:** "SQL vs NoSQL for X?"; "why Cassandra over Postgres for write-heavy time-series?"; "model this in DynamoDB (single-table)."
- **Red flags:** picking NoSQL to "scale" without an access-pattern reason; using a search index as system of record.

### Migrations — ★★★☆☆ · Intermediate · 0.5 day
- **What exactly:** Flyway/Liquibase, versioned + backward-compatible migrations, expand-contract for zero-downtime schema changes.
- **Interview Qs:** "how do you add a NOT NULL column with no downtime?" (expand → backfill → contract).

## Situational
- **Time-series DBs (Influx/Timescale/Prometheus storage) — ★★☆☆☆:** metrics/monitoring; awareness. See [Observability](8_observability_monitoring_logging.md).
- **Object storage (S3) + backups/DR — ★★★☆☆:** large blobs, lifecycle, RPO/RTO awareness.

---

## Hands-on labs & failure scenarios

- **Lab 1:** create a slow query on a seeded table; use `EXPLAIN ANALYZE`; add a composite index; measure before/after.
- **Lab 2:** reproduce a deadlock with two concurrent transactions; fix via consistent lock ordering / lower isolation / retry.
- **Lab 3:** write top-N-per-group with a window function; then the running-total query.
- **Lab 4:** do a zero-downtime column add (expand-contract) with Flyway.
- **Failure scenario:** read replica lag causes a user to not see their own write — implement read-your-writes (route to leader / sticky).
- **Debugging task:** an endpoint issues 200 queries per request — find the N+1 and fix at the SQL/JPA layer.

---

## Checklists

### Interview Checklist
- **Must know:** isolation levels + anomalies; optimistic vs pessimistic locking; deadlocks; indexing + `EXPLAIN`; composite index order; joins/windows/CTEs; SQL vs NoSQL selection; sharding vs replication.
- **Good to know:** MVCC; denormalization trade-offs; DynamoDB single-table modeling; migrations/expand-contract.
- **Bonus:** time-series stores; multi-region consistency.

### Production Checklist
- **Must know:** short transactions (no network calls inside); appropriate isolation; indexes justified by query plans; backups tested.
- **Good to know:** replica lag handling; slow-query monitoring; connection-pool sizing.

### Hands-on Checklist
- **Must:** tuned a query with EXPLAIN; reproduced + fixed a deadlock; wrote window-function queries.
- **Good:** zero-downtime migration; modeled a table for DynamoDB.
- **Bonus:** benchmarked replica-read staleness.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above.

**1. Fundamentals**
- Relational vs non-relational; OLTP vs OLAP; ACID vs BASE

**2. Relational (RDBMS)**
- Modeling: ER diagrams, normalization (1NF–BCNF), denormalization trade-offs
- SQL: SELECT/INSERT/UPDATE/DELETE; joins (inner/outer/cross/self); GROUP BY / HAVING / ORDER BY
- Advanced SQL: window functions, CTEs, subqueries, aggregate patterns
- Indexing: B-Tree vs hash, clustered vs non-clustered, composite indexes, covering indexes, index selectivity
- Transactions: isolation levels (Read Uncommitted → Serializable), anomalies (dirty/non-repeatable/phantom), locking, deadlocks, MVCC
- Views, stored procedures, triggers (use judiciously)

**3. Query performance**
- `EXPLAIN` / `EXPLAIN ANALYZE`; reading query plans; seq scan vs index scan
- Query tuning; N+1 problem; connection pooling (HikariCP)
- Caching strategies (Redis/Memcached) → see [System Design](4_system_design.md)

**4. NoSQL**
- Types & when to use: key-value (Redis, DynamoDB), document (MongoDB), wide-column (Cassandra, HBase), graph (Neo4j)
- Data modeling by access pattern (query-first); denormalization; aggregations
- CAP considerations per store; consistency tunables

**5. Scaling & distribution**
- Partitioning & sharding (hash/range/geo); shard keys & hot partitions
- Replication (leader-follower, multi-leader, quorum); read replicas & replication lag
- Distributed transactions; consistency models; time-series DBs (awareness)

**6. Schema evolution & operations**
- Migrations: Flyway / Liquibase; backward-compatible changes; zero-downtime migrations
- Backups, PITR (awareness)

**7. Security**
- AuthN/authZ, role-based access; encryption (TDE, column-level); SQL injection prevention (parameterized queries)

**8. Practice & interview**
- Schema for e-commerce / social media; MongoDB aggregation for analytics; scaling reads with replicas
- SQL vs NoSQL trade-offs; how to scale a DB; ensure availability vs consistency; optimize a slow query

---

**Nav:** [◀ Microservices](5_microservices_distributed_systems.md) · [Next ▶ API, Security & Networking](7_api_security_networking.md)
