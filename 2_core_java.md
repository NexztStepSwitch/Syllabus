# 2 — Core Java (Java 21 LTS)

> **Module rating:** ★★★★★ (Mandatory) · **Difficulty:** Foundation → Advanced · **Est. effort:** 2–3 weeks · **Depth target:** Interview + Production
> **Baseline:** **Java 21 LTS** (the enterprise baseline). Legacy items clearly marked.
> **Prerequisites:** [DSA](1_dsa.md) basics.
> **Nav:** [◀ DSA](1_dsa.md) · [Next ▶ Spring & Spring Boot](3_spring_and_spring_boot.md) · **Related:** [Performance](10_performance_profiling_reliability.md), [System Design LLD](4_system_design.md)

---

## Why this module

Java is your working language and the medium for **LLD/machine-coding rounds**, which are heavily weighted at product/fintech companies (Razorpay/PhonePe/Swiggy). Interviewers probe **concurrency correctness**, **collections internals**, and increasingly **Java 21 virtual threads**. The modern language features (records, sealed, pattern matching) make LLD code cleaner and signal that you're current.

---

## Fundamentals (revise fast — don't linger)

> These are `Foundation`. Refresh, confirm you can use them cold, move on.

### OOP + SOLID — ★★★★★ · Foundation · 1 day
- **Why:** the backbone of every LLD round. You *will* draw class hierarchies.
- **What exactly:** encapsulation/abstraction/inheritance/polymorphism; SOLID with concrete violations + fixes; composition over inheritance.
- **Interview Qs:** "refactor this to open/closed"; "where does inheritance hurt here?"
- **Red flags:** God classes; inheritance for code reuse instead of composition.
- **Related:** [Design patterns](4_system_design.md).

### Collections framework — ★★★★★ · Foundation · 2 days
- **What exactly:** `ArrayList` vs `LinkedList`, `HashMap` internals (buckets, treeification at 8, resize/load factor), `ConcurrentHashMap`, `TreeMap`/`TreeSet`, `ArrayDeque`, comparator/comparable, iterator fail-fast.
- **How deeply:** Interview level — `HashMap` internals are a perennial question.
- **Interview Qs:** "how does `HashMap` handle collisions?"; "why is `ConcurrentHashMap` better than `synchronizedMap`?"; "when `ArrayDeque` over `Stack`/`LinkedList`?"
- **Red flags:** using `Stack`/`Vector` (Legacy); mutating keys' hashcodes; `List.contains` in a hot loop.
- **Misconception:** "`HashMap` is thread-safe" — it is not; concurrent writes can corrupt/infinite-loop (pre-8).

### Generics, Exceptions — ★★★★☆ · Foundation · 1 day
- **What exactly:** bounded wildcards (PECS), type erasure implications; checked vs unchecked, try-with-resources, exception translation, never swallow exceptions.
- **Red flags:** `catch (Exception e) {}`; using exceptions for control flow.

### Streams, Lambdas, Optional — ★★★★★ · Foundation · 2 days
- **What exactly:** map/filter/reduce, collectors (grouping/partitioning), `flatMap`, lazy evaluation, parallel streams (and when *not* to use them), `Optional` for return types (not fields/params).
- **Interview Qs:** "rewrite this loop as a stream"; "when is a parallel stream harmful?" (small data, shared state, ordered ops).
- **Red flags:** side effects inside `map`; `Optional.get()` without check; overusing parallel streams.

---

## Concurrency (the depth zone) — ★★★★★ · Advanced · 4 days

- **Why:** correctness under load is the #1 thing that separates 3.5-YOE from junior in code review and interviews; fintech weighs it heavily.
- **What exactly:**
  - Java Memory Model: `volatile` (visibility, not atomicity), happens-before, `final` safe publication.
  - Synchronization: `synchronized`, `ReentrantLock`, `ReadWriteLock`, `StampedLock`; deadlock/livelock/starvation.
  - Atomics: `AtomicInteger`, `LongAdder`, CAS.
  - Executors: `ExecutorService`, thread pools (sizing for CPU- vs I/O-bound), `CompletableFuture` composition, `CountDownLatch`/`Semaphore`/`CyclicBarrier`.
  - Concurrent collections: `ConcurrentHashMap`, `BlockingQueue`, `CopyOnWriteArrayList`.
- **How deeply:** Interview + Production.
- **Interview Qs:** "`volatile` vs `synchronized`?"; "how do you size a thread pool?"; "implement a bounded blocking queue"; "producer/consumer with backpressure."
- **Red flags:** assuming `volatile` makes `count++` atomic; unbounded thread pools; sharing mutable state without synchronization.
- **Misconception:** "more threads = faster" — context-switching + contention can slow you down.

