---
title: "Module 1 — Arrays"
description: Array fundamentals, operations, patterns preview, and interview thinking for sequential data.
status: draft
phase: 1
tags: [fundamentals, arrays]
created: 2026-08-22
updated: 2026-08-22
---

# Arrays

Arrays are the default substrate for most coding interviews — and for much of backend and
data-platform work (buffers, column batches, partition arrays). Master arrays before rushing
to exotic structures.

## Overview

An **array** is contiguous indexed storage: O(1) random access by index, O(n) insert/delete
in the middle without extra structure.

This module covers array mechanics, the patterns arrays unlock, recognition signals, and how
to prepare for the first curated problems — **without** jumping into full solutions yet.

**Prerequisite:** [Module 0 — Complexity](complexity.md)

## Learning objectives

After this module you should be able to:

- State time complexity of access, scan, insert, delete on static and dynamic arrays.
- Choose between in-place mutation and extra-space approaches.
- Recognize when an array problem is really a sorting, hashing, or two-pointer problem.
- Identify edge cases: empty, single element, duplicates, negative numbers, overflow.
- Explain why "one pass" and "prefix/suffix" appear constantly in array interviews.

---

## 1. What is an array (for interviews)?

**Fixed array (Java `int[]`):** length fixed at creation; O(1) index access.

**Dynamic array (`ArrayList`):** amortized O(1) append; O(n) insert at index i; occasional resize.

| Operation | Static array | ArrayList |
| --- | --- | --- |
| Access by index | O(1) | O(1) |
| Scan all elements | O(n) | O(n) |
| Append at end | N/A (fixed) | O(1) amortized |
| Insert at front/middle | O(n) shift | O(n) |
| Delete at front/middle | O(n) shift | O(n) |

**Interview implication:** Random access favors **two pointers** and **index math**. No random
access favors linked structures or streaming — but many problems still give arrays.

### Real engineering connection

- **Columnar batches** (Spark, Arrow) — contiguous memory, scan-friendly.
- **Ring buffers** in queues — array with head/tail indices.
- **Time-series windows** — array or deque backing sliding metrics.

---

## 2. Why arrays dominate interviews

1. **Simple interface** — interviewers can test logic without API trivia.
2. **Pattern gateway** — hashing, two pointers, sliding window, prefix sum, binary search on
   answers often start with an array input.
3. **In-place tricks** — swap, read/write pointers, overwrite unused tail — test careful thinking.

---

## 3. Recognition signals

Think **array fundamentals** or **array + pattern** when you see:

- "Given an integer array…"
- Subarray, subsequence (contiguous vs not — clarify!)
- Return indices, not just values
- In-place requirement with O(1) extra space
- "Find max/min/subarray sum/product"
- Sorted array or "can you sort?"

**Clarify contiguous vs subsequence** — contiguous subarray allows O(n) sliding window;
subsequence often needs DP or different structure.

---

## 4. When to use array techniques

- Input is naturally ordered by index.
- Need O(1) access to i and j simultaneously (two pointers).
- Can overwrite unused portions for O(1) space (e.g. Dutch flag, remove element).
- Prefix aggregates over ranges — prefix sum array.

---

## 5. When NOT to use (alone)

| Situation | Better approach |
| --- | --- |
| Frequent insert/delete at front | Deque, linked list |
| Need sorted order dynamically | TreeMap, heap, TreeSet |
| Fast lookup by value | HashMap / HashSet |
| All pairs / relationships | Graph, union-find |
| Optimal substructure over sequence | Dynamic programming |

---

## 6. Core templates

### One-pass scan (track best / running min)

```java
int best = Integer.MIN_VALUE;
int runningMin = Integer.MAX_VALUE;
for (int x : nums) {
    runningMin = Math.min(runningMin, x);
    best = Math.max(best, x - runningMin); // example: max profit
}
```

Use for: max subarray variants, buy/sell stock, running aggregates.

### Two indices (read/write or left/right)

```java
int write = 0;
for (int read = 0; read < nums.length; read++) {
    if (shouldKeep(nums[read])) {
        nums[write++] = nums[read];
    }
}
// new logical length = write
```

Use for: remove element in-place, partition, dedupe sorted array.

### Prefix / suffix accumulation

