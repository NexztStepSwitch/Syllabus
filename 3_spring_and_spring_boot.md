# 3 — Spring & Spring Boot (Boot 3.x / Spring 6 / Security 6)

> **Module rating:** ★★★★★ (Mandatory) · **Difficulty:** Intermediate → Advanced · **Est. effort:** 2–3 weeks · **Depth target:** Production + Interview
> **Baseline:** **Spring Boot 3.3/3.4**, **Spring Framework 6.x** (7.0 GA Nov 2025 for forward notes), **Spring Security 6**, **Java 21**. Legacy items marked.
> **Prerequisites:** [Core Java](2_core_java.md), [Databases](6_databases_relational_nosql.md) (for JPA).
> **Nav:** [◀ Core Java](2_core_java.md) · [Next ▶ System Design](4_system_design.md) · **Related:** [API/Security](7_api_security_networking.md), [Testing](9_testing_quality.md), [Observability](8_observability_monitoring_logging.md)

---

## Why this module

Spring Boot is the default Java backend framework; the "deep dive into what's on your resume" round will hammer it. Interviewers care less about annotation trivia and more about **how the pieces behave in production**: transaction boundaries, N+1 queries, security config, and now **virtual-thread enablement** and the **`RestClient` migration**.

---

## Core (Production + Interview)

### Dependency Injection & bean lifecycle — ★★★★★ · Foundation · 1 day
- **Why:** the mental model everything else builds on.
- **What exactly:** constructor injection (preferred), bean scopes, `@Configuration`/`@Bean`, component scanning, `@ConditionalOn*`, lifecycle callbacks, circular-dependency causes/fixes.
- **Interview Qs:** "field vs constructor injection — why constructor?"; "how does Boot autoconfiguration work?"; "singleton bean with mutable state — what's the risk?"
- **Red flags:** field injection everywhere; mutable state in singletons; `@Autowired` on everything.

### REST controllers, validation, error handling — ★★★★★ · Intermediate · 2 days
- **What exactly:** `@RestController`, `ResponseEntity`, Bean Validation (`@Valid`), `@ControllerAdvice`/`@ExceptionHandler` for a consistent error contract, content negotiation, DTOs (records) vs entities.
- **Interview Qs:** "how do you return consistent error responses?"; "why not expose JPA entities directly?"
- **Red flags:** leaking entities/stack traces to clients; inconsistent error shapes; no input validation.
- **Related:** [API design](7_api_security_networking.md).

### Spring Data JPA / Hibernate — ★★★★★ · Intermediate → Advanced · 3 days
- **Why:** the data layer + the source of the most common production bug: **N+1 queries**.
- **What exactly:** entity mapping, relationships, **lazy vs eager**, `@Transactional` semantics (propagation, rollback rules, proxy self-invocation trap), fetch joins/`@EntityGraph`, the persistence context/dirty checking, `open-in-view=false`, pagination, projections.
- **How deeply:** Production — you can spot and fix N+1 and transaction-boundary bugs.
- **Interview Qs:** "what is N+1 and how do you fix it?"; "why did `@Transactional` not roll back?" (checked exception / self-invocation); "lazy loading exception — cause?" (session closed).
- **Red flags:** `FetchType.EAGER` by default; business logic in entities; giant `@Transactional` spanning external calls; relying on `open-in-view` (hides connection hoarding — worse with virtual threads).
- **Related:** [DB indexing/transactions](6_databases_relational_nosql.md).

### Spring Security 6 + JWT/OAuth2 — ★★★★☆ · Advanced · 2 days
- **What exactly:** the **lambda `SecurityFilterChain`** DSL (Security 6 removed `WebSecurityConfigurerAdapter`), stateless JWT resource server, OAuth2/OIDC login, method security (`@PreAuthorize`), password encoding, CORS/CSRF decisions for APIs.
- **Interview Qs:** "stateless JWT vs session — trade-offs?"; "where do you validate a JWT?"; "how do you handle token refresh/revocation?"
- **Red flags:** JWT with no expiry/rotation; storing secrets in code; disabling CSRF without understanding; symmetric secret shared across services.
- **Related:** [Auth deep dive](7_api_security_networking.md).

