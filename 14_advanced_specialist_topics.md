# 14 — Advanced / Specialist Topics

> **Module rating:** ★★☆☆☆ (Differentiator / Situational) · **Difficulty:** Specialized · **Est. effort:** learn on demand · **Depth target:** Awareness → Interview (only if targeting the domain)
> **Prerequisites:** [Microservices](5_microservices_distributed_systems.md), [System Design](4_system_design.md), [Databases](6_databases_relational_nosql.md).
> **Nav:** [◀ Data Engineering](13_data_engineering_big_data.md) · [Next ▶ Soft Skills](15_soft_skills_interview_prep.md) · **Related:** [Microservices](5_microservices_distributed_systems.md)

---

## Why this module (and why it's low priority)

These topics are **strong-candidate differentiators**, not gates. They rarely decide an offer at 3.5 YOE and can consume disproportionate time. **Rule:** learn the *concept + when to use it* (so you can discuss trade-offs), and only go deep if the target role explicitly needs it. Don't let these crowd out the ★★★★★ core.

---

## Topics (concept + when-to-use, then stop)

### Event sourcing — ★★☆☆☆ · Specialized
- **Concept:** persist state as an append-only log of events; rebuild state by replay.
- **When to use:** strong audit requirements, temporal queries, rebuildable read models.
- **Cost:** complexity, eventual consistency, schema/versioning of events, replay time.
- **Interview line:** "I'd use event sourcing only where auditability/rebuild justifies the operational complexity."

### CQRS — ★★☆☆☆ · Specialized
- **Concept:** separate write model from read model(s), often with async projection.
- **When to use:** read/write scale very differently; complex read shapes.
- **Cost:** eventual consistency between write and read sides; more moving parts.
- **Pairs with:** event sourcing (but doesn't require it).

### Consensus (Raft / Paxos) — ★★☆☆☆ · Specialized
- **Concept:** agreement despite failures; leader election + quorum.
- **When you need it:** building coordination/replicated state (usually you *use* etcd/ZooKeeper/Kafka rather than implement it).
- **Interview line:** know *why* (agreement, leader election, quorum) — not the proofs.
- See [Microservices consensus](5_microservices_distributed_systems.md).

### Service mesh (Istio / Linkerd) — ★★☆☆☆ · Specialized
- **Concept:** sidecar proxy gives mTLS, traffic control, telemetry without app code.
- **Cost:** ~50MB + ~1–2ms/request per pod; operational complexity.
- **When to use:** many services needing uniform mTLS/traffic policy; platform-owned.

### Exactly-once / transactional messaging — ★★☆☆☆ · Specialized
- **Reality:** true exactly-once is hard/limited; aim for **effectively-once** via idempotency + dedup. See [Delivery semantics](5_microservices_distributed_systems.md).

### Vector databases / RAG internals — ★★★☆☆ (rising) · Specialized
- **Concept:** embeddings + ANN search (pgvector/Pinecone/Weaviate) powering retrieval for LLMs.
- **When to use:** semantic search, RAG. Ties to [AI infra in system design](4_system_design.md). Medium confidence / [MIXED by company].

---

## Further reading (only if going deep)
- "Designing Data-Intensive Applications" (Kleppmann) — ch. 9 (consistency/consensus), ch. 11 (streams).
- Microsoft/AWS architecture pattern docs for CQRS/event sourcing.
- Istio docs (concepts only).

---

## Checklist (awareness-level)

- **Must know (to discuss):** what each pattern solves + its main cost + when *not* to use it.
- **Good to know:** how event sourcing + CQRS combine; consensus primitives.
- **Bonus (only if targeting the domain):** implement a small event-sourced aggregate; prototype a RAG retrieval layer.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. These are **differentiators** — aim for conceptual understanding and *when-to-use*, not deep implementation, unless a role requires it. Priorities/depth are in the guide above.

**1. Advanced Java / backend**
- Reactive programming (Project Reactor, WebFlux; RxJava **(Legacy)**); when reactive is/ isn't worth it (esp. vs virtual threads)
- Functional programming patterns; asynchronous processing (`CompletableFuture`, structured concurrency)

**2. Event-driven architectures**
- Event sourcing (benefits, pitfalls, replay); CQRS (read/write split); Kafka Streams
- Outbox pattern; idempotent consumers → see [Microservices](5_microservices_distributed_systems.md)

**3. Domain-Driven Design (DDD)**
- Strategic: bounded contexts, context mapping, ubiquitous language
- Tactical: aggregates, entities, value objects, repositories, domain events

**4. Distributed systems deep cuts (awareness)**
- Consensus (Raft/Paxos); exactly-once semantics; service mesh internals; CRDTs

**5. AI/LLM for backend engineers (2026, rising)**
- Vector databases & embeddings; RAG architecture; inference serving & cost/token reasoning
- LLM gateway/proxy patterns; prompt/response caching (awareness)

**6. Advanced security**
- Zero Trust; OAuth2 internals & flows; token security beyond basics

**7. Interview**
- Event sourcing vs CRUD; when CQRS pays off; reactive vs virtual threads; applying DDD in microservices

---

**Nav:** [◀ Data Engineering](13_data_engineering_big_data.md) · [Next ▶ Soft Skills & Interview Prep](15_soft_skills_interview_prep.md)
