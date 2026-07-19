# 5 — Microservices & Distributed Systems

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Advanced · **Est. effort:** 1–2 weeks · **Depth target:** Interview + Production
> **Prerequisites:** [System Design](4_system_design.md), [Databases](6_databases_relational_nosql.md), [Spring](3_spring_and_spring_boot.md).
> **Nav:** [◀ System Design](4_system_design.md) · [Next ▶ Databases](6_databases_relational_nosql.md) · **Related:** [Observability](8_observability_monitoring_logging.md), [Performance/Resilience](10_performance_profiling_reliability.md), [DevOps](11_devops_cicd_cloud.md)

---

## Why this module

At 3.5 YOE you're expected to reason about **services that fail independently**. Interviews probe resilience (what happens when a dependency is slow/down?), data consistency across services (SAGA), delivery guarantees, and the judgment to know **when a monolith is the right answer**. Fintech companies weigh idempotency and correctness heavily.

> **Reality check:** "microservices" is not automatically correct. A well-structured **modular monolith** is often the better call for a small team. Saying so is a senior signal.

---

## Core (Interview + Production)

### Decomposition & service boundaries — ★★★★☆ · Advanced · 1 day
- **What exactly:** bounded contexts (DDD-lite), single-responsibility services, database-per-service, avoiding the distributed monolith (chatty sync coupling), API contracts + versioning.
- **Interview Qs:** "how do you decide service boundaries?"; "when is a monolith better?"
- **Red flags:** sharing one DB across services; splitting by technical layer instead of business capability.

### Inter-service communication — ★★★★☆ · Advanced · 1 day
- **What exactly:** sync (REST/gRPC) vs async (Kafka/queues); gRPC for low-latency internal calls (contracts, streaming); async for decoupling + buffering; the coupling/latency trade-offs.
- **Interview Qs:** "REST vs gRPC vs async messaging — when each?"; "how do you stop a slow dependency cascading?"
- **Related:** [gRPC](7_api_security_networking.md), [Kafka in design](4_system_design.md).

### Resilience patterns — ★★★★☆ · Advanced · 2 days
- **Why:** the most-probed area; distributed systems fail partially, constantly.
- **What exactly:** timeouts (always!), retries with **exponential backoff + jitter**, **circuit breaker**, **bulkhead**, rate limiting, fallback/graceful degradation, load shedding — via **Resilience4j**.
- **Interview Qs:** "how do retries make an outage *worse*?" (retry storms → backoff + jitter + circuit breaker); "what does a bulkhead isolate?"; "timeout budget across a call chain?"
- **Red flags:** retries without backoff/jitter; no timeouts; unbounded retries amplifying load.
- **Related:** [Reliability](10_performance_profiling_reliability.md).

### Idempotency & delivery semantics — ★★★★☆ · Advanced · 1 day
- **Why:** central to correctness with at-least-once messaging and retried requests; fintech-critical.
- **What exactly:** at-most-once / at-least-once / exactly-once (why true exactly-once is hard → **effectively-once via idempotent consumers + dedup keys**), idempotency keys, outbox pattern (atomic DB write + event), dedup stores.
- **Interview Qs:** "how do you make a payment endpoint safe to retry?"; "at-least-once + idempotency = ?"; "how does the outbox pattern avoid dual-write problems?"

### SAGA / distributed transactions — ★★★★☆ · Advanced · 1 day
- **What exactly:** why 2PC is avoided at scale; SAGA (orchestration vs choreography), compensating transactions, eventual consistency across services.
- **Interview Qs:** "order → payment → inventory across 3 services — how do you keep consistency?" (SAGA + compensations); "orchestration vs choreography trade-offs?"
- **Red flags:** assuming a distributed transaction can be ACID like a single DB.

### Backpressure & flow control — ★★★☆☆ · Advanced · 0.5 day
- **What exactly:** bounded queues, consumer lag monitoring, shedding, pull vs push.
- **Related:** [Performance](10_performance_profiling_reliability.md).

---

## Situational / conceptual only

### Consensus (Raft / Paxos) — ★★☆☆☆ · Specialized · 0.5 day
> **Why low priority:** rarely asked beyond the concept for app engineers.
> **Learn only these basics:** what consensus solves (agreement despite failures), leader election, quorum, where it's used (etcd/ZooKeeper/Kafka controller). Know *why*, not the proofs.
> **Further reading:** Raft paper (visual), "Designing Data-Intensive Applications" ch. 9.

### Service mesh (Istio/Linkerd) — ★★☆☆☆ · Specialized · 0.5 day
> **Why low priority:** platform-owned; sidecar cost/benefit awareness suffices.
> **Learn only:** sidecar (Envoy) gives mTLS + traffic control + telemetry without app code; cost ≈ ~50MB + ~1–2ms/request per pod. Know the trade-off.

