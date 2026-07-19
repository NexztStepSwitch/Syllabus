# Backend Engineer Roadmap (2026-ready) — for ~3.5 YOE

> The shortest defensible path from fundamentals to offer for a **Java/Spring backend engineer with ~3.5 years of experience** targeting high-quality product companies (FAANG, global product, fintech, high-scale SaaS, and Indian product companies) in **2026 and beyond**.
>
> Every topic here justifies its existence. If something does not improve **interview performance**, **production skill**, or **engineering judgment**, it has been downgraded to a stub or marked Legacy — not padded out.

---

## 1. Purpose

This repo is **both a syllabus and a guide**. Every module has two layers:

- **The guide (top of each module):** a **priority engine** that tells you what to study, how deeply, and in what order. It answers three questions on every page:
  1. **Should I study this?** (a rating + a one-line reason)
  2. **How deeply, and by when?** (depth level + effort estimate + YOE expectation)
  3. **What next?** (prerequisites + navigation links, so you never search "what do I learn next?")
- **The detailed syllabus (bottom of each module):** the full, exhaustive **topic checklist** under a `## Detailed Syllabus (topic checklist)` heading — the complete inventory of sub-topics for that area, pruned of obsolete items and refreshed for 2026 (items flagged `(Legacy)`, `(low ROI)`, `(situational)`, `(2026)`). Use it to make sure you haven't missed anything.

> **How the two layers work together:** the guide tells you *what matters and why*; the detailed syllabus is the *complete tick-list* of every topic. Skim the guide to plan, then use the detailed syllabus to verify coverage.

It is grounded in live 2025–2026 hiring research. Every priority change traces back to that evidence base.

## 2. Target audience

- Backend engineers with **~3–4 years** of experience (calibrated to **3.5 YOE**).
- Primary stack: **Java 21 + Spring Boot 3.x**. Concepts transfer to other stacks.
- Goal: clear multi-round loops (DSA + LLD + HLD + behavioral) at product companies.

