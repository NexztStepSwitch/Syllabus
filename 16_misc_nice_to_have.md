# 16 — Misc / Nice-to-have

> **Module rating:** ★★★☆☆ (Situational) · **Difficulty:** Mixed · **Est. effort:** 1–2 days total · **Depth target:** Awareness → Production (as needed)
> **Prerequisites:** [System Design](4_system_design.md), [API/Security](7_api_security_networking.md), [Databases](6_databases_relational_nosql.md).
> **Nav:** [◀ Soft Skills](15_soft_skills_interview_prep.md) · [Next ▶ Final Notes](17_final_notes_actionable.md) · **Related:** [DevOps](11_devops_cicd_cloud.md), [Performance](10_performance_profiling_reliability.md)

---

## Why this module

A short catch-all for cross-cutting concerns that recur in design rounds but don't warrant a full module. Each is cross-linked to where it's covered more deeply — **avoid duplicating study**.

---

## Topics

### CDN & edge caching — ★★★★☆ · Intermediate · 0.5 day
- **What exactly:** static + dynamic edge caching, cache-control headers, invalidation/purge, edge rate limiting/DDoS protection, geo-routing.
- **Interview relevance:** "how do you serve global users with low latency?" (CDN + regional replicas).
- **Related:** [Caching](4_system_design.md), [Performance](10_performance_profiling_reliability.md).

### Secrets management & KMS — ★★★★☆ · Intermediate · 0.5 day
- **What exactly:** never in code/env-in-repo; Vault / cloud Secrets Manager / Parameter Store; envelope encryption + KMS; rotation; least-privilege access.
- **Interview relevance:** "where do secrets live and how are they rotated?"
- **Related:** [Security](7_api_security_networking.md), [Cloud IAM](11_devops_cicd_cloud.md).

### Data modeling patterns — ★★★☆☆ · Intermediate · 0.5 day
- **What exactly:** normalization vs denormalization by access pattern, single-table design (DynamoDB), read/write ratio driving the model, materialized views.
- **Related:** [Databases](6_databases_relational_nosql.md).

### Feature flags — ★★★☆☆ · Intermediate · 0.5 day
- **What exactly:** decouple deploy from release, gradual rollout, kill switches, experimentation; flag debt/cleanup.
- **Interview relevance:** "how do you safely roll out a risky change?" (flag + canary + kill switch).
- **Related:** [Deploy strategies](11_devops_cicd_cloud.md).

### Time-series patterns — ★★☆☆☆ · Intermediate · 0.5 day
- Metrics storage, downsampling/retention. See [Observability](8_observability_monitoring_logging.md) and [Databases](6_databases_relational_nosql.md).

---

## Checklists

### Interview Checklist
- **Must know:** CDN for global latency; where secrets live + rotation; denormalize by access pattern; feature-flag rollout + kill switch.
- **Good to know:** envelope encryption/KMS; materialized views; edge rate limiting.
- **Bonus:** experimentation platforms; time-series downsampling.

### Production Checklist
- **Must know:** no secrets in code; cache-control correctness; safe rollout mechanism.
- **Good to know:** secret rotation; flag cleanup discipline.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Cross-cutting / nice-to-have; keep to **awareness** unless a role needs more. Priorities/depth are in the guide above.

**1. Cross-cutting backend concerns (useful)**
- CDN & edge caching; cache invalidation strategies
- Secrets management (Vault, AWS KMS/Secrets Manager)
- Data modeling patterns (time-series, soft deletes, audit logs, multi-tenancy)
- Feature flags & progressive delivery (LaunchDarkly, Unleash) → see [DevOps](11_devops_cicd_cloud.md)
- Rate limiting patterns (token bucket, leaky bucket)

**2. Security awareness**
- OWASP Top 10; common vulnerabilities → see [API & Security](7_api_security_networking.md)

**3. Networking awareness**
- VPN, firewalls, TCP/IP details → see [API & Security](7_api_security_networking.md)

**4. Adjacent ecosystem (awareness only)**
- Frontend basics (HTML/CSS/JS, React/Angular awareness)
- Mobile awareness (Android/iOS fundamentals, REST consumption)

**5. Emerging trends (awareness)**
- AI/ML basics & LLM app patterns → see [Advanced](14_advanced_specialist_topics.md)
- Edge computing; WebAssembly (awareness); blockchain (low ROI)

**6. Checklist**
- Awareness of the ecosystem beyond backend; stay current with trends without chasing hype

---

**Nav:** [◀ Soft Skills](15_soft_skills_interview_prep.md) · [Next ▶ Final Notes (actionable)](17_final_notes_actionable.md)
