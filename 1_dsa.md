# 1 — Data Structures & Algorithms

> **Module rating:** ★★★★★ (Mandatory) · **Difficulty:** Foundation → Advanced · **Est. effort:** 3–5 weeks (ongoing) · **Depth target:** Interview level
> **Prerequisites:** basic programming, one language fluent (Java assumed).
> **Nav:** [◀ Overview](0_overview.md) · [Next ▶ Core Java](2_core_java.md) · **Related:** [System Design](4_system_design.md) (LLD), [Core Java](2_core_java.md) (Collections)

---

## Why this module (2026 framing)

DSA is a **gate, not the differentiator**. AI can produce most easy/medium solutions in seconds, so interviewers now grade *how you reason*: do you recognize the pattern in the first two minutes, narrate a clean approach, state complexity, and handle edge cases? In AI-allowed rounds (confirm format with the recruiter) the skill flips to *reviewing* generated code — you can only catch a wrong solution if you know the patterns yourself.

**So the goal is pattern fluency under time pressure, not exotic-algorithm coverage.** Master ~12 recurring patterns cold; treat competitive-only algorithms as stubs.

- **2 YOE:** solve mediums with hints.
- **3.5 YOE:** recognize pattern <2 min, code clean medium in ~20 min, explain trade-offs.
- **5+ YOE:** fluent on hard variants + can teach the pattern.

---

## Priority map

| Tier | Patterns / topics | Rating |
|------|-------------------|--------|
| Core (drill daily) | Arrays, Strings, Hashing, Two pointers, Sliding window, Binary search (+answer-space), Stack/Queue (+monotonic), Trees/BST, Graphs (BFS/DFS/topo/Union-Find/Dijkstra), Heaps/Top-K, Intervals, Greedy, DP (core) | ★★★★★ / ★★★★☆ |
| Useful | Tries, Backtracking, Bit manipulation, Linked list manipulation | ★★★☆☆ |
| Rare | Segment/Fenwick tree, advanced graphs (SCC, MST) | ★★☆☆☆ |
| Stub (competitive-only) | FFT, suffix trees/automata, Mo's algorithm, max-flow, heavy number theory, matrix exponentiation | ★☆☆☆☆ |

---

## The core patterns (deep template)

### Complexity analysis — ★★★★★ · Foundation · 2 h
- **Why:** every interview expects you to state and defend Big-O of time *and* space; wrong complexity claims are an instant red flag.
- **What exactly:** Big-O/Ω/Θ, amortized analysis (dynamic array, hashmap), recursion-stack space, common curves (O(1), log n, n, n log n, n², 2ⁿ).
- **How deeply:** Interview level — recite complexity for every solution reflexively.
- **Interview Qs:** "Why is your solution O(n log n)?" "Can you do it in O(n) space less?" "Amortized vs worst case for `ArrayList.add`?"
- **Red flags:** confusing average vs worst case; ignoring recursion stack in space; hand-waving "it's fast."
- **Misconception:** "O(n log n) is always worse than O(n)" — constants and cache behavior matter in practice.

### Arrays, Strings, Hashing — ★★★★★ · Foundation · 3 days
- **Why:** the substrate of most problems; hashing turns O(n²) into O(n).
- **What exactly:** prefix sums, frequency maps, in-place manipulation, string building (avoid `+` in loops → `StringBuilder`), set membership/dedup.
- **How deeply:** Interview level.
- **Interview Qs:** two-sum family, subarray sum = k, group anagrams, longest substring without repeats.
- **Production relevance:** dedup, counting, request aggregation.
- **Red flags:** mutating a collection while iterating; O(n) `contains` on a `List` instead of a `Set`.
- **Related:** [Core Java Collections](2_core_java.md).

### Two pointers & Sliding window — ★★★★★ · Foundation · 2 days
- **Why:** highest-frequency patterns for array/string subrange problems; convert brute force to O(n).
- **What exactly:** opposite-end pointers, fast/slow, variable/fixed windows, shrink-on-invalid.
- **Interview Qs:** min window substring, longest substring ≤ k distinct, container with most water, remove duplicates in place.
- **Red flags:** recomputing the window from scratch instead of incrementally updating.

### Binary search (+ answer-space search) — ★★★★★ · Intermediate · 2 days
- **Why:** disproportionately common, *especially in Indian product loops* (Swiggy, rotated-array reports). The powerful variant is "binary search on the answer."
- **What exactly:** first/last occurrence, floor/ceil, rotated sorted array, search on a monotonic predicate (min capacity/days/speed).
- **Interview Qs:** find min in rotated array (O(log n)), Koko eating bananas, split array largest sum, median of two sorted arrays.
- **Red flags:** off-by-one in `lo/hi/mid`; infinite loops from wrong boundary update; not proving the predicate is monotonic.
- **Misconception:** "binary search only works on sorted arrays" — it works on any monotonic answer space.