## Virtual Threads (Java 21, JEP 444) — ★★★★☆ · Intermediate · 1 day

- **Why:** the biggest JVM concurrency shift since Java 8; a **production feature in Java 21** and a common 2026 interview topic.
- **What exactly:**
  - One virtual thread per task; JVM multiplexes millions onto a few carrier threads; you keep writing simple **blocking** code.
  - **Best for I/O-bound** work (DB, HTTP). **Not** for CPU-bound work → use a bounded pool sized to cores.
  - **Pinning:** `synchronized` around blocking I/O pins the carrier thread → replace with `ReentrantLock`. (Java 24+/JEP 491 largely removes this, but Java 21 LTS still needs it.) Detect with `-Djdk.tracePinnedThreads`.
  - **ThreadLocal** memory: millions of threads × ThreadLocal = memory blowup; prefer Scoped Values.
- **How deeply:** Production — can enable, avoid pinning, and reason about downstream limits.
- **Interview Qs:** "what problem do virtual threads solve?"; "why doesn't a virtual thread help CPU-bound code?"; "what is pinning and how do you avoid it?"; "do you still need connection pools?" (yes — sized to the DB, not the thread count).
- **Red flags:** claiming virtual threads make requests *faster* (they prevent *degradation under concurrency*); leaving `synchronized` I/O blocks; oversizing the DB pool.
- **Related:** [Spring virtual-thread enablement](3_spring_and_spring_boot.md), [Performance](10_performance_profiling_reliability.md).

## Modern language features — ★★★★☆ · Foundation → Intermediate · 1 day

- **Records — ★★★★☆:** immutable data carriers; perfect for DTOs/value objects; auto equals/hashcode/toString.
- **Sealed classes — ★★★☆☆:** restrict hierarchies; pair with pattern matching for exhaustive handling.
- **Pattern matching — ★★★☆☆:** `instanceof` patterns, switch patterns, record deconstruction — cleaner LLD.
- **Text blocks, `var`:** minor ergonomics.
- **Interview Qs:** "when a record vs a class?"; "how do sealed + switch give exhaustiveness?"

## Memory & GC — ★★★☆☆ · Advanced · 1 day

- **What exactly:** heap/stack/metaspace; generational GC; **G1 (default)**, **ZGC/Generational ZGC** for low pause; GC logs; heap dumps; common leaks (static collections, unclosed resources, ThreadLocals).
- **How deeply:** Production — read a GC log, spot a leak, pick a collector.
- **Interview Qs:** "how would you debug an OOM in prod?"; "G1 vs ZGC trade-offs?"; "what causes a memory leak in Java despite GC?"
- **Related:** [Performance profiling](10_performance_profiling_reliability.md).

## Preview / awareness only — ★★☆☆☆

- **Structured Concurrency (JEP 453, preview in 21):** treat concurrent subtasks as a unit; know the concept.
- **Scoped Values (preview):** immutable per-thread context, ThreadLocal replacement for virtual threads.
- **CRaC / GraalVM native image — ★☆☆☆☆ / ★★☆☆☆:** faster startup; situational (serverless, K8s scale-to-zero). Awareness.

## Legacy (stub) — ★☆☆☆☆

> **Why low priority:** obsolete or rarely asked.
> **Learn only:** recognize them.
> Applets, `Vector`/`Stack`/`Hashtable`, manual `Thread.stop/suspend`, finalizers, deep classloader trivia, Java Security Manager.

---

## Hands-on labs & failure scenarios

- **Lab 1:** implement a thread-safe bounded blocking queue with `ReentrantLock` + conditions; then with `ArrayBlockingQueue`.
- **Lab 2:** enable virtual threads in a small HTTP+JDBC app; run `-Djdk.tracePinnedThreads=full` under load; fix a `synchronized` pinning site.
- **Lab 3:** write an LLD (e.g. logger framework — a real Razorpay question) using records + sealed + patterns + a design pattern.
- **Debugging task:** given a GC log with rising old-gen after each cycle, identify the leak.
- **Failure scenario:** a shared `HashMap` under concurrent writes corrupts; reproduce and fix with `ConcurrentHashMap`.

---

## Checklists

### Interview Checklist
- **Must know:** OOP+SOLID; `HashMap`/`ConcurrentHashMap` internals; JMM (`volatile`/happens-before); executors + pool sizing; `CompletableFuture`; virtual threads + pinning; streams; records.
- **Good to know:** sealed + pattern matching; GC collectors; deadlock detection; `Optional` idioms.
- **Bonus:** structured concurrency; ZGC tuning; native image.

### Production Checklist
- **Must know:** avoid unbounded pools; size pools/connection pools correctly; no `synchronized` around I/O on virtual threads; close resources.
- **Good to know:** read GC logs + heap dumps; choose collections by access pattern.