If you have ~2 YOE, follow the same path but expect the ★★★★☆ / ★★★☆☆ material to take longer. If you have 5+ YOE, use the [30/45/60-day accelerated tracks](18_learning_timeline.md#accelerated-tracks).

## 3. Learning philosophy

- **Fundamentals from ground zero, but fast.** Basics are revisited (marked `Difficulty: Foundation`) so nothing is assumed — but you spend real time on the 3.5-YOE material, not on re-teaching arrays.
- **Production-first.** Every concept answers at least one of: why it exists, what problem it solves, what breaks without it, how it's debugged, when *not* to use it.
- **Interview ROI over completeness.** We optimize for what recurs across companies, not for exotic trivia.
- **Judgment beats recall.** In 2026, AI can produce the algorithm. You are hired for trade-offs, failure modes, and cost — so those are foregrounded everywhere.

## 4. How to use this repository

1. Read this README, then the **module map** below (or [`0_overview.md`](0_overview.md) for the master priority table).
2. Pick a track in [`18_learning_timeline.md`](18_learning_timeline.md) (90–120 day default; 30/45/60 accelerated).
3. Work modules in order. Each module has: rated topics, depth targets, interview Qs, red flags, checklists, and hands-on labs.
4. Use the **Must know / Good to know / Bonus** checklists at the end of each module as your self-assessment gate, and the **`Detailed Syllabus (topic checklist)`** at the very bottom of each module to confirm you've covered every sub-topic.
5. Revise on weekends; run mock interviews at the checkpoints; update your resume at the milestones.

---

## 5. Priority legend (importance for a 3.5 YOE backend engineer)

| Rating | Meaning | What it implies for you |
|--------|---------|-------------------------|
| ★★★★★ | **Mandatory** | Expected in nearly every interview. Master it. |
| ★★★★☆ | **High ROI** | Appears frequently. Strong ROI on study time. |
| ★★★☆☆ | **Situational** | Company/role-dependent. Know it if targeting that domain. |
| ★★☆☆☆ | **Differentiator** | Separates strong candidates; not required to pass. |
| ★☆☆☆☆ | **Low ROI** | Learn basics only; don't spend pages on it. |

Every rating in this repo carries a short justification. Ratings were re-derived from current hiring trends, not inherited.

## 6. Difficulty legend (independent of importance)

`Foundation` · `Intermediate` · `Advanced` · `Specialized`

A topic can be **high importance + low difficulty** (e.g. Records) or **low importance + high difficulty** (e.g. Paxos internals). The two axes are tracked separately.

## 7. YOE expectation legend

Each major topic notes what is expected at **2 / 3.5 / 5+ YOE** so you neither under- nor over-study. Example: *Virtual Threads — 2 YOE: aware; 3.5 YOE: can enable + avoid pinning; 5+ YOE: can tune carrier pool + diagnose in prod.*

## 8. Effort estimates

Topics carry a study-time budget: `30 min` · `2 h` · `1 day` · `2 days` · `1 week`. Never study deep without a matching ROI.

## 9. Depth levels

`Surface` (recognize) → `Intermediate` (use with docs) → `Production` (ship + operate) → `Interview` (explain + defend trade-offs) → `Expert` (design + tune + debug under failure).

---

## 10. Module map

| # | Module | Rating | Difficulty | Focus (2026) |
|---|--------|--------|-----------|--------------|
| 1 | [DSA](1_dsa.md) | ★★★★★ | Foundation→Advanced | Pattern fluency under time pressure |
| 2 | [Core Java](2_core_java.md) | ★★★★★ | Foundation→Advanced | Java 21, concurrency, virtual threads |
| 3 | [Spring & Spring Boot](3_spring_and_spring_boot.md) | ★★★★★ | Intermediate→Advanced | Boot 3.x, RestClient, Security 6, JPA |
| 4 | [System Design (HLD + LLD)](4_system_design.md) | ★★★★★ | Intermediate→Advanced | Trade-offs, cost, failure modes, LLD |
| 5 | [Microservices & Distributed Systems](5_microservices_distributed_systems.md) | ★★★★☆ | Advanced | Resilience, SAGA, delivery semantics |
| 6 | [Databases (SQL & NoSQL)](6_databases_relational_nosql.md) | ★★★★★ | Intermediate→Advanced | Transactions, indexing, selection |
| 7 | [API, Security & Networking](7_api_security_networking.md) | ★★★★☆ | Intermediate | OAuth2/OIDC, JWT, OWASP, gRPC |
| 8 | [Observability](8_observability_monitoring_logging.md) | ★★★★☆ | Intermediate | OpenTelemetry, SLO/error budgets |
| 9 | [Testing & Quality](9_testing_quality.md) | ★★★★☆ | Intermediate | JUnit 5, Mockito, Testcontainers |
| 10 | [Performance & Reliability](10_performance_profiling_reliability.md) | ★★★★☆ | Advanced | Profiling, tail latency, resilience |
| 11 | [DevOps, CI/CD & Cloud](11_devops_cicd_cloud.md) | ★★★★☆ | Intermediate→Advanced | Docker, K8s essentials, CI/CD, AWS |
| 12 | [Build & Tooling](12_build_tooling.md) | ★★★☆☆ | Foundation | Maven/Gradle, Git |
| 13 | [Data Engineering](13_data_engineering_big_data.md) | ★★★☆☆ | Intermediate | Kafka (core); Spark/ETL (optional) |
| 14 | [Advanced/Specialist](14_advanced_specialist_topics.md) | ★★☆☆☆ | Specialized | Event sourcing, CQRS, consensus, mesh |
| 15 | [Soft Skills & Interview Prep](15_soft_skills_interview_prep.md) | ★★★★★ | Foundation | STAR, trade-off comms, storytelling |
| 16 | [Misc / Nice-to-have](16_misc_nice_to_have.md) | ★★★☆☆ | Mixed | CDN, secrets/KMS, data modeling |
| 18 | [Learning Timeline](18_learning_timeline.md) | — | — | Day-by-day execution plan + anchor project + readiness self-check |

Supporting docs: [`0_overview.md`](0_overview.md) (master priority table).

---

## 11. Recommended learning order

```
Foundations        1 DSA  →  2 Core Java  →  12 Build/Git
Framework          3 Spring Boot  →  6 Databases  →  9 Testing
Design             4 System Design (HLD+LLD)  →  5 Microservices
Production         7 API/Security  →  8 Observability  →  10 Perf/Reliability  →  11 DevOps/Cloud
Depth (optional)   13 Data Eng  →  14 Advanced  →  16 Misc
Throughout         15 Soft skills + mock interviews
```

Full day-by-day schedule: [`18_learning_timeline.md`](18_learning_timeline.md).

## 12. Estimated completion

| Track | Who | Weekday | Weekend | Duration |
|-------|-----|---------|---------|----------|
| **Primary** | 3.5 YOE, balanced | 2–3 h | 5–6 h | **90–120 days** |
| Accelerated 60 | strong, some gaps | 3–4 h | 6–8 h | 60 days |
| Accelerated 45 | strong, recent design reps | 4 h | 8 h | 45 days |
| Accelerated 30 | very strong, active interviewer | 4–5 h | 8+ h | 30 days |

## 13. Interview strategy

- **Coding round:** recognize the pattern in <2 min, narrate the approach, state complexity, handle edge cases. If AI is allowed (confirm with recruiter), your job is to *drive and verify*, catching the model's mistakes.
- **LLD / machine coding:** clarify requirements → entities → class diagram → SOLID + one or two design patterns → concurrency/thread-safety → extensibility. Practice: parking lot, logger, coupon, inventory, rate limiter.
- **HLD / system design:** clarify → back-of-envelope capacity → high-level → deep-dive 1–2 components → **scale + cost + failure modes + observability** → trade-offs. Never say "add more servers."
- **Behavioral:** STAR, ownership, measurable impact; align your stories to the role.

## 14. Revision strategy

- **Weekend consolidation:** re-derive, don't re-read. Redo one design and one LLD out loud.
- **Spaced repetition:** each module's checklists are your flashcards.
- **Revision weeks** (built into the timeline) before mock-interview checkpoints.
- **Final sprint:** the last 1–2 weeks are pure mocks + weak-area patching.

## 15. Common mistakes (that cost offers)

- Grinding DSA volume while neglecting system design and behavioral. (Design carries more weight now.)
- Name-dropping Kafka/Cassandra without explaining the property it provides.
- Jumping to a design before clarifying scale, read/write ratio, and consistency needs.
- Ignoring cost and failure modes.
- Learning Legacy tech (RestTemplate as primary, Spring XML, JUnit 4) instead of current equivalents.
- Over-studying specialist topics (Paxos proofs, service-mesh internals) that rarely gate offers.

## 16. How to study efficiently

- Follow the ratings: spend 80% of time on ★★★★★/★★★★☆.
- Stub the ★☆☆☆☆ topics — read the "Learn only these basics" box and move on.
- Build **one** end-to-end project (see timeline milestones) that touches Spring Boot + DB + cache + Kafka + Docker + observability. It anchors your resume and your design stories.
- Do hands-on labs; interviewers can tell theory from practice.

---

Start here → [`0_overview.md`](0_overview.md) (priority table) or jump straight to [`18_learning_timeline.md`](18_learning_timeline.md).
