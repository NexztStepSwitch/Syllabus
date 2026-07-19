# 12 — Build & Tooling

> **Module rating:** ★★★☆☆ (Situational depth; Git is Mandatory) · **Difficulty:** Foundation · **Est. effort:** 2–3 days · **Depth target:** Production
> **Prerequisites:** none.
> **Nav:** [◀ DevOps/CI/CD/Cloud](11_devops_cicd_cloud.md) · [Next ▶ Data Engineering](13_data_engineering_big_data.md) · **Related:** [Testing](9_testing_quality.md), [DevOps CI/CD](11_devops_cicd_cloud.md)

---

## Why this module

Tooling is table stakes: interviewers assume fluency and only notice its *absence*. Git is ★★★★★ because collaboration breaks without it; build tools are ★★★★☆ (know your own project cold); IDE mastery is a quiet productivity multiplier. Keep this module tight — don't over-study.

---

## Core

### Git — ★★★★★ · Foundation · 1 day
- **What exactly:** branching models (trunk-based/GitHub flow), merge vs **rebase** (and when each), interactive rebase/squash, resolving conflicts, `cherry-pick`, `bisect` (find the breaking commit), reflog (recover lost commits), good PRs + commit hygiene.
- **Interview Qs:** "merge vs rebase — when?"; "how do you find which commit introduced a bug?" (`git bisect`); "you committed to the wrong branch — recover?"
- **Red flags:** force-pushing shared branches; giant unfocused PRs; committing secrets.

### Build tools (Maven / Gradle) — ★★★★☆ · Foundation · 1 day
- **What exactly:** dependency management + transitive resolution, scopes, the build lifecycle, plugins, multi-module builds, dependency conflict resolution (`dependency:tree`), reproducible builds, BOM/version alignment. Gradle: incremental builds + build cache.
- **Interview Qs:** "how do you resolve a transitive dependency conflict?"; "Maven vs Gradle trade-offs?"
- **Red flags:** version drift; unpinned versions; ignoring dependency vulnerabilities.

### IDE & debugging — ★★★☆☆ · Foundation · 0.5 day
- **What exactly:** IntelliJ debugging (breakpoints, conditional/exception breakpoints, evaluate expression, remote debug), refactoring tools, profiling integration.
- **Related:** [Profiling](10_performance_profiling_reliability.md).

---

## Hands-on labs

- **Lab 1:** use `git bisect` to find a bug-introducing commit in a sample repo.
- **Lab 2:** resolve a real transitive dependency conflict with `dependency:tree`.
- **Lab 3:** set a conditional breakpoint and use "evaluate expression" to inspect state.

---

## Checklists

### Interview Checklist
- **Must know:** merge vs rebase; bisect; conflict resolution; reflog recovery; dependency conflict resolution.
- **Good to know:** Gradle build cache; multi-module builds; BOMs.

### Production Checklist
- **Must know:** pinned dependency versions; PR/commit hygiene; no secrets in Git.
- **Good to know:** dependency vulnerability scanning; reproducible builds.

### Hands-on Checklist
- **Must:** used bisect + interactive rebase; resolved a dependency conflict.
- **Good:** debugged with conditional breakpoints.
- **Bonus:** set up a multi-module build.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above; **(Legacy)** = recognize only.

**1. Build tools**
- Maven (lifecycle, POM, plugins); Gradle (tasks, Kotlin/Groovy DSL, build cache); Ant **(Legacy)**
- Choosing Maven vs Gradle

**2. Dependency management**
- Transitive dependencies; conflict resolution / dependency mediation; BOMs
- Versioning (SemVer); lockfiles; vulnerability scanning (OWASP Dependency-Check)

**3. Packaging & deployment**
- JAR / WAR / EAR **(EAR Legacy)**; fat/uber jars; Docker images; artifact repos (Nexus, Artifactory)

**4. Version control (Git)**
- Branching models; merge vs rebase; interactive rebase; `git bisect`; cherry-pick; resolving conflicts; PR hygiene

**5. Code quality tools**
- Static analysis (SonarQube, PMD, SpotBugs, Checkstyle); formatting/linting (Spotless); pre-commit hooks

**6. IDE & productivity**
- IntelliJ IDEA shortcuts; debugger (breakpoints, watches, evaluate, remote debug); profiler integration; Git integration

**7. Interview**
- Maven vs Gradle; how dependency resolution works; static vs dynamic analysis; how you'd debug with the IDE

---

**Nav:** [◀ DevOps/CI/CD/Cloud](11_devops_cicd_cloud.md) · [Next ▶ Data Engineering](13_data_engineering_big_data.md)
