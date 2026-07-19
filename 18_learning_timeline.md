# 18 — Learning Timeline (Execution Plan)

> The day-by-day plan that turns this repo into an offer. **Primary track: ~16 weeks (110 days)**, assuming **2–3 h weekdays / 5–6 h weekends**. Accelerated **30 / 45 / 60-day** tracks below.
> **Nav:** [◀ Final Notes](17_final_notes_actionable.md) · [Overview](0_overview.md) · [README](README.md)

---

## How to read this plan

Each day lists: **Objective · Topics (linked) · Est. hours · Exercises · Checkpoint**. Weekends are **build + revise + mock**. Reading = the linked module (open it and go to the day's topic); Revision = re-derive prior material from memory.

**Legend:** :books: study · :hammer: hands-on/lab · :arrows_counterclockwise: revision · :dart: mock/interview · :checkered_flag: milestone.

**Cadence rules:** at most one cognitively heavy topic/day; every week has revision + practice + interview Qs + hands-on; DSA is a *daily* background habit (2–3 problems) alongside the module of the week.

---

## Phase overview

| Phase | Weeks | Focus | Milestone |
|-------|-------|-------|-----------|
| 1. Foundations | 1–3 | DSA patterns + Java 21 core | Anchor project scaffold |
| 2. Framework & Data | 4–6 | Spring Boot 3.x + Databases + Testing | CRUD service + tests live |
| 3. Design | 7–9 | System design (HLD) + LLD + Microservices | 5 HLD + 5 LLD done |
| 4. Production | 10–12 | API/Security + Observability + Perf + DevOps | Project deployed + observable |
| 5. Depth & Consolidation | 13–14 | Kafka + advanced + revision week | Full anchor project complete |
| 6. Interview Sprint | 15–16 | Mocks + weak-area patching + final revision | Interview-ready |

---

## Phase 1 — Foundations (Weeks 1–3)

### Week 1 — DSA core patterns + complexity
| Day | Objective | Topics | Hrs | Exercises / Checkpoint |
|-----|-----------|--------|-----|------------------------|
| 1 | Complexity fluency | [Complexity](1_dsa.md) | 2 | :books: State Big-O for 10 snippets. **Checkpoint:** explain amortized `ArrayList.add`. |
| 2 | Arrays + hashing | [Arrays/Strings/Hashing](1_dsa.md) | 3 | :hammer: 3 problems (two-sum, subarray sum=k, group anagrams). |
| 3 | Two pointers + sliding window | [Two pointers/window](1_dsa.md) | 2 | :hammer: 3 problems (min window, longest substring). |
| 4 | Binary search + answer-space | [Binary search](1_dsa.md) | 3 | :hammer: rotated-array min, Koko bananas. **Checkpoint:** prove predicate monotonicity. |
| 5 | Stacks/queues/monotonic | [Stacks/Queues](1_dsa.md) | 2 | :hammer: valid parens, daily temperatures. |
| 6 (wknd) | Build kickoff + revise | [Anchor project](17_final_notes_actionable.md#the-anchor-project-build-this) | 5 | :hammer: scaffold Spring Boot 3.x project (empty). :arrows_counterclockwise: week's patterns. |
| 7 (wknd) | Trees | [Trees & BST](1_dsa.md) | 5 | :hammer: traversals, LCA, validate BST, serialize. :dart: self-mock 1 medium timed. |

### Week 2 — DSA graphs/DP + Java fundamentals
| Day | Objective | Topics | Hrs | Exercises / Checkpoint |
|-----|-----------|--------|-----|------------------------|
| 8 | Graphs I | [Graphs](1_dsa.md) | 3 | :hammer: number of islands, clone graph. |
| 9 | Graphs II (topo/DSU/Dijkstra) | [Graphs](1_dsa.md) | 3 | :hammer: course schedule, accounts merge, network delay. |
| 10 | Heaps + intervals | [Heaps](1_dsa.md), [Intervals](1_dsa.md) | 2 | :hammer: top-K, merge intervals, meeting rooms II. |
| 11 | DP I | [DP core](1_dsa.md) | 3 | :hammer: coin change, house robber, LIS. **Checkpoint:** state+transition out loud. |
| 12 | DP II | [DP core](1_dsa.md) | 2 | :hammer: LCS, edit distance, word break. |
| 13 (wknd) | Java OOP + Collections | [OOP+SOLID](2_core_java.md), [Collections](2_core_java.md) | 5 | :books: HashMap internals. :hammer: model a domain with records. |
| 14 (wknd) | Streams + revise DSA | [Streams](2_core_java.md) | 5 | :hammer: rewrite loops as streams. :dart: mock: 2 mediums timed. :arrows_counterclockwise: graphs/DP. |

### Week 3 — Java concurrency + virtual threads
| Day | Objective | Topics | Hrs | Exercises / Checkpoint |
|-----|-----------|--------|-----|------------------------|
| 15 | JMM + synchronization | [Concurrency](2_core_java.md) | 3 | :books: volatile vs synchronized. **Checkpoint:** explain happens-before. |
| 16 | Executors + CompletableFuture | [Concurrency](2_core_java.md) | 3 | :hammer: build a bounded blocking queue. |
| 17 | Virtual threads + pinning | [Virtual Threads](2_core_java.md) | 2 | :hammer: enable VT in a toy app; trace pinning. |
| 18 | Modern Java + GC | [Modern features](2_core_java.md), [GC](2_core_java.md) | 2 | :books: records/sealed/patterns; read a GC log. |
| 19 | Generics/exceptions + DSA | [Generics/Exceptions](2_core_java.md) | 2 | :hammer: 2 DSA problems (tries/backtracking). |
| 20 (wknd) | :checkered_flag: **Milestone 1** | [Core Java](2_core_java.md) | 5 | :hammer: anchor project: OOP domain model + one LLD (logger). :dart: **Mock: 1 LLD**. |
| 21 (wknd) | Revision + resume v1 | [Resume](15_soft_skills_interview_prep.md) | 5 | :arrows_counterclockwise: Java+DSA. :hammer: write resume v1 + 3 STAR stories. |

> **Checkpoint 1 (end W3):** core DSA patterns fluent; can explain concurrency + virtual threads; project scaffolded with a domain model.

---

## Phase 2 — Framework & Data (Weeks 4–6)

### Week 4 — Spring Boot core
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 22 | DI + autoconfig | [DI/lifecycle](3_spring_and_spring_boot.md) | 2 | :hammer: convert project to constructor injection. |
| 23 | REST + validation + errors | [REST controllers](3_spring_and_spring_boot.md) | 3 | :hammer: build endpoints + `@ControllerAdvice`. |
| 24 | `RestClient` + HTTP Interfaces | [RestClient](3_spring_and_spring_boot.md) | 2 | :hammer: call an external API with RestClient + timeouts. |
| 25 | Config/profiles + Actuator | [Actuator](3_spring_and_spring_boot.md) | 2 | :hammer: profiles + health/readiness. |
| 26 | DSA revision | [DSA](1_dsa.md) | 2 | :hammer: 3 mixed-pattern problems timed. |
| 27 (wknd) | JPA I | [Spring Data JPA](3_spring_and_spring_boot.md) | 5 | :hammer: entities + repos vs Postgres (Testcontainers). |
| 28 (wknd) | JPA II (N+1) + mock | [Spring Data JPA](3_spring_and_spring_boot.md) | 5 | :hammer: reproduce + fix an N+1. :dart: mock: 2 mediums. |

### Week 5 — Databases
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 29 | Transactions + isolation | [Transactions](6_databases_relational_nosql.md) | 3 | :hammer: reproduce a deadlock; fix it. |
| 30 | Indexing + EXPLAIN | [Indexing](6_databases_relational_nosql.md) | 3 | :hammer: tune a slow query; measure. **Checkpoint:** read a plan. |
| 31 | SQL (joins/windows/CTEs) | [SQL fluency](6_databases_relational_nosql.md) | 2 | :hammer: top-N-per-group, running total. |
| 32 | NoSQL selection | [NoSQL selection](6_databases_relational_nosql.md) | 2 | :books: decision table; model in DynamoDB. |
| 33 | Schema + migrations + DSA | [Migrations](6_databases_relational_nosql.md) | 2 | :hammer: expand-contract migration (Flyway). |
| 34 (wknd) | Sharding/replication + build | [Sharding](6_databases_relational_nosql.md) | 5 | :hammer: add Flyway + indexes to project. :arrows_counterclockwise: SQL. |
| 35 (wknd) | :dart: Mock + revise | [Databases](6_databases_relational_nosql.md) | 5 | :dart: mock: 1 coding + 1 DB deep-dive. |

### Week 6 — Testing + Security
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 36 | JUnit 5 + Mockito | [Unit testing](9_testing_quality.md) | 3 | :hammer: unit-test a service (mock repo, verify). |
| 37 | Testcontainers | [Integration testing](9_testing_quality.md) | 3 | :hammer: integration test vs real Postgres. |
| 38 | Spring Security 6 + JWT | [Security 6](3_spring_and_spring_boot.md) | 3 | :hammer: stateless JWT + `@PreAuthorize`. |
| 39 | OAuth2/OIDC | [Auth](7_api_security_networking.md) | 2 | :books: auth-code+PKCE flow. |
| 40 | DSA revision | [DSA](1_dsa.md) | 2 | :hammer: 3 problems timed. |
| 41 (wknd) | :checkered_flag: **Milestone 2** | [Testing](9_testing_quality.md) | 6 | :hammer: project = secured CRUD + tests (JUnit5/Mockito/Testcontainers). :dart: mock: behavioral (4 STAR). |
| 42 (wknd) | :arrows_counterclockwise: **Revision + resume v2** | [Soft skills](15_soft_skills_interview_prep.md) | 5 | :arrows_counterclockwise: Spring+DB+Testing. Update resume with project. |

> **Checkpoint 2 (end W6):** a secured, tested CRUD service against real Postgres; can discuss transactions, indexing, N+1, JWT.

---

## Phase 3 — Design (Weeks 7–9)

### Week 7 — System design framework + building blocks
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 43 | The 7-step framework | [HLD framework](4_system_design.md) | 2 | :books: memorize; back-of-envelope drill. |
| 44 | Caching | [Caching](4_system_design.md) | 3 | :books: stampede/hot key/consistent hashing. |
| 45 | LB + scaling + replication/sharding | [LB](4_system_design.md), [Replication](4_system_design.md) | 3 | :hammer: design "scale reads then writes." |
| 46 | Consistency/CAP/PACELC | [Consistency](4_system_design.md) | 2 | :books: per-data-type consistency. |
| 47 | Rate limiting | [Rate limiting](4_system_design.md) | 2 | :hammer: design distributed rate limiter (Redis Lua). |
| 48 (wknd) | Design practice + build | [System Design](4_system_design.md) | 6 | :hammer: **Design URL shortener** end-to-end (+cost+failure). :dart: present it aloud. |
| 49 (wknd) | Design practice | [System Design](4_system_design.md) | 5 | :hammer: **Design rate limiter + distributed cache**. |

### Week 8 — LLD + patterns + Microservices
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 50 | LLD approach + patterns | [LLD](4_system_design.md) | 3 | :hammer: parking lot (classes + patterns + thread-safe). |
| 51 | LLD practice | [LLD](4_system_design.md) | 3 | :hammer: coupon system / inventory. |
| 52 | Resilience patterns | [Resilience](5_microservices_distributed_systems.md) | 3 | :hammer: Resilience4j circuit breaker + retry+jitter. |
| 53 | Idempotency + delivery | [Idempotency](5_microservices_distributed_systems.md) | 2 | :books: outbox pattern; idempotency keys. |
| 54 | SAGA + comms | [SAGA](5_microservices_distributed_systems.md) | 2 | :hammer: sketch an order SAGA. |
| 55 (wknd) | Design + LLD mocks | [System Design](4_system_design.md) | 6 | :dart: **Mock: 1 HLD + 1 LLD** (recorded). Review trade-off gaps. |
| 56 (wknd) | :arrows_counterclockwise: Revise design | [System Design](4_system_design.md) | 5 | :arrows_counterclockwise: building blocks; redo 1 design from memory. |

### Week 9 — Design consolidation
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 57 | Message queues in design | [Queues/Kafka](4_system_design.md) | 3 | :hammer: **Design notification system**. |
| 58 | API design + idempotency | [API design](4_system_design.md) | 2 | :hammer: design payment API with idempotency keys. |
| 59 | AI/LLM infra (rising) | [AI infra](4_system_design.md) | 2 | :books: RAG + fallback + token budget. |
| 60 | LLD practice | [LLD](4_system_design.md) | 2 | :hammer: rate limiter / snake-and-ladder. |
| 61 | DSA revision | [DSA](1_dsa.md) | 2 | :hammer: 3 problems timed. |
| 62 (wknd) | :checkered_flag: **Milestone 3** | [System Design](4_system_design.md) | 6 | :hammer: **Design chat + news feed**. Now 6+ HLD, 5+ LLD done. :dart: mock HLD. |
| 63 (wknd) | :arrows_counterclockwise: Revision week prep | [System Design](4_system_design.md) | 5 | :arrows_counterclockwise: consolidate all designs into a one-page cheatsheet. |

> **Checkpoint 3 (end W9):** can drive any classic design with cost+failure analysis; can code an LLD with patterns + thread-safety.

---

## Phase 4 — Production (Weeks 10–12)

### Week 10 — API/Security depth + Observability
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 64 | REST design + pagination | [REST design](7_api_security_networking.md) | 2 | :hammer: cursor pagination + idempotency on project. |
| 65 | OWASP + TLS | [OWASP](7_api_security_networking.md) | 2 | :hammer: run a dependency/security scan; fix findings. |
| 66 | HTTP/DNS/TCP + gRPC | [HTTP fundamentals](7_api_security_networking.md) | 2 | :books: HTTP/2 vs 3; gRPC basics. |
| 67 | Logging + metrics | [Logging](8_observability_monitoring_logging.md), [Metrics](8_observability_monitoring_logging.md) | 3 | :hammer: structured logs + correlation ID; RED metrics. |
| 68 | Tracing + OTel + SLOs | [Tracing](8_observability_monitoring_logging.md), [SLOs](8_observability_monitoring_logging.md) | 2 | :hammer: OTel traces to Jaeger; define an SLO. |
| 69 (wknd) | Observability build | [Observability](8_observability_monitoring_logging.md) | 6 | :hammer: add Micrometer+OTel+Grafana RED dashboard to project. |
| 70 (wknd) | :dart: Mock + revise | [System Design](4_system_design.md) | 5 | :dart: mock: 1 coding + 1 design. |

### Week 11 — Performance + Reliability
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 71 | Tail latency | [Tail latency](10_performance_profiling_reliability.md) | 2 | :books: fan-out amplification math. |
| 72 | JVM profiling | [Profiling](10_performance_profiling_reliability.md) | 3 | :hammer: flame graph a hot endpoint; fix it. |
| 73 | Leak/GC debugging | [GC](2_core_java.md) | 2 | :hammer: capture + analyze a heap dump. |
| 74 | Resilience + capacity | [Resilience](10_performance_profiling_reliability.md) | 2 | :hammer: simulate a retry storm; fix with backoff+breaker. |
| 75 | DSA revision | [DSA](1_dsa.md) | 2 | :hammer: 3 problems timed. |
| 76 (wknd) | Perf build + design | [Performance](10_performance_profiling_reliability.md) | 6 | :hammer: add cache; show p99 improvement. :dart: design mock. |
| 77 (wknd) | :arrows_counterclockwise: Revision | [Performance](10_performance_profiling_reliability.md) | 5 | :arrows_counterclockwise: production topics; update resume v3. |

### Week 12 — DevOps + Cloud
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 78 | Docker | [Docker](11_devops_cicd_cloud.md) | 2 | :hammer: multi-stage Dockerfile <200MB, non-root. |
| 79 | Kubernetes I | [K8s essentials](11_devops_cicd_cloud.md) | 3 | :hammer: deploy to kind with probes+limits+HPA. |
| 80 | Kubernetes II (debug) | [K8s essentials](11_devops_cicd_cloud.md) | 2 | :hammer: fix a `CrashLoopBackOff`/`OOMKilled`. |
| 81 | CI/CD | [CI/CD](11_devops_cicd_cloud.md) | 2 | :hammer: GitHub Actions: build→test→image. |
| 82 | Cloud + IAM | [Cloud fundamentals](11_devops_cicd_cloud.md) | 2 | :books: IAM least privilege; ECS vs EKS vs Lambda. |
| 83 (wknd) | :checkered_flag: **Milestone 4** | [DevOps](11_devops_cicd_cloud.md) | 6 | :hammer: project deployed to K8s + CI green + observable. :dart: mock: DevOps deep-dive. |
| 84 (wknd) | :arrows_counterclockwise: Revision | [DevOps](11_devops_cicd_cloud.md) | 5 | :arrows_counterclockwise: all production modules. |

> **Checkpoint 4 (end W12):** project is deployed, observable, and CI-gated; can debug K8s + read a flame graph.

---

## Phase 5 — Depth & Consolidation (Weeks 13–14)

### Week 13 — Kafka + advanced awareness
| Day | Objective | Topics | Hrs | Exercises |
|-----|-----------|--------|-----|-----------|
| 85 | Kafka model | [Kafka](13_data_engineering_big_data.md) | 3 | :hammer: keyed produce/consume; observe ordering. |
| 86 | Idempotent consumer + DLQ | [Kafka](13_data_engineering_big_data.md) | 3 | :hammer: idempotent consumer + DLQ; replay test. |
| 87 | CDC/outbox | [ETL](13_data_engineering_big_data.md) | 2 | :hammer: wire outbox → Kafka. |
| 88 | Advanced concepts | [Advanced](14_advanced_specialist_topics.md) | 2 | :books: event sourcing/CQRS/consensus — when-to-use only. |
| 89 | DSA revision | [DSA](1_dsa.md) | 2 | :hammer: 3 hard-ish problems. |
| 90 (wknd) | :checkered_flag: **Milestone 5 — anchor project complete** | [Anchor project](17_final_notes_actionable.md#the-anchor-project-build-this) | 6 | :hammer: integrate Kafka into project (full stack done). |
| 91 (wknd) | :arrows_counterclockwise: Consolidate | [Overview](0_overview.md) | 5 | :arrows_counterclockwise: build a personal cheatsheet across all modules. |

### Week 14 — REVISION WEEK (no new topics)
| Day | Objective | Focus | Hrs | Exercises |
|-----|-----------|-------|-----|-----------|
| 92 | DSA sprint | [DSA](1_dsa.md) | 3 | :dart: 4 timed mediums across patterns. |
| 93 | Java + Spring | [Java](2_core_java.md) / [Spring](3_spring_and_spring_boot.md) | 3 | :arrows_counterclockwise: flash the checklists; explain aloud. |
| 94 | Databases | [Databases](6_databases_relational_nosql.md) | 2 | :arrows_counterclockwise: isolation/indexing Q&A. |
| 95 | HLD | [System Design](4_system_design.md) | 3 | :dart: redo 2 designs from memory. |
| 96 | LLD | [LLD](4_system_design.md) | 2 | :dart: code 1 LLD cold. |
| 97 (wknd) | :dart: **Full mock loop** | [Soft skills](15_soft_skills_interview_prep.md) | 6 | :dart: coding + LLD + HLD + behavioral in one day. |
| 98 (wknd) | Gap analysis | weak areas | 5 | List weak areas from mocks → plan sprint. |

> **Checkpoint 5 (end W14):** full anchor project done; a mock loop passed end-to-end; weak areas identified.

---

## Phase 6 — Interview Sprint (Weeks 15–16)

### Week 15 — Mocks + weak-area patching
| Day | Objective | Focus | Hrs | Exercises |
|-----|-----------|-------|-----|-----------|
| 99 | Weak area #1 | your gap | 3 | :hammer: targeted practice + re-mock. |
| 100 | Weak area #2 | your gap | 3 | :hammer: targeted practice. |
| 101 | HLD mock | [System Design](4_system_design.md) | 2 | :dart: recorded design mock; review. |
| 102 | LLD mock | [LLD](4_system_design.md) | 2 | :dart: recorded machine-coding mock. |
| 103 | Behavioral | [Soft skills](15_soft_skills_interview_prep.md) | 2 | :dart: full behavioral mock; refine STAR. |
| 104 (wknd) | :dart: Company-specific prep | [company cheatsheet](15_soft_skills_interview_prep.md#company-format-cheatsheet-from-researchmd-10) | 6 | Tailor to target companies; confirm formats/AI policy with recruiters. |
| 105 (wknd) | :dart: Full mock loop #2 | all | 5 | :dart: another end-to-end loop. |

### Week 16 — Final revision sprint
| Day | Objective | Focus | Hrs | Exercises |
|-----|-----------|-------|-----|-----------|
| 106 | DSA warm-keeping | [DSA](1_dsa.md) | 2 | :hammer: 2–3 mediums/day (keep warm, don't burn out). |
| 107 | Design cheatsheet | [System Design](4_system_design.md) | 2 | :arrows_counterclockwise: 1-page framework + numbers. |
| 108 | Java/Spring rapid | [Java](2_core_java.md) / [Spring](3_spring_and_spring_boot.md) | 2 | :arrows_counterclockwise: checklists only. |
| 109 | Behavioral polish | [Soft skills](15_soft_skills_interview_prep.md) | 2 | :dart: 2-min STAR delivery. |
| 110 | :checkered_flag: **Interview-ready** | [Self-check](17_final_notes_actionable.md#interview-readiness-self-check) | 2 | Complete the readiness self-check → apply broadly. |

> **Checkpoint 6:** all readiness self-check items "Yes." Keep a light DSA + one mock/week going while interviewing.

---

## Accelerated tracks

> Same modules, compressed. Assume the learner already has working knowledge and just needs targeted prep. Confirm company format/AI policy first.

### 60-day track (strong, some gaps · 3–4 h weekday / 6–8 h weekend)
- **W1–2:** DSA core patterns (daily) + Java concurrency/virtual threads + Spring Boot refresh.
- **W3–4:** Databases (transactions/indexing/SQL) + Testing + Security + build the anchor project.
- **W5–6:** System design building blocks + 8 HLD + 6 LLD (heaviest focus).
- **W7:** Observability + Perf + Docker/K8s + Kafka.
- **W8:** Revision week + daily mocks + behavioral + readiness self-check.
- Skip: deep IaC, big data beyond Kafka, advanced/specialist.

### 45-day track (strong, recent design reps · 4 h weekday / 8 h weekend)
- **W1:** DSA patterns + Java/Spring rapid refresh (checklists, not ground-up).
- **W2:** Databases + resilience/idempotency + minimal anchor project (cache+Kafka+security).
- **W3–4:** System design + LLD daily (2 designs/day) — the core of this track.
- **W5:** Observability + K8s essentials + Kafka.
- **W6 (days 43–45):** mock loops + behavioral + gaps.
- Skip: everything ★★☆☆☆ and below; big data; deep cloud.

### 30-day track (very strong, actively interviewing · 4–5 h weekday / 8+ h weekend)
- **Days 1–6:** DSA pattern sprint (recognition speed) + 1 mock/day.
- **Days 7–14:** System design intensive — 1 HLD + 1 LLD daily, always with cost+failure.
- **Days 15–20:** Java/Spring/DB rapid Q&A + fix specific weak spots; skim project (don't build from scratch).
- **Days 21–26:** production topics (observability/K8s/Kafka) at interview depth only + daily mocks.
- **Days 27–30:** full mock loops + behavioral polish + readiness self-check.
- Skip: everything not ★★★★☆+; rely on existing project for stories.

---

## Weekly rhythm (applies to every track)

```
Mon–Fri   1 module topic/day (2–3h) + 2–3 DSA problems (background)
Sat       build (anchor project) + 1 mock
Sun       revision (re-derive prior week) + resume/STAR upkeep
Every 3 wk  revision checkpoint + full mock loop
```

**Burnout guard:** cap heavy new-topic days at one/day; if a mock loop goes badly, spend the next day on that gap, not new material.

---

**Nav:** [◀ Final Notes](17_final_notes_actionable.md) · [Overview](0_overview.md) · [README](README.md)
