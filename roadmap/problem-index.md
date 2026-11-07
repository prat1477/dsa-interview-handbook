# Problem Index

Curated **~60 problems** for senior interview preparation. Each problem earns its place
by teaching a **reusable pattern** — not by inflating a solved count.

**Legend:** `Planned` = in index only · `Learning` = doc exists, studying · `Comfortable` =
can re-solve timed · `Interview Ready` = strong recall + communication

Problem files live under [`problems/`](../problems/) and are **created as we study them** —
not upfront.

---

## Summary by area

| Area | Target | Planned | Completed | Doc path |
| --- | ---: | ---: | ---: | --- |
| Arrays | 4 | 4 | 1 | [A1](../problems/easy/best-time-buy-sell-stock.md) |
| HashMap / HashSet | 4 | 5 | 3 | [H0](../problems/easy/contains-duplicate.md), [H1](../problems/easy/two-sum.md), [H4](../problems/medium/subarray-sum-equals-k.md) |
| Strings | 3 | 3 | 1 | [S2](../problems/medium/longest-substring-without-repeating-characters.md) |
| Two Pointers | 4 | 4 | 0 | (sorted Two Sum only) |
| Sliding Window | 5 | 5 | 1 | [S2](../problems/medium/longest-substring-without-repeating-characters.md) |
| Prefix Sum | 2 | 2 | 1 | [PS2](../problems/medium/subarray-sum-equals-k.md) |
| Binary Search | 4 | 4 | 0 | — |
| Intervals | 3 | 3 | 0 | — |
| Stack / Monotonic Stack | 5 | 5 | 0 | — |
| Heap | 4 | 4 | 1 | [HP2](../problems/medium/top-k-frequent-elements.md) |
| Linked List | 4 | 4 | 0 | — |
| Trees / BST | 7 | 7 | 0 | — |
| Graphs / BFS / DFS | 6 | 6 | 0 | — |
| Topological Sort | 2 | 2 | 0 | — |
| Union Find | 2 | 2 | 0 | — |
| Trie | 2 | 2 | 0 | — |
| Backtracking | 3 | 3 | 0 | — |
| Greedy | 3 | 3 | 0 | — |
| Dynamic Programming | 5 | 5 | 0 | — |
| Bit Manipulation | 2 | 2 | 0 | — |
| **Total** | **~60** | **73** | **6** | — |

> Count may trim slightly as we merge cosmetic duplicates during study.

---

## Phase 1 — Foundations

### Arrays (4)

| # | Problem | Difficulty | Pattern | Status | Notes |
| --- | --- | --- | --- | --- | --- |
| A1 | Best Time to Buy and Sell Stock | Easy | One pass / min tracking | Comfortable | [doc](../problems/easy/best-time-buy-sell-stock.md) |
| A2 | Product of Array Except Self | Medium | Prefix/suffix or two passes | Planned | No division constraint |
| A3 | Maximum Subarray | Medium | Kadane / DP flavor | Planned | Classic invariant |
| A4 | Merge Intervals (array form) | Medium | Sort + merge | Planned | Bridges to intervals |

### HashMap / HashSet (4+)

| # | Problem | Difficulty | Pattern | Status |
| --- | --- | --- | --- | --- |
| H0 | Contains Duplicate | Easy | HashSet membership | Comfortable |
| H1 | Two Sum | Easy | Hash complement | Comfortable |
| H2 | Group Anagrams | Medium | Hash by key | Planned |
| H3 | Longest Consecutive Sequence | Medium | Hash set + chain | Planned |
| H4 | Subarray Sum Equals K | Medium | Prefix sum + hash | Learning |

### Strings (3)

| # | Problem | Difficulty | Pattern | Status |
| --- | --- | --- | --- | --- |
| S1 | Valid Anagram | Easy | Frequency count | Planned |
| S2 | Longest Substring Without Repeating Characters | Medium | Sliding window | Comfortable |
| S3 | Minimum Window Substring | Hard | Sliding window + hash | Planned |

---

## Phase 2 — High-ROI Patterns

### Two Pointers (4)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| TP1 | Valid Palindrome | Easy | Planned |
| TP2 | 3Sum | Medium | Planned |
| TP3 | Container With Most Water | Medium | Planned |
| TP4 | Trapping Rain Water | Hard | Planned |

### Sliding Window (5)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| SW1 | Maximum Average Subarray I | Easy | Planned |
| SW2 | Longest Repeating Character Replacement | Medium | Planned |
| SW3 | Permutation in String | Medium | Planned |
| SW4 | Sliding Window Maximum | Hard | Planned |
| SW5 | Minimum Size Subarray Sum | Medium | Planned |

### Prefix Sum (2)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| PS1 | Range Sum Query — Immutable | Easy | Planned |
| PS2 | Subarray Sum Equals K | Medium | Learning | [doc](../problems/medium/subarray-sum-equals-k.md) *(also H4)* |