### `RestClient` & declarative HTTP Interfaces — ★★★★☆ · Intermediate · 1 day
- **Why:** the **modern Spring HTTP client**. `RestTemplate` is deprecated in favor of `RestClient`: doc-level deprecation in **Spring Framework 7.0** (Nov 2025), formal `@Deprecated` annotation in **7.1** (2026, [issue #36574](https://github.com/spring-projects/spring-framework/issues/36574)), removal targeted for **8.0**.
- **What exactly:** `RestClient` (synchronous, fluent, virtual-thread friendly); declarative `@HttpExchange` interfaces; timeouts, error handling, interceptors; `WebClient` **only** for reactive/WebFlux stacks.
- **Interview Qs:** "which HTTP client for a new Spring MVC service, and why?" (RestClient/HTTP Interfaces); "why is RestTemplate being retired?"
- **Red flags:** choosing `RestTemplate` for greenfield; pulling in WebFlux just to use `WebClient` in a blocking app; no timeouts on outbound calls.

### Virtual threads in Spring Boot — ★★★★☆ · Intermediate · 0.5 day
- **What exactly:** `spring.threads.virtual.enabled=true` (Boot 3.2+) makes Tomcat use a virtual thread per request; pair with `spring.jpa.open-in-view=false`, HikariCP 5.1+, pool sized to the DB, short `connection-timeout`. Not for WebFlux.
- **Interview Qs:** "how do you enable virtual threads in Boot and what else must you check?"
- **Related:** [Core Java virtual threads](2_core_java.md).

### Actuator + Micrometer + observability — ★★★★☆ · Intermediate · 1 day
- **What exactly:** health/readiness/liveness endpoints, metrics via Micrometer, **Micrometer Observation → OpenTelemetry** for traces, structured logging, config via profiles + `@ConfigurationProperties`, externalized config/secrets.
- **Related:** [Observability](8_observability_monitoring_logging.md).

### Testing Spring apps — ★★★★☆ · Intermediate · 1 day
- **What exactly:** `@WebMvcTest` (slice) vs `@SpringBootTest` (full), `MockMvc`, `@DataJpaTest`, **Testcontainers** for real DB/Kafka, `@MockBean`.
- **Related:** [Testing](9_testing_quality.md).

---

## Situational / awareness

- **GraalVM native image — ★★☆☆☆:** fast startup/low memory for serverless/scale-to-zero; build-time complexity. Awareness.
- **Spring AI — ★★☆☆☆:** integrating LLMs (chat, RAG, vector stores) — rising with AI infra questions; know it exists.
- **Spring Batch / Integration / Cloud Gateway — ★★★☆☆:** learn if the role uses them.

## Legacy (stub) — ★☆☆☆☆

> **Why low priority:** deprecated or superseded.
> **Learn only:** recognize them in old codebases.
> **Further reading:** spring.io "state of HTTP clients" (2025-09-30); Spring Framework 7.0/7.1 release notes.
- `RestTemplate` as primary client → use `RestClient`.
- XML bean/`<mvc:*>` config → Java config.
- `WebSecurityConfigurerAdapter` → `SecurityFilterChain` lambda DSL.
- JUnit 4 test base classes → JUnit 5.
- WebFlux/reactive as the *default* → only when truly non-blocking end-to-end.

---

## Hands-on labs & failure scenarios

- **Lab 1:** build a Spring Boot 3.x REST service: DTO records, validation, `@ControllerAdvice`, JPA with Postgres via Testcontainers.
- **Lab 2:** reproduce an N+1 query (enable SQL logging), then fix with `JOIN FETCH`/`@EntityGraph`; measure query count.
- **Lab 3:** secure it with Spring Security 6 stateless JWT; add `@PreAuthorize`.
- **Lab 4:** enable virtual threads; load-test; verify no pinning and correct HikariCP sizing.
- **Failure scenario:** `@Transactional` method calls another `@Transactional` method in the same bean and rollback doesn't happen — explain (self-invocation bypasses the proxy) and fix.
- **Debugging task:** `LazyInitializationException` in a serializer — trace to session boundary + `open-in-view`.

---

## Checklists

### Interview Checklist
- **Must know:** DI + autoconfiguration; `@Transactional` semantics + pitfalls; N+1 + fixes; lazy/eager; Security 6 JWT; `RestClient` vs RestTemplate; virtual-thread enablement; slice vs full tests.
- **Good to know:** Actuator + Micrometer/OTel; profiles/config; `@EntityGraph`; declarative HTTP Interfaces.
- **Bonus:** native image; Spring AI; Batch.

### Production Checklist
- **Must know:** constructor injection; `open-in-view=false`; timeouts on outbound calls; externalized secrets; consistent error contract; health/readiness probes.
- **Good to know:** connection-pool sizing with virtual threads; graceful shutdown.

### Hands-on Checklist
- **Must:** shipped a Boot 3.x service with JPA + Security + tests via Testcontainers.
- **Good:** fixed a real N+1; enabled virtual threads with validation.
- **Bonus:** built a native image; integrated an LLM via Spring AI.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference (baseline **Spring Boot 3.x / Spring Framework 6.x / Spring Security 6**, Jakarta EE namespace). Priorities/depth are in the guide above; **(Legacy)** = recognize only; **(2026)** = modern default.

**1. Spring Core**
- IoC & DI (constructor > setter > field); bean lifecycle; `ApplicationContext` vs `BeanFactory`
- Bean scopes (singleton, prototype, request, session); init/destroy callbacks; autowiring
- Config: annotation & Java `@Configuration`/`@Bean`; XML config **(Legacy)**

**2. Spring AOP**
- Aspect, join point, advice, pointcut, weaving; advice types (Before/After/Around/…)
- Uses: logging, transactions, security; `@Aspect`, `@EnableAspectJAutoProxy`; proxy limitations (self-invocation)

**3. Data access**
- JdbcTemplate / NamedParameterJdbcTemplate; exception translation
- JPA/Hibernate: EntityManager, entity lifecycle, fetch types, N+1 problem
- Transactions: `@Transactional`, propagation, isolation, rollback rules, read-only

**4. Spring MVC**
- DispatcherServlet flow; `@RestController` vs `@Controller`; request mapping annotations
- Path/query params, `@RequestBody`/`@ResponseBody`, validation (`@Valid`, Bean Validation)
- View resolvers / Thymeleaf **(situational; API-first favored)**

**5. Spring Boot fundamentals**
- Auto-configuration, starters, convention over configuration
- `application.yml`/`.properties`, profiles, `@ConfigurationProperties`
- `@SpringBootApplication`; CommandLineRunner/ApplicationRunner

**6. Web development**
- REST controllers, content negotiation, API versioning
- Exception handling: `@ControllerAdvice`, `@ExceptionHandler`, RFC 7807 Problem Details **(2026)**
- Filters & interceptors
- Outbound HTTP: **`RestClient`** / `@HttpExchange` interfaces / WebClient **(2026)**; `RestTemplate` **(Legacy)**

**7. Data & persistence**
- Spring Data JPA: repositories, derived/JPQL/native queries, pagination & sorting, projections, specifications
- DB config: PostgreSQL/MySQL/H2; HikariCP pooling
- Spring Data MongoDB / Redis (situational)

**8. Security (Spring Security 6)**
- AuthN vs AuthZ; `SecurityFilterChain` bean (lambda DSL); `WebSecurityConfigurerAdapter` **(Legacy)**
- UserDetailsService; PasswordEncoder (BCrypt/Argon2)
- JWT stateless auth; OAuth2 resource server & client; OpenID Connect; method security (`@PreAuthorize`)

**9. Microservices (Spring Cloud)**
- Communication: REST, messaging, gRPC
- Service discovery (Eureka/Consul); API Gateway — **Spring Cloud Gateway**; Zuul **(Legacy)**
- Config: Spring Cloud Config; Resilience4j (circuit breaker, retry, fallback, bulkhead)
- Distributed tracing: **Micrometer Tracing + OpenTelemetry** **(2026)**; Sleuth **(Legacy)**

**10. Messaging**
- Kafka (spring-kafka), RabbitMQ; Spring Cloud Stream (producers/consumers, bindings) → see [Data Eng](13_data_engineering_big_data.md)

**11. Testing**
- JUnit 5 + Mockito; `@SpringBootTest`, slices (`@WebMvcTest`, `@DataJpaTest`), MockMvc / `WebTestClient`
- Testcontainers (real DB/broker) **(2026)**; WireMock for external services → see [Testing](9_testing_quality.md)

**12. Actuator & observability**
- Actuator endpoints (health, metrics, info); custom endpoints
- Micrometer → Prometheus/Grafana; Micrometer Observation API **(2026)** → see [Observability](8_observability_monitoring_logging.md)

**13. Deployment & runtime**
- JAR (embedded Tomcat) vs WAR; profiles & externalized config
- Docker, Kubernetes, cloud → see [DevOps/Cloud](11_devops_cicd_cloud.md)
- **Virtual threads** (`spring.threads.virtual.enabled`) **(2026)**; GraalVM native image (situational)

**14. Best practices**
- Layered architecture (Controller → Service → Repository); DTOs vs entities; avoid N+1; consistent exception handling; config management; structured logging

---

**Nav:** [◀ Core Java](2_core_java.md) · [Next ▶ System Design](4_system_design.md)
