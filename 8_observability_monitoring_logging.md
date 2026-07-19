# 8 — Observability, Monitoring & Logging

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Intermediate · **Est. effort:** 4–5 days · **Depth target:** Production + Interview
> **Baseline:** **OpenTelemetry-first** (the industry standard).
> **Prerequisites:** [Spring Actuator/Micrometer](3_spring_and_spring_boot.md), [Microservices](5_microservices_distributed_systems.md).
> **Nav:** [◀ API/Security](7_api_security_networking.md) · [Next ▶ Testing](9_testing_quality.md) · **Related:** [Performance](10_performance_profiling_reliability.md), [DevOps](11_devops_cicd_cloud.md)

---

## Why this module

You cannot operate distributed systems you cannot see. In 2026, "observability-first" is an explicit expectation and appears on system-design rubrics (failure modes + monitoring). The shift is from ad-hoc logs to **correlated traces + metrics + logs**, and from raw dashboards to **SLOs + error budgets**.

> **The three pillars, correlated:** metrics tell you *something is wrong*, traces tell you *where*, logs tell you *why*. The 2026 skill is stitching them via trace/correlation IDs.

---

## Core

### Structured logging + correlation — ★★★★★ · Intermediate · 1 day
- **What exactly:** JSON structured logs, log levels, **correlation/trace IDs** propagated across services (MDC), no PII/secrets in logs, sampling, log volume/cost awareness.
- **Interview Qs:** "how do you trace one request across 5 services in logs?" (propagated correlation ID); "what do you never log?"
- **Red flags:** `System.out.println`; logging secrets/PII; unstructured logs; logging in hot loops.

### Metrics (Prometheus / Micrometer) — ★★★★☆ · Intermediate · 1 day
- **What exactly:** counters/gauges/histograms/summaries, **RED** (Rate, Errors, Duration) for services and **USE** (Utilization, Saturation, Errors) for resources, percentiles (p50/p95/p99), cardinality pitfalls, dashboards (Grafana), alerting rules.
- **Interview Qs:** "which metrics for a REST service?" (RED); "why is average latency misleading?" (use p99); "what is a high-cardinality label and why is it dangerous?"
- **Related:** [Tail latency](10_performance_profiling_reliability.md).

### Tracing + OpenTelemetry — ★★★★☆ · Intermediate · 1 day
- **What exactly:** spans/traces, context propagation, **OpenTelemetry** (vendor-neutral SDK + Collector), exporting to Jaeger/Tempo, sampling (head vs tail), Micrometer Observation → OTel in Spring Boot 3.
- **Interview Qs:** "how does distributed tracing work?"; "head vs tail sampling trade-offs?"; "why OpenTelemetry over vendor SDKs?" (portability).

### SLI / SLO / error budgets — ★★★★☆ · Intermediate · 0.5 day
- **What exactly:** SLI (measured), SLO (target), SLA (contract), error budgets driving release decisions, alert on symptoms/burn-rate not causes.
- **Interview Qs:** "define an SLO for a checkout API"; "what is an error budget and how does it change how you ship?"

## Situational
- **ELK / EFK stack — ★★★☆☆:** log aggregation/search; many shops consolidating toward Loki + OTel [MIXED]. Know the concept.
- **APM tools (Datadog/New Relic) — ★★★☆☆:** managed observability; awareness.

---

## Hands-on labs & failure scenarios

- **Lab 1:** instrument a Spring Boot 3 service with Micrometer + OTel; export traces to Jaeger/Tempo and metrics to Prometheus; view p99 in Grafana.
- **Lab 2:** propagate a correlation ID across two services and follow one request end-to-end in logs + traces.
- **Lab 3:** define an SLO + a burn-rate alert.
- **Failure scenario:** p99 latency spikes but averages look fine — use the trace to find the slow downstream span.
- **Debugging task:** a high-cardinality label (user ID) blows up Prometheus memory — fix the metric design.

---

## Checklists

### Interview Checklist
- **Must know:** three pillars + correlation IDs; RED/USE; p99 vs average; distributed tracing; SLI/SLO/error budget; OpenTelemetry.
- **Good to know:** sampling strategies; alert-on-symptoms; cardinality pitfalls.
- **Bonus:** tail-based sampling; OTel Collector architecture.

### Production Checklist
- **Must know:** structured logs + correlation; RED metrics + p99 alerts; no PII in logs; health/readiness probes.
- **Good to know:** error-budget-driven releases; trace-metric-log correlation in one pane.

### Hands-on Checklist
- **Must:** instrumented a service with OTel; built a RED dashboard.
- **Good:** end-to-end trace across services; defined an SLO.
- **Bonus:** tuned sampling for cost.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference (**OpenTelemetry-first**). Priorities/depth are in the guide above.

**1. Fundamentals**
- Monitoring vs observability
- Three pillars: logs, metrics, traces (+ events); when each is the right tool

**2. Logging**
- Structured (JSON) vs unstructured; log levels; correlation IDs / trace IDs in logs
- Aggregation (ELK/EFK, Loki); rotation & retention; PII scrubbing; cost control

**3. Metrics & monitoring**
- Instrumentation: Micrometer; method types (counter, gauge, timer, histogram)
- Method frameworks: RED (Rate, Errors, Duration), USE (Utilization, Saturation, Errors)
- Percentiles (p50/p95/p99) vs averages; system vs app vs business metrics
- Tools: Prometheus (PromQL basics), Grafana, CloudWatch, Datadog

**4. Distributed tracing**
- Spans, traces, context propagation; sampling strategies
- OpenTelemetry (SDK, collector); Jaeger / Zipkin; instrumenting a Spring Boot service

**5. SLI / SLO / error budgets**
- Defining SLIs; setting SLOs; error budgets & burn-rate alerts; SLA vs SLO

**6. Alerting & incident management**
- Alert thresholds & rules; symptom-based vs cause-based alerting; reducing alert noise/fatigue
- On-call, escalation (PagerDuty/Opsgenie); runbooks; blameless post-mortems

**7. Practice & interview**
- Set up Prometheus + Grafana; add OTel tracing to a service; design low-noise alerts
- Trace a request across microservices; monitoring vs observability; debugging a p99 latency spike

---

**Nav:** [◀ API/Security](7_api_security_networking.md) · [Next ▶ Testing & Quality](9_testing_quality.md)
