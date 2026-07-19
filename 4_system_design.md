# 4 — System Design (HLD + LLD)

> **Module rating:** ★★★★★ (Mandatory) · **Difficulty:** Intermediate → Advanced · **Est. effort:** 3–4 weeks (ongoing) · **Depth target:** Interview + Expert
> **Prerequisites:** [Core Java](2_core_java.md), [Databases](6_databases_relational_nosql.md), [Microservices](5_microservices_distributed_systems.md) concepts.
> **Nav:** [◀ Spring](3_spring_and_spring_boot.md) · [Next ▶ Microservices](5_microservices_distributed_systems.md) · **Related:** [Databases](6_databases_relational_nosql.md), [Performance](10_performance_profiling_reliability.md), [Observability](8_observability_monitoring_logging.md)

---

## Why this module (2026 framing)

**System design carries more of the hiring decision than ever.** As coding got easier to game with AI, design + behavioral separate candidates. Two things are newly, *explicitly* graded in 2026:

1. **Cost reasoning** — "add more servers" is a failing answer. You must estimate infra cost and name the biggest driver.
2. **Failure modes + operations** — observability, degradation, and recovery are on the rubric, not bonus points.

There are two distinct rounds. Treat them separately:
- **HLD** (distributed architecture) — ★★★★★
- **LLD / machine coding** (OOP class design) — ★★★★★, heavily weighted at product/fintech (esp. India).

---

## The universal HLD framework — ★★★★★ · Intermediate · practice weekly

Every strong answer follows this shape (interviewers grade the *habit*):

```
1. Clarify        functional + non-functional reqs, RPS, read/write ratio,
                  latency SLA, consistency need, data size
2. Estimate       back-of-envelope: QPS, storage/day, bandwidth, cache size
3. High-level     API contract → core components → data flow (draw it)
4. Deep-dive      pick 1–2 components; go deep on data model + algorithms
5. Scale          bottleneck move for each layer: LB, cache, shard, replicate, queue
6. Cost + Ops     $ drivers, failure modes, observability, degradation, recovery
7. Trade-offs     defend choices; state what you gave up
```

- **Red flags:** designing before clarifying; skipping capacity math; name-dropping Kafka/Cassandra without stating the property it provides; ignoring cost/failure.
- **Differentiator:** knowing **when NOT** to add a queue/cache/mesh (a senior signal).

---

## Tier-1 building blocks (appear in nearly every design)

### Caching — ★★★★★ · Intermediate · 2 days
- **Why:** the most common optimization; nearly every system is read-heavy.
- **What exactly:** cache-aside (default), write-through, write-behind, TTL + invalidation; **cache stampede** (locking, request coalescing, early expiry); **hot keys** (celebrity problem → replication/local cache); **consistent hashing** for distribution; eviction (LRU/LFU); local vs distributed (Redis).
- **Interview Qs:** "cache-aside vs write-through?"; "how do you invalidate?"; "handle a cache stampede/hot key?"; "how does consistent hashing minimize reshuffling?"
- **Red flags:** unbounded cache; no invalidation strategy; caching write-heavy data.
- **Related:** [Redis](6_databases_relational_nosql.md), [Performance](10_performance_profiling_reliability.md).

### Load balancing + horizontal scaling — ★★★★★ · Intermediate · 1 day
- **What exactly:** L4 vs L7, algorithms (round-robin, least-conn, consistent hashing), health checks, sticky sessions (and why to avoid them → stateless services), horizontal vs vertical.
- **Interview Qs:** "how do you make a service horizontally scalable?" (statelessness, externalized session/state).

### Replication + sharding — ★★★★★ · Advanced · 2 days
- **What exactly:** leader/follower replication, replication lag + read-your-writes, multi-AZ; sharding strategies (range/hash/geo), resharding pain, hotspots, cross-shard queries/joins.
- **Interview Qs:** "how do you shard a users table?"; "how do you handle a celebrity hotspot?"; "read replica lag — how does it bite you?"
- **Related:** [DB sharding](6_databases_relational_nosql.md).

### Consistency, CAP & PACELC — ★★★★★ · Advanced · 1 day
- **Why:** the central distributed-systems trade-off; appears in almost every design with distributed data.
- **What exactly:** strong vs eventual consistency (per data type), CAP (choose CP vs AP under partition), **PACELC** (latency vs consistency even without partitions), quorums (R+W>N), read-your-writes/monotonic reads.
- **Interview Qs:** "where do you need strong consistency and where is eventual OK?" (justify per data type — money = strong, feed = eventual).
- **Misconception:** "CAP means pick 2 of 3 always" — partitions are rare; the real everyday trade-off is PACELC's latency-vs-consistency.