### Stacks, Queues, Monotonic structures — ★★★★☆ · Foundation · 2 days
- **Why:** parsing, next-greater-element, and window extremes.
- **What exactly:** balanced parentheses, monotonic stack (next greater/smaller), monotonic deque (sliding window max), expression eval.
- **Interview Qs:** valid parentheses, largest rectangle in histogram, sliding window maximum, daily temperatures.

### Trees & BST — ★★★★★ · Intermediate · 3 days
- **What exactly:** all traversals (recursive + iterative), BFS level-order, height/diameter, LCA, BST insert/delete/validate, serialize/deserialize.
- **Interview Qs:** LCA, validate BST, level-order zigzag, diameter, serialize a tree, kth smallest in BST.
- **Red flags:** recursion without base case; assuming a binary tree is a BST.

### Graphs — ★★★★★ · Intermediate → Advanced · 4 days
- **Why:** models dependencies, networks, scheduling — and shows up in both DSA and design.
- **What exactly:** adjacency list, BFS/DFS, connected components, cycle detection, topological sort (Kahn's), Union-Find (DSU with path compression), Dijkstra. Bellman-Ford/Floyd-Warshall = awareness.
- **Interview Qs:** number of islands, course schedule (topo), clone graph, network delay time (Dijkstra), accounts merge (DSU).
- **Red flags:** revisiting nodes (no visited set); using DFS recursion on huge graphs → stack overflow (prefer iterative/BFS).
- **Related:** [System Design consistent hashing](4_system_design.md), [Microservices](5_microservices_distributed_systems.md).

### Heaps / Top-K — ★★★★☆ · Intermediate · 1 day
- **Why:** streaming, ranking (incl. ranking AI outputs), scheduling — a 2026 staple.
- **Interview Qs:** top-K frequent, merge k sorted lists, find median from data stream, k closest points.

### Intervals & Greedy — ★★★★☆ · Intermediate · 2 days
- **Interview Qs:** merge intervals, insert interval, meeting rooms II, non-overlapping intervals, jump game.
- **Red flags:** forgetting to sort; greedy without proving the greedy choice is safe.

### Dynamic Programming (core) — ★★★★☆ · Advanced · 4–5 days
- **Why:** common in medium/hard rounds; the hardest to fake.
- **What exactly:** memoization → tabulation, 1D/2D DP, classic set: coin change, LIS, LCS, edit distance, house robber, 0/1 knapsack, word break. **Advanced (stub):** DP on trees, bitmask DP, digit DP.
- **How deeply:** Interview level for the classics; awareness for advanced.
- **Interview Qs:** the classics above + "define the state and transition out loud."
- **Red flags:** jumping to code before defining the state; exponential recursion without memoization.

### Useful but secondary
- **Tries — ★★★☆☆:** autocomplete, prefix search, word dictionaries.
- **Backtracking — ★★★☆☆:** permutations/combinations/subsets, N-Queens, word search. (Know the template; it's a controlled DFS.)
- **Bit manipulation — ★★★☆☆:** XOR tricks, set/clear/toggle, count bits, subsets via bitmask.
- **Linked lists — ★★★☆☆:** reversal, cycle detection (Floyd), merge, LRU (hashmap + DLL — bridges to [caching](4_system_design.md)).

---

## Low-ROI / Legacy (stub only)

> **Why low priority:** these appear almost exclusively in competitive programming, not product backend interviews.
>
> **Learn only these basics:** know the *name* and *one-line use case* so you can say "that's a segment-tree / max-flow problem" and move on.
>
> **Further reading:** CP-Algorithms, Competitive Programmer's Handbook — only if you also do contests.

Topics: FFT, suffix trees/automata, Mo's algorithm, Ford-Fulkerson/Edmonds-Karp (max-flow), Miller-Rabin, matrix exponentiation, heavy combinatorics.

---

## Hands-on labs & exercises

- **Lab 1 (pattern drill):** solve 3 problems/day rotating through the core patterns for 3 weeks (~60 problems). Track pattern → problem in a sheet.
- **Lab 2 (timed):** 45-min mock: one medium coded clean + complexity stated out loud.
- **Debugging task:** take an AI-generated solution to a medium, find the bug/edge case before running it (mirrors AI-allowed rounds).
- **Failure scenario:** your recursive DFS stack-overflows on a 10⁶-node graph in prod — rewrite iteratively.

---

## Checklists

### Interview Checklist
- **Must know:** complexity analysis; two pointers; sliding window; binary search + answer-space; hashing; BFS/DFS; topo sort; Union-Find; heaps/top-K; trees/BST; intervals; core DP.
- **Good to know:** tries, backtracking template, bit tricks, monotonic stack/deque, Dijkstra.
- **Bonus:** segment/Fenwick tree, MST, SCC.

### Production Checklist
- **Must know:** choose the right collection ([Core Java](2_core_java.md)); avoid accidental O(n²); bound memory on large inputs.
- **Good to know:** streaming top-K; when to precompute vs compute on read.

### Hands-on Checklist
- **Must:** 60+ pattern-tagged problems solved; can code LRU cache from scratch.
- **Good:** 3 timed mocks passed; reviewed 10 AI-generated solutions for bugs.
- **Bonus:** a contest or two for speed.

---

## Detailed Syllabus (topic checklist)

> Full topic inventory for reference. Priorities/depth are in the guide above; competitive-only items are marked **(low ROI)** — know the name, skip deep study.

**1. Foundations**
- Math basics: logarithms, exponents; time & space complexity
- Big-O / Big-Ω / Big-Θ; amortized analysis
- Paradigms: brute force, divide & conquer, greedy, DP, backtracking, recursion vs iteration

**2. Complexity analysis**
- Time: constant, linear, log, quadratic, polynomial, exponential
- Space: allocation, recursion stack
- Best/worst/average case; practical factors (cache, branch prediction)

**3. Arrays & Strings**
- Arrays: traversal/insert/delete, prefix sums, sliding window, two pointers
- Strings: reversal/rotation/substring search; pattern matching — naïve, KMP, Rabin-Karp, Z (KMP/Z = low ROI); string hashing; tries

**4. Linked lists**
- Singly / doubly / circular; reversal; Floyd cycle detection; LRU cache (hashmap + DLL)

**5. Stacks & Queues**
- Stack apps: balanced parentheses, expression evaluation, call stack
- Queue: simple/circular, deque, priority queue
- Monotonic stack/queue; blocking queue

**6. Hashing**
- Hash functions; collision resolution (chaining, open addressing)
- Apps: hashmap/hashset, frequency counting, subarray-sum, caching

**7. Recursion & Backtracking**
- Tail vs non-tail; recursion-tree tracing
- N-Queens, Sudoku solver, rat-in-a-maze, word search

**8. Sorting**
- Basic: bubble/insertion/selection (O(n²)); efficient: merge/quick/heap (O(n log n))
- Specialized: counting/radix/bucket; stable vs unstable; library sorts

**9. Searching**
- Linear; binary search + variants (first/last occurrence, floor/ceil); rotated sorted array; exponential; ternary search (low ROI)

**10. Trees**
- Binary tree: traversals (in/pre/post/level), height, diameter, serialize/deserialize
- BST: insert/delete/search, balanced BST
- Heaps: min/max, heapify, heap sort
- AVL / Red-Black (awareness); Segment tree / Fenwick tree (low ROI)

**11. Graphs**
- Representation: adjacency matrix/list
- Traversal: BFS/DFS; connected components, cycle detection, bipartite check
- Shortest path: Dijkstra (Bellman-Ford / Floyd-Warshall = awareness)
- MST: Kruskal / Prim; topological sort (Kahn's); Union-Find (DSU); SCC — Kosaraju/Tarjan (low ROI)

**12. Dynamic Programming**
- Memoization vs tabulation; overlapping subproblems / optimal substructure
- Classics: 0/1 & unbounded knapsack, coin change, LIS, LCS, edit distance, house robber, word break
- Advanced (low ROI): DP on trees, bitmask DP, digit DP, matrix-chain multiplication

**13. Greedy**
- Activity selection, interval scheduling, job sequencing, fractional knapsack, Huffman coding

**14. Bit manipulation**
- AND/OR/XOR/NOT/shift; even-odd, power-of-two, count set bits, swap without temp
- Subset generation, bitmask DP, fast exponentiation

**15. Math algorithms (mostly low ROI)**
- Number theory: GCD/LCM, modular arithmetic, modular exponentiation, extended Euclid
- Primes: Sieve of Eratosthenes; Miller-Rabin **(low ROI)**
- Combinatorics: nCr, factorials, Pascal's triangle
- Matrix exponentiation, FFT **(low ROI, competitive-only)**

**16. Advanced (low ROI, competitive-only)**
- Suffix arrays / suffix trees; max-flow / min-cut (Ford-Fulkerson, Edmonds-Karp); sparse table; Mo's algorithm

**17. Practice & problem solving**
- Platforms: LeetCode (primary), Codeforces, HackerRank, GeeksforGeeks
- Patterns: sliding window, two pointers, fast/slow pointers, recursion→iteration
- Mock: time-bound coding, contest-style problem solving

---

**Nav:** [◀ Overview](0_overview.md) · [Next ▶ Core Java](2_core_java.md)
