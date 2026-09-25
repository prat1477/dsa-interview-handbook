# Progress Tracker

Mastery levels: **Not Started** → **Learning** → **Practicing** → **Comfortable** → **Interview Ready**

> Solving a problem once does **not** mean Interview Ready. Use spaced repetition in
> [`revision-log.md`](revision-log.md).

**Last updated:** 2026-09-07

---

## Overall

| Metric | Value |
| --- | --- |
| Problems with docs | 5 / ~60 |
| Problems Interview Ready | 0 |
| Current phase | Phase 2 — Two Pointers next |
| Current module | High-ROI patterns (window, heap started) |
| Weekly DSA budget | 1.5–3 hours |

---

## Phase progress

| Phase | Topics | Confidence | Last activity |
| --- | --- | --- | --- |
| 1 — Foundations | Complexity, Arrays, Strings, HashMap | Practicing | 2026-09-07 |
| 2 — High-ROI patterns | Two pointers, window, heap started | Learning | 2026-09-07 |
| 3 — Core structures | Linked list, trees, DFS/BFS | Not Started | — |
| 4 — Advanced structures | Graphs, topo, UF, trie | Not Started | — |
| 5 — Techniques | Backtracking, greedy, DP, bits | Not Started | — |
| 6 — Interview mode | Mixed, timed, mocks | Not Started | — |

---

## Topic detail

| Topic | Document | Problems done | Recalled | Confidence | Last revision | Weak areas |
| --- | --- | ---: | ---: | --- | --- | --- |
| Complexity | [`complexity.md`](../fundamentals/complexity.md) | — | — | Learning | 2026-08-22 | Formal proofs; amortized |
| Arrays | [`arrays.md`](../fundamentals/arrays.md) | 1/4 | 0 | Practicing | 2026-09-07 | Confusing max price vs max profit |
| Strings | [`strings.md`](../fundamentals/strings.md) | 1/3 | 0 | Learning | 2026-09-07 | Substring vs subsequence |
| HashMap / HashSet | [`hashmap-hashset.md`](../patterns/hashmap-hashset.md) | 2/4 | 0 | Practicing | 2026-09-07 | Put-before-lookup on Two Sum |
| Two Pointers | [`two-pointers.md`](../patterns/two-pointers.md) | 0/4 | 0 | Learning | 2026-09-07 | Only as Two Sum alternative |
| Sliding Window | [`sliding-window.md`](../patterns/sliding-window.md) | 1/5 | 0 | Learning | 2026-09-07 | `if` vs `while`; remove vs left++ order |
| Prefix Sum | [`prefix-sum.md`](../patterns/prefix-sum.md) | 0/2 | 0 | Not Started | — | — |
| Binary Search | [`binary-search.md`](../patterns/binary-search.md) | 0/4 | 0 | Not Started | — | — |
| Intervals | [`intervals.md`](../patterns/intervals.md) | 0/3 | 0 | Not Started | — | — |
| Stack | [`stack.md`](../patterns/stack.md) | 0/5 | 0 | Not Started | — | — |
| Heap | [`heap-priority-queue.md`](../patterns/heap-priority-queue.md) | 1/4 | 0 | Learning | 2026-09-07 | PQ does not auto-cap; heap vs sort when k≈u |
| Linked List | [`linked-list.md`](../data-structures/linked-list.md) | 0/4 | 0 | Not Started | — | — |
| Fast/Slow Pointers | [`fast-slow-pointers.md`](../patterns/fast-slow-pointers.md) | 0/2 | 0 | Not Started | — | — |
| Trees / BST | [`trees.md`](../data-structures/trees.md) | 0/7 | 0 | Not Started | — | — |
| Graphs | [`graphs.md`](../data-structures/graphs.md) | 0/6 | 0 | Not Started | — | — |
| Topological Sort | [`topological-sort.md`](../algorithms/topological-sort.md) | 0/2 | 0 | Not Started | — | — |
| Union Find | [`union-find.md`](../data-structures/union-find.md) | 0/2 | 0 | Not Started | — | — |
| Trie | [`trie.md`](../data-structures/trie.md) | 0/2 | 0 | Not Started | — | — |
| DFS / BFS | [`dfs-bfs.md`](../algorithms/dfs-bfs.md) | 0/6 | 0 | Not Started | — | — |
| Backtracking | [`backtracking.md`](../algorithms/backtracking.md) | 0/3 | 0 | Not Started | — | — |
| Greedy | [`greedy.md`](../patterns/greedy.md) | 0/3 | 0 | Not Started | — | — |
| Dynamic Programming | [`dynamic-programming.md`](../algorithms/dynamic-programming.md) | 0/5 | 0 | Not Started | — | — |
| Bit Manipulation | [`bit-manipulation.md`](../algorithms/bit-manipulation.md) | 0/2 | 0 | Not Started | — | — |
| Recursion | [`recursion.md`](../fundamentals/recursion.md) | — | — | Not Started | — | — |

---

## Documented problems

| ID | Problem | Pattern | Confidence |
| --- | --- | --- | --- |
| H0 | [Contains Duplicate](../problems/easy/contains-duplicate.md) | HashSet | Comfortable |
| H1 | [Two Sum](../problems/easy/two-sum.md) | HashMap / two pointers | Comfortable |
| A1 | [Best Time to Buy and Sell Stock](../problems/easy/best-time-buy-sell-stock.md) | State tracking | Comfortable |
| HP2 | [Top K Frequent Elements](../problems/medium/top-k-frequent-elements.md) | HashMap + min-heap | Comfortable |
| S2 | [Longest Substring Without Repeating Characters](../problems/medium/longest-substring-without-repeating-characters.md) | Sliding window | Comfortable |

Comfortable ≠ Interview Ready. Run Day 3/7 recall before upgrading.

---

## Mock interviews

| Session | Topic | Date | Score (/35) | Notes |
| --- | --- | --- | --- | --- |
| — | — | — | — | After two-pointers + a second window problem |

---

## Weak-area queue

1. Sliding window: shrink with `while`; remove character **then** `left++`
2. Two Sum: lookup complement **before** `put`
3. Stock: track max **profit**, not max price
4. Heap: `PriorityQueue` size is not automatically k; heap vs sort when k ≈ u
5. Complexity: nested loops can still be O(n) if pointers are monotonic; HashMap is O(1) **average**

---

## How to update

After each study session:

1. Set **Confidence** for the topic touched.
2. Increment **Problems done** when a problem doc exists and you've solved it independently.
3. Log **Recalled** when you pass a Day 3/7/21 recall drill.
4. Add **Weak areas** when you hesitate on pattern, invariant, or complexity.