### Rate limiting — ★★★★☆ · Intermediate · 1 day
- **What exactly:** token bucket (bursts), leaky bucket, sliding window log/counter; **distributed** via Redis (Lua for atomic incr-and-check, sorted sets for sliding window); local approximation + periodic sync for scale; where to enforce (edge/gateway/service); return `429` + `Retry-After`.
- **Interview Qs:** "design a distributed rate limiter"; "token bucket vs sliding window?"; "how do you avoid race conditions across nodes?" (Redis Lua atomicity).
- **Related:** [API/Security](7_api_security_networking.md).

### Message queues / Kafka in design — ★★★★★ · Advanced · 2 days
- **Why:** decoupling, async processing, buffering, event-driven architectures.
- **What exactly:** when a queue helps (and when it doesn't); Kafka partitions (parallelism + ordering-within-partition), consumer groups, retention/replay, delivery semantics (at-least-once default → idempotent consumers), DLQ, poison messages, backpressure.
- **Interview Qs:** "why a queue here?"; "how do you guarantee ordering?"; "handle a poison message?"; "at-least-once + idempotency = effectively-once — explain."
- **Related:** [Data Engineering / Kafka](13_data_engineering_big_data.md), [Microservices delivery semantics](5_microservices_distributed_systems.md).

### API design + idempotency — ★★★★☆ · Intermediate · 1 day
- **What exactly:** resource modeling, pagination (cursor > offset at scale), versioning, idempotency keys for safe retries (critical in payments), error contracts.
- **Related:** [API design](7_api_security_networking.md).

### Cost + failure modes + observability — ★★★★★ · Advanced · ongoing
- **Why:** newly explicit on the 2026 rubric.
- **What exactly:** estimate monthly cost + name the biggest driver; "cheapest architecture that meets 80% of the requirement"; failure injection (what if the cache/DB/queue dies?); graceful degradation; RED/USE metrics, SLOs, alerts.
- **Interview Qs:** "what's the cost driver and how would you cut it?"; "what happens when Redis goes down?" (fallback to DB + local limiter + shed load).

---

## Rising: AI / LLM infrastructure — ★★★☆☆ · Advanced · 1–2 days · [MIXED by company]

- **Why:** ~half of 2026 design loops include an ML-adjacent prompt at many companies (medium confidence). The bar is *systems*, not ML theory.
- **What exactly:** integrate an LLM like any component — LLM gateway (auth, rate limit, routing), **RAG** (embeddings → vector DB like pgvector/Pinecone/Weaviate → retrieval → prompt), token cost + latency budgets in the hot path, **fallback when the model is down/slow**, caching LLM responses, model versioning.
- **Interview Qs:** "design a real-time recommendation/RAG service"; "the model takes 400ms not 50ms — what do you do?"; "how do you cap token cost?"
- **When to skip:** confirm relevance with the recruiter; not every company asks.

---

## Low-Level Design (LLD) — ★★★★★ · Intermediate → Advanced · 1 week

- **Why:** a **distinct, heavily-weighted round** at product/fintech companies; often a 60–90 min machine-coding exercise.
- **Approach:** clarify requirements → identify entities → class diagram → apply SOLID + 1–2 patterns → handle **concurrency/thread-safety** → make it **extensible** → (machine coding) working, tested code.
- **Design patterns (GoF core) — ★★★★☆:** Strategy, Factory/Abstract Factory, Singleton (thread-safe), Observer, Builder, Decorator, Adapter, State. Know *when* each applies, not just definitions.
- **Practice problems (reported 2025):** logger framework (Razorpay), parking lot, train ticket booking (Swiggy), coupon system (Swiggy), inventory management (Swiggy), customer-issue/agent assignment (PhonePe), rate limiter, elevator, snake-and-ladder, splitwise, in-memory KV store, notification service.
- **Interview Qs:** "make this thread-safe"; "add a new log destination without changing existing code" (open/closed + Strategy); "where's the concurrency bottleneck?"
- **Red flags:** God class; no interfaces/abstraction; ignoring thread-safety; patterns for their own sake.
- **Related:** [Core Java OOP](2_core_java.md), [DSA](1_dsa.md).

---

## Hands-on labs & failure scenarios

- **Lab 1 (HLD):** design a URL shortener end-to-end incl. capacity math + monthly cost + failure modes. Repeat for: rate limiter, news feed, notification system, chat, distributed cache, payment system.
- **Lab 2 (LLD):** implement parking lot + logger + coupon system in Java with patterns + thread-safety + tests.
- **Lab 3 (AI infra):** sketch a RAG service with fallback + token budget.
- **Failure scenario:** in your design, Redis (cache + rate limiter) fails at peak — design the degradation path.
- **Cost drill:** for any design, state the biggest cost driver and a cheaper 80%-solution.

---

## Checklists

### Interview Checklist
- **Must know:** the 7-step framework; back-of-envelope; caching (stampede/hot key/consistent hashing); LB + horizontal scaling; replication + sharding; CAP/PACELC/consistency; rate limiter; queues/Kafka; idempotency; **cost + failure modes**; LLD with patterns + thread-safety.
- **Good to know:** CDN, search/indexing, gRPC vs REST, geo-distribution.
- **Bonus:** AI/LLM infra, vector DBs, consensus at a conceptual level.

### Production Checklist
- **Must know:** statelessness; graceful degradation; SLOs + alerts; idempotent writes; capacity headroom.
- **Good to know:** cost monitoring; multi-AZ; chaos/failure testing.

### Hands-on Checklist
- **Must:** 8–10 HLD designs practiced out loud; 5+ LLD problems coded.
- **Good:** each design has capacity + cost + failure analysis.
- **Bonus:** one AI-infra design.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference (HLD + LLD). Priorities/depth are in the guide above; **(2026)** = rising in interviews.

**1. Fundamentals**
- HLD vs LLD scope
- Quality attributes: scalability, availability, reliability, maintainability, performance
- Principles: separation of concerns, modularity, abstraction, encapsulation, reusability
- Back-of-the-envelope estimation (QPS, storage, bandwidth, memory)

**2. High-Level Design (HLD)**
- Requirements: functional, non-functional, constraints & assumptions
- Architectural styles: monolith, layered, microservices, event-driven, serverless, SOA **(Legacy term)**
- Components: API gateway, load balancer, SQL/NoSQL DBs, caches, message queues, object storage (S3/GCS)
- Data management: normalization/denormalization, sharding, replication, partitioning, indexing, ACID vs BASE
- Scalability & performance: horizontal vs vertical, CAP, latency vs throughput, rate limiting/throttling
- Caching: client, CDN, reverse proxy, application, DB caching (Redis/Memcached); eviction & invalidation; cache-aside/write-through/write-back
- Reliability & fault tolerance: failover, replication, circuit breaker, retries, DR (RPO/RTO)
- Security: authN/authZ, encryption at rest/in transit, API security, DDoS protection
- Observability: logs, metrics, traces, alerting → see [Observability](8_observability_monitoring_logging.md)

**3. Low-Level Design (LLD)**
- OOD principles: SOLID, DRY, KISS, YAGNI
- UML: class, sequence, activity, state diagrams
- Design patterns:
  - Creational: Singleton, Factory, Abstract Factory, Builder, Prototype
  - Structural: Adapter, Composite, Proxy, Decorator, Facade
  - Behavioral: Strategy, Observer, Command, Chain of Responsibility, Template Method
- API design in LLD: resource modeling, status codes, versioning, pagination, idempotency → see [API & Security](7_api_security_networking.md)
- DB modeling: ER diagrams, relationships (1:1/1:N/M:N), schema examples, indexes/FKs
- Concurrency in LLD: thread safety, locks, optimistic vs pessimistic
- Error handling & logging: exception design, structured logging, correlation IDs

**4. Core building blocks (deep-dive)**
- Load balancing (L4 vs L7, algorithms); consistent hashing
- Message queues & streaming (Kafka vs RabbitMQ); pub/sub
- Consistency models (strong, eventual, causal); quorum reads/writes
- Data partitioning strategies; hot-key handling
- Idempotency, dedup, exactly-once vs at-least-once

**5. Modern & rising topics (2026)**
- AI/LLM infrastructure: inference serving, token cost reasoning, vector DBs / RAG (awareness)
- Cost reasoning & capacity planning as a first-class design axis
- Multi-region / geo-distribution; edge

**6. Practice & case studies**
- URL shortener (TinyURL); ride-hailing (Uber/Lyft); Instagram/WhatsApp; e-commerce; distributed file storage (Drive/Dropbox); payment gateway; rate limiter; news feed; notification system; typeahead/search

**7. Interview delivery**
- 7-step framework: requirements → estimation → API → data model → high-level → deep-dive → bottlenecks/trade-offs
- Explicit trade-offs; state assumptions; drive the conversation

---

**Nav:** [◀ Spring](3_spring_and_spring_boot.md) · [Next ▶ Microservices](5_microservices_distributed_systems.md)
