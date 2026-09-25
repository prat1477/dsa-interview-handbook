---
title: "Pattern — HashMap / HashSet"
description: Average O(1) membership and complement lookup — the first high-ROI interview structure.
status: review
phase: 1
tags: [pattern, hashmap, hashset]
created: 2026-08-22
updated: 2026-09-07
---

# HashMap / HashSet

Hash-based collections turn **“have I seen this?”** and **“what pairs with this?”** into average O(1) work. That is why they appear in the first week of this handbook — not because they are “easy,” but because they change the complexity class of a linear scan.

## What is the pattern?

Keep a **set of seen values** or a **map from value → useful payload** (index, count, last position) so you do not rescan the prefix.

- `HashSet` — membership / uniqueness.
- `HashMap` — lookup of a related value (complement, frequency, index).

## Why does it work?

Scanning the prefix again for every element is O(n²). If equality and hashing are cheap, remembering the prefix in a table makes each check average O(1). You trade **auxiliary memory** for **not repeating search**.

Hashing is **average-case** O(1) for get/put/contains. Worst case degrades with collisions (say this once in interviews; do not dwell unless asked).

## Recognition signals

- “Any duplicate?” / “all unique?”
- “Two values that sum / differ / complement to X”
- “Frequency of each value” / “group by key”
- “First index where this appeared”

Think: **If I remember the past in a table, what query becomes O(1)?**

## When to use

- Unsorted input, need fast lookup by **value**.
- Counting / grouping.
- Need **original indices** after a one-pass scan (Two Sum).

## When NOT to use

| Situation | Prefer |
| --- | --- |
| Input already sorted; pair from two ends; indices not required | [Two pointers](two-pointers.md) |
| Contiguous window constraint | [Sliding window](sliding-window.md) |
| Extra memory forbidden; mutation allowed | Sort + adjacent scan |
| Ordered keys / range queries | TreeMap (later) |
| Need top k of frequencies, k ≪ uniques | HashMap **then** [heap](heap-priority-queue.md) |

## Core template

**Membership (duplicate):**

```java
Set<Integer> seen = new HashSet<>();
for (int num : nums) {
    if (!seen.add(num)) {
        return true; // already present
    }
}
```

`add` returns `false` if the element existed — use that return value.

**Complement (Two Sum):** lookup **then** insert so the current index cannot match itself.

```java
Map<Integer, Integer> seen = new HashMap<>(); // value → index
for (int i = 0; i < nums.length; i++) {
    int needed = target - nums[i];
    if (seen.containsKey(needed)) {
        return new int[] { seen.get(needed), i };
    }
    seen.put(nums[i], i);
}
```

**Frequency:**

```java
Map<Integer, Integer> frequency = new HashMap<>();
for (int num : nums) {
    frequency.put(num, frequency.getOrDefault(num, 0) + 1);
}
```

## Complexity

| Operation | Average | Worst |
| --- | --- | --- |
| HashSet/HashMap get/put/contains | O(1) | O(n) collisions |
| Full scan + table | O(n) | rare O(n²) |

Auxiliary space: O(u) unique keys (up to O(n)).

## Common variations

- Map value → **list** of indices.
- Map **canonical key** (sorted string) → group (anagrams — not yet studied).
- Frequency map + another structure (heap, bucket).

## Common mistakes

- Saying operations are **guaranteed** O(1).
- Inserting the current key **before** complement lookup (Two Sum / `[3,3]`).
- `contains` + `add` as two statements when `!seen.add(x)` is enough.
- Sorting and losing indices when the API wants positions.

## Related patterns

```text
HashSet          vs  sort + adjacent     — time vs memory
HashMap Two Sum  vs  two pointers        — unsorted+indices vs sorted+values
HashMap counts   vs  heap                — all frequencies vs only top k
HashSet in window vs sliding window      — set is the window state, not a different problem
```

## Curated problems

| ID | Problem | Status |
| --- | --- | --- |
| H0 | [Contains Duplicate](../problems/easy/contains-duplicate.md) | Documented |
| H1 | [Two Sum](../problems/easy/two-sum.md) | Documented |
| — | [Top K Frequent](../problems/medium/top-k-frequent-elements.md) (map + heap) | Documented |
| H2 | Group Anagrams | Planned |
| H3 | Longest Consecutive Sequence | Planned |
| H4 | Subarray Sum Equals K | Planned |

## Revision notes

```text
Pattern: remember past values in HashSet / HashMap
Recognition: seen before? complement? frequency?
Core idea: lookup then insert; add() return value; getOrDefault for counts
Time: O(n) average
Space: O(u)
Common mistake: guaranteed O(1); put before lookup
Interview takeaway: justify hash vs sort vs two pointers
```

## Real engineering connection

Caching, indexing, aggregation, join-by-key, idempotency sets. A JVM `HashMap` is process-local — not Redis, not a shuffled Spark map-side combine, though the **idea** (key → payload) is the same.