```java
int n = nums.length;
int[] prefix = new int[n + 1];
for (int i = 0; i < n; i++) {
    prefix[i + 1] = prefix[i] + nums[i];
}
// sum of nums[l..r] inclusive = prefix[r + 1] - prefix[l]
```

Use for: range sums, product except self (prefix + suffix), subarray sum equals k (with hash).

---

## 7. Complexity (typical)

| Technique | Time | Extra space |
| --- | --- | --- |
| Single scan | O(n) | O(1) |
| Sort then scan | O(n log n) | O(1) or O(n) |
| Prefix array | O(n) | O(n) |
| Hash + scan | O(n) | O(n) |
| Nested loops all pairs | O(n²) | O(1) |

Always reconcile with **n** in constraints.

---

## 8. Common variations

- **Sorted array** — two pointers from both ends; binary search.
- **Circular array** — modulo index `(i + 1) % n`.
- **2D matrix** — row-major; same patterns with `(r, c)` indices.
- **Almost sorted** — bubble of one element; still may sort O(n log n).
- **Kadane's algorithm** — max subarray sum; DP-like O(n) scan.

---

## 9. Common mistakes

- Off-by-one in subarray indices (inclusive vs exclusive ranges).
- Assuming sorted without checking — or sorting when O(n) hash exists.
- Overflow in sum/product — use `long` when constraints allow large values.
- Modifying array while iterating forward without careful write index.
- Confusing **subarray** (contiguous) with **subsequence**.

---

## 10. Related patterns

```text
Arrays alone     → one pass, in-place two indices
Arrays + hash    → complement lookup, frequency (see hashmap pattern)
Arrays + sort    → two pointers, intervals, binary search
Arrays + window  → contiguous constraint on subarray
Arrays + prefix  → range queries, transform to O(1) range sum
```

Compare [Two Pointers](../patterns/two-pointers.md), [Sliding Window](../patterns/sliding-window.md),
[Prefix Sum](../patterns/prefix-sum.md) when you hit those signals.

---

## 11. Curated problems (from index — docs added when studied)

| ID | Problem | Why it's here |
| --- | --- | --- |
| A1 | [Best Time to Buy and Sell Stock](../problems/easy/best-time-buy-sell-stock.md) | One-pass; min buy + max profit (not max price) |
| A2 | Product of Array Except Self | Prefix/suffix; no division |
| A3 | Maximum Subarray | Kadane; classic invariant |
| A4 | Merge Intervals | Sort + merge; bridges to intervals |

A1 is documented. Next handbook problem: two pointers (Container With Most Water or 3Sum).

---

## 12. Revision notes

```text
Pattern: sequential storage; O(1) index access; O(n) scan baseline
Recognition: subarray, in-place, indices, contiguous constraint
Core idea: one pass (running state), two indices, or prefix/suffix
Time: usually O(n) or O(n log n) if sort
Space: often O(1) in-place or O(n) for prefix/hash
Common mistake: subarray vs subsequence; off-by-one; overflow
Interview takeaway: name scan structure before coding
Engineering: batches, buffers, sliding metrics over arrays
```

---

## Think before coding (warm-up — no solutions)

Before opening problem A1, answer without looking up solutions:

1. Given prices by day, one transaction — what single value do you track while scanning left to right?
2. Product except self — why might division be disallowed? What two passes give each position?
3. Maximum subarray — if all numbers are negative, what is the answer?
4. For n = 10⁵, is O(n²) acceptable for an array problem?

Write answers in your notes; compare when we author the first problem together.

---

## Exercises

1. Reverse an array in-place — time and space?
2. Rotate array k steps — O(n) time approaches?
3. Find duplicate in array of n+1 integers in [1,n] — O(n) time, O(1) space (Floyd) — preview only.
4. Given sorted array, remove duplicates in-place — two-index template.

---

## Key takeaways

1. Arrays reward **clear index invariants** and **one-pass state**.
2. Many "array problems" are really **hash**, **two pointer**, or **prefix** problems in disguise.
3. First array problem in this handbook is one-pass state tracking (LC 121), not Kadane.

---

## See also

- [Complexity](complexity.md) — Module 0
- [Problem index — Arrays](../roadmap/problem-index.md#arrays-4)
- [HashMap / HashSet](../patterns/hashmap-hashset.md) — next pattern after strings
- [Strings](strings.md) — similar sequential structure, different operations
