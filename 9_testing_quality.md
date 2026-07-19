# 9 — Testing & Quality

> **Module rating:** ★★★★☆ (High ROI) · **Difficulty:** Intermediate · **Est. effort:** 4–5 days · **Depth target:** Production
> **Baseline:** **JUnit 5 (Jupiter)**, **Mockito**, **Testcontainers**. JUnit 4 = Legacy.
> **Prerequisites:** [Core Java](2_core_java.md), [Spring testing](3_spring_and_spring_boot.md).
> **Nav:** [◀ Observability](8_observability_monitoring_logging.md) · [Next ▶ Performance & Reliability](10_performance_profiling_reliability.md) · **Related:** [Build tooling](12_build_tooling.md), [DevOps CI/CD](11_devops_cicd_cloud.md)

---

## Why this module

Testing is judged more by **habits and design** than trivia: can you write fast, isolated unit tests and realistic integration tests? The modern differentiator is **Testcontainers** — testing against a real Postgres/Kafka in a container instead of mocks/H2.

> **The test pyramid:** many fast unit tests, fewer integration tests, few E2E. Invert it (mostly slow E2E) and CI becomes unusable.

---

## Core

### Unit testing (JUnit 5) + Mockito — ★★★★★ · Foundation · 1 day
- **What exactly:** JUnit 5 (`@Test`, parameterized, lifecycle, assertions, `assertThrows`), Mockito (`mock`/`when`/`verify`, argument captors, `@Mock`/`@InjectMocks`), test naming, AAA (arrange-act-assert), what to mock (collaborators) vs not (value objects).
- **Interview Qs:** "what makes a good unit test?" (fast, isolated, deterministic); "when do you *not* mock?"; "how do you test exception paths?"
- **Red flags:** testing implementation not behavior; over-mocking; flaky/order-dependent tests; no assertions.

### Integration testing + Testcontainers — ★★★★☆ · Intermediate · 2 days
- **Why:** mocks/H2 hide real DB behavior; Testcontainers spins up the *actual* dependency.
- **What exactly:** `@SpringBootTest` vs slices (`@DataJpaTest`, `@WebMvcTest`), `MockMvc`/`RestTestClient`, **Testcontainers** for Postgres/Kafka/Redis, test data setup/teardown, transactional test rollback.
- **Interview Qs:** "why Testcontainers over an embedded H2?"; "unit vs integration boundary?"
- **Related:** [Spring testing](3_spring_and_spring_boot.md).

### Contract testing — ★★★☆☆ · Intermediate · 0.5 day
- **What exactly:** consumer-driven contracts (Pact/Spring Cloud Contract) so microservices evolve safely.
- **Interview Qs:** "how do you stop a provider change from breaking consumers?"

### Load / performance testing — ★★★☆☆ · Intermediate · 0.5 day
- **What exactly:** k6/Gatling/JMeter, throughput vs latency, finding the knee, validating scale claims before prod.
- **Related:** [Performance](10_performance_profiling_reliability.md).

### Quality gates — ★★★★☆ · Foundation · 0.5 day
- **What exactly:** coverage (as a signal, not a target), static analysis (SonarQube/SpotBugs), linting/formatting, code review discipline, mutation testing (awareness).
- **Red flags:** chasing 100% coverage; treating coverage as quality.

## Approach (not a gate)
- **TDD — ★★☆☆☆:** useful discipline for well-specified logic; know the red-green-refactor loop; don't dogmatize.

## Legacy (stub) — ★☆☆☆☆
> **Why low priority:** superseded. **Learn only:** recognize it. **JUnit 4** (`@RunWith`, `@Before`) → use JUnit 5 Jupiter.

---

## Hands-on labs & failure scenarios

- **Lab 1:** unit-test a service with Mockito (mock the repo, verify interactions, test the exception path).
- **Lab 2:** integration-test the JPA layer against real Postgres via Testcontainers; assert real SQL behavior.
- **Lab 3:** add a k6 load test hitting your endpoint; find the throughput knee.
- **Failure scenario:** a flaky test fails 1/10 runs in CI — diagnose (shared state / time / ordering) and fix.
- **Debugging task:** a test passes on H2 but the query fails on Postgres — reproduce with Testcontainers.

---

## Checklists

### Interview Checklist
- **Must know:** test pyramid; good unit test properties; Mockito verify/capture; slice vs full Spring tests; Testcontainers rationale.
- **Good to know:** contract testing; load testing basics; coverage as signal.
- **Bonus:** mutation testing; consumer-driven contracts in CI.

### Production Checklist
- **Must know:** fast deterministic unit tests; integration tests on real deps; tests in CI gate merges.
- **Good to know:** flaky-test quarantine; load tests before scale events.

### Hands-on Checklist
- **Must:** wrote Mockito unit tests + a Testcontainers integration test.
- **Good:** added a load test; fixed a flaky test.
- **Bonus:** wired contract tests.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above; **(Legacy)** = recognize only.

**1. Fundamentals**
- Purpose of testing; functional vs non-functional; the testing pyramid (and anti-patterns: ice-cream cone)

**2. Unit testing**
- JUnit 5 (lifecycle, assertions, parameterized, nested); JUnit 4 **(Legacy)**
- Mockito (mocks, stubs, spies, argument captors); test doubles distinctions
- Code coverage (JaCoCo) — and why coverage % is not quality

**3. Integration testing**
- `@SpringBootTest` + slices; MockMvc / `WebTestClient`
- **Testcontainers** for real DB / Kafka / Redis (2026 default); DB integration testing
- API testing: RestAssured, Postman

**4. Contract & E2E testing**
- Contract testing (Pact / Spring Cloud Contract) for microservices
- E2E: Selenium/Cypress (mostly out of backend scope — awareness)

**5. Performance & load testing**
- Tools: k6 (modern), Gatling, JMeter, Locust
- Load vs stress vs spike vs soak testing; interpreting results → see [Performance](10_performance_profiling_reliability.md)

**6. CI/CD & quality gates**
- Running tests in pipelines; regression testing; test reporting
- Static analysis (SonarQube, SpotBugs, Checkstyle); code review; quality gates → see [Build & Tooling](12_build_tooling.md)

**7. Practices**
- Shift-left testing; TDD; BDD (awareness); flaky-test management; deterministic tests

**8. Interview**
- Mocks vs stubs vs spies; testing microservices with dependencies; testing strategy in CI/CD; what to unit- vs integration-test

---

**Nav:** [◀ Observability](8_observability_monitoring_logging.md) · [Next ▶ Performance & Reliability](10_performance_profiling_reliability.md)
