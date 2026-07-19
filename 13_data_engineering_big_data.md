# 13 — Data Engineering (Kafka core; Big Data optional)

> **Module rating:** ★★★☆☆ overall — but **Kafka is ★★★★★** for backend. · **Difficulty:** Intermediate → Advanced · **Est. effort:** 3–4 days (Kafka); rest optional · **Depth target:** Production (Kafka), Awareness (rest)
> **Prerequisites:** [Microservices](5_microservices_distributed_systems.md), [System Design queues](4_system_design.md).
> **Nav:** [◀ Build & Tooling](12_build_tooling.md) · [Next ▶ Advanced/Specialist](14_advanced_specialist_topics.md) · **Related:** [System Design](4_system_design.md), [Databases](6_databases_relational_nosql.md)

---

## Why this module

**Kafka has graduated from "optional big data" to a core backend skill** — it's the default event backbone and a recurring design/deep-dive topic. The rest of "big data" (Spark, warehouses) is **role-dependent** — learn it only if you're targeting data-heavy teams.

---

## Core

### Kafka — ★★★★★ · Advanced · 3 days
- **Why:** decoupling, async processing, event-driven architectures, buffering, replay.
- **What exactly:**
  - **Model:** topics, **partitions** (parallelism + ordering-within-partition), offsets, **consumer groups** + rebalancing, replication factor + ISR, retention/compaction.
  - **Producers:** keys → partitioning, `acks` (0/1/all), idempotent producer, batching/linger.
  - **Consumers:** at-least-once (default) → **idempotent consumers**, manual vs auto commit, poison messages → **DLQ**, consumer lag, backpressure.
  - **Delivery:** why exactly-once is hard → effectively-once via idempotency/dedup + transactions.
- **How deeply:** Production — can design a topic layout and reason about ordering + delivery.
- **Interview Qs:** "how does Kafka guarantee ordering?" (per partition, via key); "at-least-once vs exactly-once?"; "how do you handle a poison message?" (DLQ + alert); "consumer lag is growing — causes + fixes?" (scale consumers/partitions, slow processing); "how do you avoid reprocessing on rebalance?" (idempotency + offset management).
- **Red flags:** expecting global ordering across partitions; auto-commit + non-idempotent processing (message loss/dup); one giant partition (no parallelism).
- **Related:** [Idempotency + delivery semantics](5_microservices_distributed_systems.md).

### ETL / ELT & pipelines — ★★☆☆☆ · Intermediate · 0.5 day (awareness)
- **What exactly:** batch vs streaming, idempotent + replayable pipelines, schema evolution, CDC (Debezium) as a bridge from DB → Kafka.
- **Interview Qs:** "how would you stream DB changes to other systems?" (CDC/outbox → Kafka).

## Situational / optional (stub)

> **Why low priority for backend:** relevant to data-platform roles, not general backend.
> **Learn only these basics:** what each is for, one line each.
> **Further reading:** vendor docs, "Designing Data-Intensive Applications."

- **Spark — ★★☆☆☆:** distributed batch/stream processing (RDD/DataFrame). Know it exists.
- **Data lake vs warehouse — ★★☆☆☆:** raw storage vs structured analytics (S3/Delta vs Snowflake/BigQuery/Redshift).
- **Flink — ★★☆☆☆:** low-latency stream processing; awareness.

---

## Hands-on labs & failure scenarios

- **Lab 1:** produce/consume with a keyed topic; observe ordering within a partition and parallelism across consumers in a group.
- **Lab 2:** build an **idempotent consumer** with a dedup store; replay a message and prove no double-processing.
- **Lab 3:** route failed messages to a DLQ; add lag monitoring.
- **Failure scenario:** a consumer crashes mid-batch with auto-commit on → messages lost; switch to manual commit + idempotency and re-test.
- **Design task:** stream order events to inventory + analytics with at-least-once + idempotency.

---

## Checklists

### Interview Checklist
- **Must know:** partitions/ordering/consumer groups; `acks` + idempotent producer; at-least-once + idempotent consumer; DLQ; consumer lag; CDC/outbox concept.
- **Good to know:** compaction; rebalancing; transactions/exactly-once trade-offs.
- **Bonus:** Spark/Flink/warehouse awareness.

### Production Checklist
- **Must know:** idempotent consumers; sensible partition count; lag alerts; DLQ + retries.
- **Good to know:** schema registry; compaction for state topics.

### Hands-on Checklist
- **Must:** built keyed produce/consume + an idempotent consumer.
- **Good:** added DLQ + lag monitoring.
- **Bonus:** wired CDC (Debezium) from a DB.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. **Kafka is core backend**; the rest is **role-dependent / optional** for general backend interviews. Priorities/depth are in the guide above.

**1. Kafka (core backend skill)**
- Architecture: brokers, topics, partitions, offsets, replication, ISR
- Producers (acks, idempotent producer, batching); consumers & consumer groups; rebalancing
- Delivery semantics: at-least-once, at-most-once, exactly-once (transactions)
- Ordering guarantees (per-partition); keys & partitioning; retention & compaction
- Dead-letter queues; consumer lag monitoring; schema registry / Avro (awareness)

**2. Data engineering fundamentals (optional)**
- ETL vs ELT; data pipelines; batch vs stream processing

**3. Big data ecosystem (optional / role-dependent)**
- Spark (RDD, DataFrames, Spark SQL); Hadoop (HDFS, MapReduce, YARN) **(mostly legacy)**; Hive/Pig **(legacy)**

**4. Streaming systems (optional)**
- Kafka Streams; Flink; Spark Streaming; Kinesis

**5. Data warehousing & lakes (awareness)**
- Warehouses: Snowflake, Redshift, BigQuery; star/snowflake schema; OLAP
- Data lakes / lakehouses: Delta Lake, Apache Iceberg

**6. Interview**
- Kafka delivery semantics & how to achieve idempotency; consumer-group rebalancing; batch vs stream; (if relevant) Hadoop vs Spark, warehouse vs lakehouse

---

**Nav:** [◀ Build & Tooling](12_build_tooling.md) · [Next ▶ Advanced/Specialist Topics](14_advanced_specialist_topics.md)
