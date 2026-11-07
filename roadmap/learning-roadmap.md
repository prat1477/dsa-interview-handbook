# Learning Roadmap

The phased learning order for this handbook. Progress is tracked in
[`progress/progress.md`](../progress/progress.md); planned problems in
[`problem-index.md`](problem-index.md).

> **Pace.** ~2–3 hours per week. Consistency beats volume. Skip ahead only when a
> phase is genuinely comfortable — not when problems were solved once.

## Phase 1 — Foundations

| Order | Topic | Document | Status |
| --- | --- | --- | --- |
| 1 | Big-O / Complexity | [`fundamentals/complexity.md`](../fundamentals/complexity.md) | Learning |
| 2 | Arrays | [`fundamentals/arrays.md`](../fundamentals/arrays.md) | Practicing |
| 3 | Strings | [`fundamentals/strings.md`](../fundamentals/strings.md) | Learning (via LC 3) |
| 4 | HashMap / HashSet | [`patterns/hashmap-hashset.md`](../patterns/hashmap-hashset.md) | Practicing |

**Exit criteria:** You can state time/space complexity confidently, walk through array
manipulation with correct edge-case thinking, and recognize when hashing helps.

---

## Phase 2 — High-ROI Patterns

| Order | Topic | Document | Status |
| --- | --- | --- | --- |
| 5 | Two Pointers | [`patterns/two-pointers.md`](../patterns/two-pointers.md) | Learning (Two Sum alternative only) |
| 6 | Sliding Window | [`patterns/sliding-window.md`](../patterns/sliding-window.md) | Learning |
| 7 | Prefix Sum | [`patterns/prefix-sum.md`](../patterns/prefix-sum.md) | Learning (via [PS2](../problems/medium/subarray-sum-equals-k.md)) |
| 8 | Binary Search | [`patterns/binary-search.md`](../patterns/binary-search.md) | Not Started |
| 9 | Intervals | [`patterns/intervals.md`](../patterns/intervals.md) | Not Started |
| 10 | Stack | [`patterns/stack.md`](../patterns/stack.md) | Not Started |
| 11 | Monotonic Stack | [`patterns/monotonic-stack.md`](../patterns/monotonic-stack.md) | Not Started |
| 12 | Heap / Priority Queue | [`patterns/heap-priority-queue.md`](../patterns/heap-priority-queue.md) | Learning |

**Exit criteria:** For a new medium problem, you can name 2–3 candidate patterns within
two minutes and justify why one fits.

---

## Phase 3 — Core Data Structures

| Order | Topic | Document |
| --- | --- | --- |
| 13 | Linked List | [`data-structures/linked-list.md`](../data-structures/linked-list.md) |
| 14 | Fast & Slow Pointers | [`patterns/fast-slow-pointers.md`](../patterns/fast-slow-pointers.md) |
| 15 | Trees | [`data-structures/trees.md`](../data-structures/trees.md) |
| 16 | BST | [`data-structures/bst.md`](../data-structures/bst.md) |
| 17 | DFS | [`algorithms/dfs-bfs.md`](../algorithms/dfs-bfs.md) |
| 18 | BFS | [`algorithms/dfs-bfs.md`](../algorithms/dfs-bfs.md) |

---

## Phase 4 — Advanced Structures

| Order | Topic | Document |
| --- | --- | --- |
| 19 | Graphs | [`data-structures/graphs.md`](../data-structures/graphs.md) |
| 20 | Topological Sort | [`algorithms/topological-sort.md`](../algorithms/topological-sort.md) |
| 21 | Union Find | [`data-structures/union-find.md`](../data-structures/union-find.md) |
| 22 | Trie | [`data-structures/trie.md`](../data-structures/trie.md) |
| 23 | Shortest Path | [`algorithms/shortest-path.md`](../algorithms/shortest-path.md) |

---

## Phase 5 — Problem-Solving Techniques

| Order | Topic | Document |
| --- | --- | --- |
| 24 | Backtracking | [`algorithms/backtracking.md`](../algorithms/backtracking.md) |
| 25 | Greedy | [`patterns/greedy.md`](../patterns/greedy.md) |
| 26 | Dynamic Programming | [`algorithms/dynamic-programming.md`](../algorithms/dynamic-programming.md) |
| 27 | Bit Manipulation | [`algorithms/bit-manipulation.md`](../algorithms/bit-manipulation.md) |

---

## Phase 6 — Interview Mode

| Order | Activity | Location |
| --- | --- | --- |
| 28 | Mixed problems | [`problems/`](../problems/) |
| 29 | Timed problems | Same + revision log |
| 30 | Mock interviews | [`mock-interviews/`](../mock-interviews/) |
| 31 | Revision | [`revision/`](../revision/) |
| 32 | Weak-area targeting | [`progress/progress.md`](../progress/progress.md) |

---

## Weekly rhythm (repeat each week)

```text
Session 1 (30–40 min) → Learn / revise one pattern
Session 2 (30–40 min) → Solve one problem independently
Session 3 (30–40 min) → Related variation or recall drill
Optional weekend     → Timed problem or cheatsheet review
```

## Spaced repetition (per problem)

After learning a problem, schedule:

| Day | Activity |
| --- | --- |
| 0 | Learn fully |
| 3 | Recall (pattern, invariant, complexity) |
| 7 | Re-solve from scratch |
| 21 | Revisit — variation or follow-up |
| 45 | Interview-style timed attempt |

Not every revisit requires a full re-solve. Sometimes answer:

- What's the pattern?
- What's the invariant?
- What if input were sorted?
- What if memory were limited?
- What if data were streaming?

Log dates in [`progress/revision-log.md`](../progress/revision-log.md).

## Current focus

**Completed (documented):** Contains Duplicate, Two Sum, Best Time to Buy and Sell Stock, Top K Frequent Elements, Longest Substring Without Repeating Characters.

**You are here:** Phase 2 — make **two pointers** first-class (next problem: Container With Most Water or 3Sum). Sliding window and heap stay in Learning until a second problem each.

Do not restart Big-O or re-teach the five documented problems unless revision is requested.
