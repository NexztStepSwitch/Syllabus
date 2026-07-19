# 10 — Performance, Profiling & Reliability

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Advanced · **Est. effort:** 1 week · **Depth target:** Production + Interview
> **Prerequisites:** [Core Java (memory/GC, concurrency)](2_core_java.md), [Databases (indexing)](6_databases_relational_nosql.md), [Microservices (resilience)](5_microservices_distributed_systems.md).
> **Nav:** [◀ Testing](9_testing_quality.md) · [Next ▶ DevOps/CI/CD/Cloud](11_devops_cicd_cloud.md) · **Related:** [Observability](8_observability_monitoring_logging.md), [System Design](4_system_design.md)

---

## Why this module

At 3.5 YOE you're expected to **diagnose**, not just build. "The service got slow" is a common interview scenario and a daily production task. The skills: read a profile, understand **tail latency**, and apply **resilience patterns** so partial failures don't become outages.

> **Golden rule:** measure before optimizing. "Premature optimization" and "optimizing without a profiler" are both red flags.

---

## Core

### Latency & tail latency (p99) — ★★★★☆ · Advanced · 1 day
- **Why:** users feel the tail; averages lie. At scale, one request touching many services means p99 of each becomes the common case.
- **What exactly:** percentiles, latency budgets across a call chain, fan-out amplification, timeouts + hedged requests, why p99 > average matters.
- **Interview Qs:** "why optimize p99 not average?"; "a request fans out to 10 services each with p99=100ms — what's the effective latency?"
- **Related:** [Metrics/percentiles](8_observability_monitoring_logging.md).

### Caching for performance — ★★★★★ · Intermediate · 0.5 day
- **What exactly:** where to cache (client/CDN/app/DB), what to cache, invalidation, hit ratio, stampede/hot keys.
- **Related:** [Caching in system design](4_system_design.md).

### JVM profiling — ★★★★☆ · Advanced · 1 day
- **What exactly:** **JFR (Java Flight Recorder)** + async-profiler, **flame graphs**, CPU vs allocation profiling, thread dumps (deadlocks, hot locks), heap dumps (leaks), GC log analysis, virtual-thread pinning events (`jdk.VirtualThreadPinned`).
- **Interview Qs:** "service CPU is 100% — how do you find the hot method?" (profiler/flame graph); "how do you debug a memory leak / OOM?" (heap dump + dominator tree); "how do you find a deadlock?" (thread dump).
- **Related:** [GC](2_core_java.md).

### Resilience patterns — ★★★★☆ · Advanced · 1 day
- **What exactly:** circuit breaker, bulkhead, timeouts, retries+backoff+jitter, graceful degradation, load shedding (Resilience4j). Cross-links [Microservices](5_microservices_distributed_systems.md).
- **Interview Qs:** "how do you keep one slow dependency from taking down the service?"

### Capacity & autoscaling — ★★★☆☆ · Advanced · 0.5 day
- **What exactly:** capacity estimation, headroom, HPA (CPU/custom metrics), scale-up latency, cost vs headroom trade-off.
- **Related:** [K8s HPA](11_devops_cicd_cloud.md), [Cost in design](4_system_design.md).

### Microbenchmarking — ★★★☆☆ · Advanced · 0.5 day
- **What exactly:** JMH, warmup/JIT effects, avoiding benchmark pitfalls (dead-code elimination). Know that microbenchmarks rarely predict system behavior.

---

## Hands-on labs & failure scenarios

- **Lab 1:** profile a CPU-hot endpoint with async-profiler; read the flame graph; fix the hot path; re-measure.
- **Lab 2:** trigger + capture an OOM heap dump; find the leak in a dominator tree.
- **Lab 3:** measure p50/p99 under load; add a cache; show the p99 improvement.
- **Failure scenario:** a retry storm during a downstream blip amplifies load 5x — add backoff+jitter+circuit breaker and re-test.
- **Debugging task:** thread pool exhausted; take a thread dump, find the blocking call, fix (timeout / async / virtual threads).

---

## Checklists

### Interview Checklist
- **Must know:** p99 vs average + fan-out; profiling (flame graphs, thread/heap dumps); GC/leak diagnosis; resilience patterns; caching for latency.
- **Good to know:** hedged requests; autoscaling; capacity math.
- **Bonus:** JMH; latency budgeting across chains.

### Production Checklist
- **Must know:** measure before optimizing; timeouts + circuit breakers; alert on p99; bounded resources.
- **Good to know:** GC log monitoring; autoscaling policies; load tests before peaks.

### Hands-on Checklist
- **Must:** produced a flame graph; analyzed a heap dump; improved p99 with a change.
- **Good:** survived a simulated retry storm; tuned autoscaling.
- **Bonus:** wrote a valid JMH benchmark.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above.

**1. Performance fundamentals**
- Latency vs throughput; response-time distribution (p50/p95/p99), tail latency
- Bottleneck analysis; Amdahl's & Little's law (awareness); Little's law for capacity

**2. Profiling (JVM-focused)**
- CPU profiling; allocation/memory profiling; wall-clock vs CPU time
- Tools: JDK Flight Recorder (JFR), async-profiler, flame graphs, VisualVM; JProfiler/YourKit (commercial)
- Heap dumps & analysis (MAT); thread dumps (deadlocks, contention); GC logs

**3. JVM tuning**
- Heap sizing; GC selection (G1 vs ZGC); GC pause analysis
- JIT warm-up; escape analysis; microbenchmarking with JMH (avoid naive benchmarks)

**4. Reliability engineering**
- SLI / SLO / SLA; error budgets; chaos engineering (awareness)

**5. Optimization techniques**
- Caching; connection pooling; query optimization; batching; async/non-blocking; reducing allocations

**6. Fault tolerance & resilience**
- Circuit breaker, retry + backoff + jitter, timeouts, bulkhead (Resilience4j); graceful degradation; load shedding → see [Microservices](5_microservices_distributed_systems.md)

**7. Load & stress testing**
- Tools: k6, Gatling, JMeter, Locust; load vs stress vs spike vs soak
- Monitoring resources under load; finding the knee point → see [Testing](9_testing_quality.md)

**8. Capacity planning**
- Throughput/latency targets; headroom; autoscaling signals; cost vs performance trade-offs

**9. Interview**
- How to profile a slow Java service; diagnose a p99 spike; find a memory leak; design for an SLA; performance vs reliability trade-offs

---

**Nav:** [◀ Testing](9_testing_quality.md) · [Next ▶ DevOps, CI/CD & Cloud](11_devops_cicd_cloud.md)