### Hands-on Checklist
- **Must:** built a thread-safe structure; enabled + validated virtual threads; coded one LLD in modern Java.
- **Good:** diagnosed one leak; benchmarked a pool size.
- **Bonus:** compared G1 vs ZGC on a load test.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference (baseline **Java 21 LTS**). Priorities/depth are in the guide above; **(Legacy)** = recognize only; **(2026)** = modern addition.

**1. Java basics**
- JVM / JRE / JDK; WORA; program structure, compilation & execution
- Data types (primitive/reference); operators (arithmetic/logical/bitwise/ternary/`instanceof`)

**2. Control flow**
- if / if-else / switch (+ switch expressions & pattern matching **(2026)**)
- Loops: for / while / do-while / for-each; break / continue / return

**3. OOP**
- Class & objects; encapsulation (access modifiers); inheritance & overriding; polymorphism (overload/override); abstraction (abstract classes, interfaces w/ default & static methods)
- Composition vs inheritance; association / aggregation / composition; SOLID

**4. Memory management**
- Stack vs heap vs metaspace; object allocation & escape analysis
- Garbage collection: G1 (default), ZGC / Generational ZGC **(2026)**, Parallel, Serial; `finalize()` **(Legacy)**
- Memory leaks (static collections, ThreadLocals, unclosed resources)

**5. Strings & wrappers**
- String / StringBuilder / StringBuffer; string pool & interning; immutability
- Wrapper classes; autoboxing/unboxing

**6. Exception handling**
- Checked vs unchecked; Error vs Exception; try/catch/finally/throw/throws; try-with-resources
- Custom exceptions; exception translation; never swallow exceptions

**7. Collections framework**
- Interfaces: List, Set, Queue, Map
- Impl: ArrayList / LinkedList, HashSet / TreeSet / LinkedHashSet, HashMap / TreeMap / LinkedHashMap, ArrayDeque, PriorityQueue
- HashMap internals (buckets, treeify, resize); Comparable vs Comparator; fail-fast vs fail-safe
- Concurrent: ConcurrentHashMap, CopyOnWriteArrayList; `Vector`/`Stack`/`Hashtable` **(Legacy)**

**8. Generics**
- Generic classes/methods; bounded types; wildcards (`?`, `? extends`, `? super`, PECS); type erasure

**9. Multithreading & concurrency**
- Thread lifecycle; Runnable/Callable; `Thread.stop/suspend` **(Legacy)**
- Synchronization (`synchronized`, monitors); `wait/notify/notifyAll`
- Java Memory Model: `volatile`, happens-before, safe publication
- Executors (ThreadPoolExecutor, sizing), `CompletableFuture`, Future
- Locks (ReentrantLock, ReadWriteLock, StampedLock); Semaphore, CountDownLatch, CyclicBarrier
- Atomics / CAS (`AtomicInteger`, `LongAdder`); Fork/Join
- **Virtual Threads (JEP 444)** + pinning, `ReentrantLock` over `synchronized` on I/O **(2026)**

**10. Java I/O**
- Byte vs character streams; File I/O; Buffered I/O; NIO (channels/buffers, Path & Files); serialization (`Serializable`, `Externalizable` — use sparingly)

**11. Functional / Java 8+**
- Functional interfaces; lambdas; Streams (intermediate/terminal, map/filter/reduce, collectors); parallel streams (careful); Optional; default/static interface methods; Date/Time API (LocalDate/Time, ZonedDateTime, Duration/Period)

**12. Modern language features**
- `var` (Java 10); Records (16); Sealed classes (17); Pattern matching for `instanceof` & `switch`, record patterns (21); text blocks
- Enums with behavior; annotations (built-in + custom); reflection (awareness); inner/anonymous classes

**13. JVM internals**
- Architecture: classloader subsystem, runtime data areas, execution engine
- Class loading (load/link/init); classloader types (deep trivia = **Legacy**); JIT; basic tuning flags

**14. Preview / emerging (2026, awareness)**
- Structured Concurrency (JEP 453, preview); Scoped Values (preview); CRaC; GraalVM native image

**15. Best practices**
- Effective Java principles; immutability; thread-safety; SOLID in Java; coding standards

**16. Testing & tooling (cross-links)**
- JUnit 5, Mockito, Testcontainers → see [Testing](9_testing_quality.md)
- Maven/Gradle, IntelliJ, SonarLint/Checkstyle, SLF4J/Logback → see [Build & Tooling](12_build_tooling.md)

---

**Nav:** [◀ DSA](1_dsa.md) · [Next ▶ Spring & Spring Boot](3_spring_and_spring_boot.md)