### Binary Search (4)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| BS1 | Binary Search | Easy | Planned |
| BS2 | Search in Rotated Sorted Array | Medium | Planned |
| BS3 | Find Minimum in Rotated Sorted Array | Medium | Planned |
| BS4 | Koko Eating Bananas | Medium | Planned |

### Intervals (3)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| IV1 | Merge Intervals | Medium | Planned |
| IV2 | Insert Interval | Medium | Planned |
| IV3 | Non-overlapping Intervals | Medium | Planned |

### Stack / Monotonic Stack (5)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| ST1 | Valid Parentheses | Easy | Planned |
| ST2 | Daily Temperatures | Medium | Planned |
| ST3 | Largest Rectangle in Histogram | Hard | Planned |
| ST4 | Evaluate Reverse Polish Notation | Medium | Planned |
| ST5 | Min Stack | Medium | Planned |

### Heap (4)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| HP1 | Kth Largest Element in an Array | Medium | Planned |
| HP2 | Top K Frequent Elements | Medium | Comfortable |
| HP3 | Merge k Sorted Lists | Hard | Planned |
| HP4 | Find Median from Data Stream | Hard | Planned |

---

## Phase 3 — Core Data Structures

### Linked List (4)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| LL1 | Reverse Linked List | Easy | Planned |
| LL2 | Linked List Cycle | Easy | Planned |
| LL3 | Merge Two Sorted Lists | Easy | Planned |
| LL4 | Reorder List | Medium | Planned |

### Trees / BST (7)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| T1 | Maximum Depth of Binary Tree | Easy | Planned |
| T2 | Validate Binary Search Tree | Medium | Planned |
| T3 | Lowest Common Ancestor of BST | Medium | Planned |
| T4 | Binary Tree Level Order Traversal | Medium | Planned |
| T5 | Serialize and Deserialize Binary Tree | Hard | Planned |
| T6 | Construct Binary Tree from Preorder and Inorder | Medium | Planned |
| T7 | Kth Smallest Element in BST | Medium | Planned |

### Graphs / BFS / DFS (6)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| G1 | Number of Islands | Medium | Planned |
| G2 | Clone Graph | Medium | Planned |
| G3 | Course Schedule | Medium | Planned |
| G4 | Pacific Atlantic Water Flow | Medium | Planned |
| G5 | Word Search | Medium | Planned |
| G6 | Rotting Oranges | Medium | Planned |

---

## Phase 4 — Advanced Structures

### Topological Sort (2)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| TS1 | Course Schedule II | Medium | Planned |
| TS2 | Alien Dictionary | Hard | Planned |

### Union Find (2)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| UF1 | Number of Connected Components | Medium | Planned |
| UF2 | Redundant Connection | Medium | Planned |

### Trie (2)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| TR1 | Implement Trie | Medium | Planned |
| TR2 | Word Search II | Hard | Planned |

### Shortest Path (included in graphs phase)

Covered by G3, G6, and dedicated shortest-path doc problems as needed.

---

## Phase 5 — Techniques

### Backtracking (3)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| BT1 | Subsets | Medium | Planned |
| BT2 | Combination Sum | Medium | Planned |
| BT3 | Word Search | Medium | Planned | *(also G5)* |

### Greedy (3)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| GR1 | Jump Game | Medium | Planned |
| GR2 | Merge Intervals (greedy view) | Medium | Planned |
| GR3 | Task Scheduler | Medium | Planned |

### Dynamic Programming (5)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| DP1 | Climbing Stairs | Easy | Planned |
| DP2 | House Robber | Medium | Planned |
| DP3 | Coin Change | Medium | Planned |
| DP4 | Longest Increasing Subsequence | Medium | Planned |
| DP5 | Edit Distance | Medium | Planned |

### Bit Manipulation (2)

| # | Problem | Difficulty | Status |
| --- | --- | --- | --- |
| BM1 | Single Number | Easy | Planned |
| BM2 | Number of 1 Bits | Easy | Planned |

---

## Selection criteria (reminder)

Each problem must satisfy at least two of:

- High frequency in senior backend / data platform interviews
- Teaches a pattern with multiple variations
- Clear difficulty progression (easy → medium → hard when useful)
- Senior relevance: trade-offs, correctness, clean structure

**Avoid:** obscure math tricks, cosmetic duplicates, pure competitive programming.

---

## Next problems to add (when ready)

Do **not** restart Big-O or re-solve the five documented problems unless revising.

Recommended next (new pattern depth — two pointers):

1. **TP3** — Container With Most Water
2. **TP2** — 3Sum

Then continue the senior shortlist as time allows: `#56` Merge Intervals, `#146` LRU Cache, `#23` Merge K Sorted Lists.
