# 7 — API, Security & Networking

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Intermediate · **Est. effort:** 1 week · **Depth target:** Interview + Production
> **Prerequisites:** [Spring Security](3_spring_and_spring_boot.md), [System Design](4_system_design.md).
> **Nav:** [◀ Databases](6_databases_relational_nosql.md) · [Next ▶ Observability](8_observability_monitoring_logging.md) · **Related:** [Microservices](5_microservices_distributed_systems.md), [Misc/secrets](16_misc_nice_to_have.md)

---

## Why this module

Every backend engineer designs APIs and is expected to reason about **auth** and the **OWASP Top 10** — security lapses are hard-fail signals. Networking is mostly a *debugging* skill: enough to diagnose latency and connection issues, not to pass a networking exam.

---

## Core

### REST API design — ★★★★★ · Intermediate · 1 day
- **What exactly:** resource modeling, correct status codes, versioning (URI vs header), **pagination (cursor > offset at scale)**, filtering/sorting, idempotency for retries, consistent error contract, rate limiting, OpenAPI/Swagger.
- **Interview Qs:** "design the API for X"; "offset vs cursor pagination?"; "how do you version without breaking clients?"; "make POST safe to retry" (idempotency key).
- **Red flags:** verbs in URLs, 200 for errors, unbounded list endpoints, breaking changes without versioning.
- **Related:** [API design in system design](4_system_design.md).

### Authentication & Authorization — ★★★★★ · Advanced · 2 days
- **What exactly:** authN vs authZ; **OAuth2** flows (authorization code + PKCE, client credentials), **OIDC** (ID token), **JWT** structure/validation/**pitfalls** (expiry, rotation, `alg=none`, revocation, don't store sensitive data), refresh tokens, session vs token trade-offs, RBAC/ABAC.
- **Interview Qs:** "walk through OAuth2 authorization code + PKCE"; "how do you revoke a stateless JWT?" (short TTL + denylist/rotation); "where do you validate the token in microservices?" (gateway + per-service).
- **Red flags:** long-lived JWTs with no rotation; secrets in code/JWT; trusting client-side claims; symmetric secret shared everywhere.

### TLS & encryption — ★★★★☆ · Intermediate · 0.5 day
- **What exactly:** TLS handshake basics, cert chains, mTLS (service-to-service), encryption in transit vs at rest, KMS for keys.
- **Interview Qs:** "encryption in transit vs at rest?"; "what is mTLS and when?"
- **Related:** [Secrets/KMS](16_misc_nice_to_have.md).

### OWASP Top 10 + input validation — ★★★★★ · Intermediate · 1 day
- **What exactly:** injection (SQL/command), broken auth, broken access control, SSRF, insecure deserialization, security misconfig, sensitive data exposure; parameterized queries; validation + output encoding; secrets management; dependency scanning.
- **Interview Qs:** "how do you prevent SQL injection?" (parameterized queries); "how would you find an IDOR?"; "how do you handle dependency CVEs?"
- **Red flags:** string-concatenated SQL; trusting client input; verbose error leakage.

### HTTP / DNS / TCP fundamentals — ★★★★☆ · Foundation · 1 day
- **What exactly:** HTTP methods/status/headers, HTTP/1.1 vs HTTP/2 (multiplexing) vs HTTP/3 (QUIC) at a high level, keep-alive, DNS resolution, TCP handshake + TLS overhead, idempotent/safe methods.
- **Interview Qs:** "what happens when you type a URL and hit enter?"; "why is HTTP/2 faster?"; "connection pooling — why?"

## Situational
- **gRPC — ★★★☆☆:** protobuf, streaming, low-latency internal comms. Learn if the stack uses it. See [Microservices comms](5_microservices_distributed_systems.md).
- **GraphQL — ★★★☆☆:** flexible client queries; N+1 + caching complexity. Awareness unless the role uses it.
- **Sockets / low-level networking — ★★☆☆☆:** debugging-only (`tcpdump`, `ss`, connection states).

## Legacy / low-ROI (stub) — ★☆☆☆☆
> **Why low priority:** rarely required in practice.
> **Learn only:** recognize the term.
> **HATEOAS / rich hypermedia REST** — know it exists; almost never expected.

---

## Hands-on labs & failure scenarios

- **Lab 1:** implement OAuth2 authorization-code + PKCE against a provider; validate JWTs in a Spring resource server.
- **Lab 2:** add cursor pagination + idempotency keys to a write endpoint.
- **Lab 3:** run an OWASP scan (e.g. dependency-check/ZAP) on your project; fix findings.
- **Failure scenario:** an attacker replays a request — your idempotency + rate limiting must handle it.
- **Debugging task:** intermittent 502s under load — trace to connection-pool exhaustion / missing keep-alive.

---

## Checklists

### Interview Checklist
- **Must know:** REST design + status codes + pagination + versioning + idempotency; OAuth2/OIDC/JWT + pitfalls; OWASP Top 10; TLS in-transit/at-rest; HTTP semantics.
- **Good to know:** mTLS; HTTP/2 vs HTTP/3; gRPC basics; RBAC/ABAC.
- **Bonus:** GraphQL trade-offs; QUIC internals.

### Production Checklist
- **Must know:** parameterized queries; validated inputs; secrets in a vault/KMS; TLS everywhere; token TTL + rotation.
- **Good to know:** dependency CVE scanning; security headers (CORS/CSP/HSTS).

### Hands-on Checklist
- **Must:** implemented OAuth2/JWT; ran a security scan.
- **Good:** added idempotency + cursor pagination.
- **Bonus:** set up mTLS between two services.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above; **(low ROI)** = awareness only.

**1. API fundamentals**
- REST: resources, endpoints, verbs, status codes; pagination & filtering
- GraphQL (basics, when to use); gRPC & Protocol Buffers (when to use)

**2. API design best practices**
- Versioning strategies (URI, header, media-type)
- Error handling (RFC 7807 Problem Details); idempotency & idempotency keys
- Documentation: OpenAPI/Swagger, Postman
- HATEOAS **(low ROI)**

**3. Networking**
- OSI & TCP/IP models; DNS; HTTP/1.1 vs HTTP/2 vs HTTP/3; HTTPS
- TCP handshake, connection reuse/keep-alive; load balancing (L4 vs L7)
- Reverse proxies (Nginx, HAProxy); CDN basics

**4. Security principles**
- AuthN: Basic Auth, API keys, OAuth 2.0, OpenID Connect, JWT (structure, signing, expiry, common pitfalls)
- AuthZ: RBAC, ABAC; scopes
- TLS/SSL basics, mTLS; CORS; cookies vs tokens; session vs stateless

**5. API security practices**
- Rate limiting & throttling; API gateway integration; secret management (Vault/KMS)
- OWASP Top 10; preventing SQL injection, CSRF, XSS, SSRF, DDoS
- Input validation, output encoding, least privilege

**6. Practice & interview**
- Secure a REST API with JWT; design a payment API; rate limiting with Redis
- Explain OAuth2 authorization-code flow; authN vs authZ; REST vs GraphQL vs gRPC trade-offs

---

**Nav:** [◀ Databases](6_databases_relational_nosql.md) · [Next ▶ Observability](8_observability_monitoring_logging.md)
