# 0 — Overview & Master Priority Table

> Navigation index and single source of truth for **ratings** across the repository. Ratings reflect importance for a **~3.5 YOE Java/Spring backend engineer** in 2026, derived from current hiring trends.
>
> New here? Read [`README.md`](README.md) first for the legends and learning philosophy.

**Legend:** ★★★★★ Mandatory · ★★★★☆ High ROI · ★★★☆☆ Situational · ★★☆☆☆ Differentiator · ★☆☆☆☆ Low ROI (basics only). Difficulty: `Foundation` / `Intermediate` / `Advanced` / `Specialized`.

> This table summarizes the **guide** (priorities). The **exhaustive topic checklist** for each area lives at the bottom of its module under `## Detailed Syllabus (topic checklist)` — the full sub-topic inventory to verify you've covered everything.

---

## How the priorities changed vs the old 2-YOE list

- **Up:** Virtual Threads, `RestClient`/HTTP Interfaces, cost reasoning in design, OpenTelemetry, Kubernetes debugging, Testcontainers, idempotency, LLD practice, Kafka (now core).
- **Down / Legacy:** `RestTemplate` (deprecated), Spring XML, JUnit 4, WebFlux-as-default, HATEOAS, competitive-only DSA (FFT/suffix trees/Mo's/max-flow), Paxos/Raft deep dive, service-mesh internals, event sourcing/CQRS deep dive, Spark/big-data.

---

## Master priority table

### [1 — DSA](1_dsa.md) · module ★★★★★
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Arrays, Strings, Hashing | ★★★★★ | Foundation | bedrock of coding rounds |
| Two pointers / Sliding window | ★★★★★ | Foundation | highest-frequency patterns |
| Binary search (+ answer-space) | ★★★★★ | Intermediate | disproportionately common (India) |
| Trees / BST / traversals | ★★★★★ | Intermediate | interview staple |
| Graphs (BFS/DFS/topo/Dijkstra/Union-Find) | ★★★★★ | Intermediate→Advanced | modeling + pathfinding |
| Heaps / Top-K | ★★★★☆ | Intermediate | streaming/ranking |
| Dynamic Programming (core) | ★★★★☆ | Advanced | medium/hard rounds |
| Stacks/Queues/Monotonic | ★★★★☆ | Foundation | parsing, windows |
| Tries | ★★★☆☆ | Intermediate | prefix/autocomplete |
| Greedy, Intervals | ★★★★☆ | Intermediate | scheduling |
| Bit manipulation | ★★★☆☆ | Intermediate | basics + bitmask DP |
| Segment/Fenwick tree | ★★☆☆☆ | Advanced | occasional |
| FFT, suffix trees, Mo's, max-flow | ★☆☆☆☆ | Specialized | competitive-only — stub |

### [2 — Core Java](2_core_java.md) · module ★★★★★
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| OOP + SOLID | ★★★★★ | Foundation | LLD backbone |
| Collections framework | ★★★★★ | Foundation | daily + internals asked |
| Streams / Lambdas / Optional | ★★★★★ | Foundation | modern idiom |
| Concurrency (memory model, locks, executors, `CompletableFuture`) | ★★★★★ | Advanced | correctness under load |
| Virtual Threads (Java 21) + pinning | ★★★★☆ | Intermediate | production concurrency |
| Records, Sealed, Pattern matching | ★★★★☆ | Foundation→Intermediate | modern Java |
| Generics, Exceptions | ★★★★☆ | Foundation | type safety, robustness |
| Memory model + GC (G1/ZGC) | ★★★☆☆ | Advanced | debugging/tuning |
| Structured Concurrency / Scoped Values (preview) | ★★☆☆☆ | Advanced | awareness |
| Applets, classloader trivia, finalizers | ★☆☆☆☆ | — | Legacy — stub |

### [3 — Spring & Spring Boot](3_spring_and_spring_boot.md) · module ★★★★★
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| DI / bean lifecycle | ★★★★★ | Foundation | core |
| REST controllers + validation + error handling | ★★★★★ | Intermediate | daily |
| Spring Data JPA / Hibernate (lazy/eager, N+1) | ★★★★★ | Intermediate→Advanced | data layer |
| Spring Security 6 + JWT/OAuth2 | ★★★★☆ | Advanced | auth |
| `RestClient` / HTTP Interfaces | ★★★★☆ | Intermediate | modern HTTP client |
| Actuator + Micrometer + OTel | ★★★★☆ | Intermediate | observability |
| Virtual-thread enablement | ★★★★☆ | Intermediate | one property + tuning |
| Profiles/config, Testcontainers | ★★★★☆ | Intermediate | env + testing |
| GraalVM native image | ★★☆☆☆ | Advanced | situational |
| `RestTemplate`, XML config, WebFlux-as-default | ★☆☆☆☆ | — | Legacy/situational — stub |

### [4 — System Design (HLD + LLD)](4_system_design.md) · module ★★★★★
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Requirements + back-of-envelope | ★★★★★ | Intermediate | every interview |
| Caching (strategies, stampede, hot keys) | ★★★★★ | Intermediate | top optimization |
| Load balancing + horizontal scaling | ★★★★★ | Intermediate | universal |
| Replication + sharding | ★★★★★ | Advanced | scale |
| Consistency / CAP / PACELC | ★★★★★ | Advanced | central trade-off |
| Rate limiting | ★★★★☆ | Intermediate | infra staple |
| Message queues / Kafka in design | ★★★★★ | Advanced | decoupling |
| API design + idempotency | ★★★★☆ | Intermediate | correctness |
| **Cost + failure modes + observability** | ★★★★★ | Advanced | now explicitly graded |
| LLD (OOP, patterns, concurrency, machine coding) | ★★★★★ | Intermediate→Advanced | distinct round |
| AI/LLM infra (gateway, RAG, vector DB, fallback) | ★★★☆☆ | Advanced | rising [MIXED] |
| Design patterns (GoF core) | ★★★★☆ | Intermediate | LLD |

### [5 — Microservices & Distributed Systems](5_microservices_distributed_systems.md) · module ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Decomposition + boundaries | ★★★★☆ | Advanced | design |
| Comms: REST/gRPC/async | ★★★★☆ | Advanced | trade-offs |
| Resilience (circuit breaker/retry/backoff/bulkhead) | ★★★★☆ | Advanced | Resilience4j |
| Idempotency + delivery semantics | ★★★★☆ | Advanced | fintech |
| SAGA / distributed transactions | ★★★★☆ | Advanced | consistency |
| Backpressure / flow control | ★★★☆☆ | Advanced | stability |
| Consensus (Raft/Paxos) | ★★☆☆☆ | Specialized | conceptual only |
| Service mesh internals | ★★☆☆☆ | Specialized | situational |

### [6 — Databases](6_databases_relational_nosql.md) · module ★★★★★
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Transactions/ACID/isolation/locks | ★★★★★ | Advanced | correctness |
| Indexing + `EXPLAIN` + tuning | ★★★★★ | Intermediate→Advanced | top real skill |
| SQL (joins, windows, CTEs) | ★★★★★ | Intermediate | daily + interview |
| Schema design + normalization | ★★★★☆ | Intermediate | design |
| Sharding + replication | ★★★★☆ | Advanced | scale |
| NoSQL selection (Redis/Mongo/Cassandra/Dynamo) | ★★★★☆ | Intermediate | when-to-use |
| Migrations (Flyway/Liquibase) | ★★★☆☆ | Intermediate | hygiene |
| Time-series DB | ★★☆☆☆ | Intermediate | situational |

### [7 — API, Security & Networking](7_api_security_networking.md) · ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| REST design + versioning + pagination | ★★★★★ | Intermediate | daily |
| OAuth2 / OIDC / JWT (+ pitfalls) | ★★★★★ | Advanced | auth flows |
| TLS + encryption at rest/in transit | ★★★★☆ | Intermediate | security baseline |
| OWASP Top 10 + input validation | ★★★★★ | Intermediate | hygiene |
| gRPC / GraphQL | ★★★☆☆ | Intermediate | situational |
| HTTP/DNS/TCP fundamentals | ★★★★☆ | Foundation | debugging |
| Sockets / low-level networking | ★★☆☆☆ | Advanced | basics only |
| HATEOAS | ★☆☆☆☆ | — | stub |

### [8 — Observability](8_observability_monitoring_logging.md) · ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Structured logging + correlation IDs | ★★★★★ | Intermediate | baseline |
| Metrics (Prometheus/Micrometer) | ★★★★☆ | Intermediate | health |
| Tracing + OpenTelemetry | ★★★★☆ | Intermediate | distributed debugging |
| SLI/SLO/error budgets, RED/USE | ★★★★☆ | Intermediate | reliability literacy |
| ELK/EFK | ★★★☆☆ | Intermediate | consolidating |

### [9 — Testing & Quality](9_testing_quality.md) · ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| JUnit 5 + Mockito | ★★★★★ | Foundation | baseline |
| Integration tests + Testcontainers | ★★★★☆ | Intermediate | modern standard |
| Contract testing | ★★★☆☆ | Intermediate | microservices |
| Load testing (k6) | ★★★☆☆ | Intermediate | validate scale |
| TDD | ★★☆☆☆ | Intermediate | approach |
| JUnit 4 | ★☆☆☆☆ | — | Legacy — stub |

### [10 — Performance & Reliability](10_performance_profiling_reliability.md) · ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Caching for latency | ★★★★★ | Intermediate | user-facing |
| Tail latency (p99) | ★★★★☆ | Advanced | real UX |
| Profiling (JFR/async-profiler, flame graphs) | ★★★★☆ | Advanced | diagnose |
| Resilience patterns | ★★★★☆ | Advanced | stability |
| Capacity/autoscaling | ★★★☆☆ | Advanced | cost/load |
| Microbenchmarks (JMH) | ★★★☆☆ | Advanced | hotspots |

### [11 — DevOps, CI/CD & Cloud](11_devops_cicd_cloud.md) · ★★★★☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Docker (multi-stage, image hygiene) | ★★★★☆ | Intermediate | packaging |
| K8s essentials (probes, resources, debug) | ★★★★☆ | Intermediate→Advanced | run + debug |
| CI/CD (GitHub Actions) | ★★★★☆ | Intermediate | daily |
| Cloud fundamentals (AWS) | ★★★★☆ | Intermediate | substrate |
| Terraform basics | ★★★☆☆ | Intermediate | read/modify |
| Helm | ★★★☆☆ | Intermediate | deploy |
| GitOps/ArgoCD, serverless | ★★☆☆☆ | Advanced | situational |

### [12 — Build & Tooling](12_build_tooling.md) · ★★★☆☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Maven / Gradle | ★★★★☆ | Foundation | builds |
| Git (branching, rebase, PRs) | ★★★★★ | Foundation | collaboration |
| IDE/debugging | ★★★☆☆ | Foundation | productivity |

### [13 — Data Engineering](13_data_engineering_big_data.md) · ★★★☆☆
| Topic | Rating | Difficulty | Note |
|-------|--------|-----------|------|
| Kafka (backend event backbone) | ★★★★★ | Advanced | core |
| Spark / batch | ★★☆☆☆ | Advanced | role-dependent |
| ETL/ELT, lake vs warehouse | ★★☆☆☆ | Intermediate | awareness |

### [14 — Advanced/Specialist](14_advanced_specialist_topics.md) · ★★☆☆☆
Event sourcing, CQRS, consensus deep dive, service mesh internals, exactly-once — all **Specialized / situational**. Learn only if the target role demands it.

### [15 — Soft Skills & Interview Prep](15_soft_skills_interview_prep.md) · ★★★★★
STAR, trade-off communication, resume storytelling, mock interviews, negotiation — ★★★★★, decisive.

### [16 — Misc / Nice-to-have](16_misc_nice_to_have.md) · ★★★☆☆
CDN/edge, secrets/KMS, data modeling patterns — cross-linked, condensed.

---

Next → [`1_dsa.md`](1_dsa.md) · Plan → [`18_learning_timeline.md`](18_learning_timeline.md)