### Event sourcing / CQRS — ★★☆☆☆ · Specialized
> See [Advanced topics](14_advanced_specialist_topics.md). Learn only if the role demands audit/rebuildable state or read/write scaling separation.

---

## Hands-on labs & failure scenarios

- **Lab 1:** add Resilience4j circuit breaker + retry(backoff+jitter) + timeout to a Spring Boot client; simulate a slow dependency and observe the breaker open.
- **Lab 2:** implement an idempotent Kafka consumer with a dedup key; replay the same message and prove no double-processing.
- **Lab 3:** implement the outbox pattern (DB write + event) and a relay.
- **Failure scenario:** a downstream service degrades to 5s latency; without timeouts your thread pool exhausts and the whole service falls over — design + implement the fix.
- **Design task:** sketch a SAGA for an e-commerce order with compensations.

---

## Checklists

### Interview Checklist
- **Must know:** service boundaries + when-monolith; REST/gRPC/async trade-offs; timeouts/retries/backoff+jitter/circuit breaker/bulkhead; idempotency + delivery semantics; SAGA + compensations; outbox.
- **Good to know:** backpressure; consumer-lag monitoring; API versioning across services.
- **Bonus:** consensus concept; service mesh trade-offs; event sourcing/CQRS.

### Production Checklist
- **Must know:** every remote call has a timeout; retries are bounded + jittered; consumers are idempotent; per-service DB ownership.
- **Good to know:** DLQs; circuit-breaker dashboards; graceful degradation paths.

### Hands-on Checklist
- **Must:** wired Resilience4j; built an idempotent consumer.
- **Good:** implemented outbox; simulated + survived a dependency failure.
- **Bonus:** prototyped a SAGA orchestrator.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above; **(situational)** = go deep only if the role/interview demands it.

**1. Fundamentals**
- Microservices vs monolith; when NOT to use microservices (start-with-monolith)
- Characteristics: independent deployability, scalability, autonomy
- Benefits (modularity, independent scaling, fault isolation) vs challenges (distributed complexity, data consistency, operational overhead)

**2. Service design**
- Service boundaries; Domain-Driven Design (entities, value objects, aggregates, bounded contexts)
- Granularity (fine vs coarse); API-first design; avoiding the distributed monolith

**3. Communication**
- Synchronous: REST, gRPC (when to prefer each)
- Asynchronous: Kafka, RabbitMQ, ActiveMQ; event-driven
- Patterns: request-response, publish-subscribe, event sourcing (situational), CQRS (situational)

**4. Distributed systems fundamentals**
- Concurrency, no global clock, independent/partial failures
- CAP; PACELC; consistency models (strong, eventual, causal)
- Consensus: Raft / Paxos / ZAB **(situational — conceptual understanding)**
- Time, ordering, logical clocks (awareness)

**5. Scalability & reliability**
- Horizontal vs vertical scaling; load balancing (round-robin, least-connections, hashing)
- Fault tolerance: retries + backoff + jitter, circuit breakers, timeouts, bulkheads, failover
- Redundancy: replication, leader election, quorum reads/writes

**6. Resilience & correctness patterns**
- Idempotency & idempotency keys; deduplication
- Delivery semantics: at-least-once, at-most-once, effectively-once
- Backpressure; graceful degradation; load shedding

**7. Infrastructure**
- Service discovery (Eureka, Consul, etcd); API gateway (Spring Cloud Gateway, Kong, Nginx)
- Sidecar / service mesh (Istio, Linkerd) **(situational — awareness)**
- Centralized config (Spring Cloud Config, Consul)

**8. Security**
- OAuth2, OpenID Connect, JWT; RBAC / ABAC; mTLS between services; gateway rate-limiting; secret management (Vault, KMS) → see [API & Security](7_api_security_networking.md)

**9. Data management**
- Database-per-service; distributed transactions
- Saga (choreography vs orchestration); Outbox pattern; two-phase commit vs eventual consistency; CDC (awareness)

**10. Observability**
- Centralized logging (ELK/EFK); distributed tracing (OpenTelemetry, Jaeger, Zipkin); metrics (Prometheus/Grafana); health checks (liveness/readiness) → see [Observability](8_observability_monitoring_logging.md)

**11. Practice & interview**
- Design order/checkout with saga; event-driven order management; auth service
- Explain monolith↔microservices trade-offs; failure handling; data consistency across services

---

**Nav:** [◀ System Design](4_system_design.md) · [Next ▶ Databases](6_databases_relational_nosql.md)
