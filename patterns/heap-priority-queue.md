---
title: "Pattern — Heap / Priority Queue"
description: Bounded candidate set — especially top K when K is much smaller than the candidate count.
status: review
phase: 2
tags: [pattern, heap, priority-queue]
created: 2026-08-22
updated: 2026-09-07
---

# Heap / Priority Queue

A heap gives you the **next most important** candidate in O(log n), without sorting the entire set. In interviews, the high-ROI use is **top K with a bounded heap** when K is small.

## What is the pattern?

Maintain a **priority-ordered** collection. Java `PriorityQueue` is a **binary heap**:

- Default: **min-heap** (smallest priority at the root).
- Max-heap: `new PriorityQueue<>(Comparator.reverseOrder())`.

Priority is whatever the comparator says: number, frequency, timestamp, distance — **not** inherently “the array value.”

## Why does it work?

Sorting all u candidates is O(u log u). If you only need k winners and k ≪ u, each of u offers is O(log k) on a size-k heap → O(u log k).

For **top k largest frequencies**, the heap of size k should be a **min-heap on frequency**: the root is the **weakest** current winner, so you can evict it when a stronger candidate arrives.

## Recognition signals

- “K most frequent / largest / closest”
- “Merge k sorted lists”
- “Always process the next due job”
- k mentioned and k looks much smaller than n or unique count

## When to use

```text
Top K + K << candidate count  →  bounded min-heap (for k largest)
```

Also: k-way merge, running median (two heaps — later).

## When NOT to use

| Situation | Prefer |
| --- | --- |
| k ≈ number of uniques | Sort — similar complexity, simpler code |
| Need full order of all elements | `Arrays.sort` / TreeMap |
| Need arbitrary key lookup | HashMap |
| Distributed durable queue | Not `PriorityQueue` |

Do **not** memorize: “Top K always means heap.”

## Core template

`PriorityQueue` does **not** auto-limit size. Enforce it:

```java
PriorityQueue<Map.Entry<Integer, Integer>> heap =
    new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));

for (var entry : frequency.entrySet()) {
    heap.offer(entry);
    if (heap.size() > k) {
        heap.poll();
    }
}
```

| Method | Effect | Cost |
| --- | --- | --- |
| `offer` / `add` | insert | O(log n) |
| `peek` | min (default) without remove | O(1) |
| `poll` | min and remove | O(log n) |

No comparator needed when natural ordering (`Integer`) is the priority. Comparator when ordering by `Map.Entry` frequency, etc.

## Complexity

Typical top-k frequent: **O(n + u log k)** time, **O(u + k)** space (map still holds all uniques).

## Common variations

- Max-heap of size n (kth largest by polling n−k times) — different tradeoff.
- Bucket sort by frequency when frequencies lie in `[1, n]`.
- Two heaps for median of a stream.

## Common mistakes

- Expecting the queue to stay size k by itself.
- Max-heap when you needed to evict the **minimum** of the current k.
- Confusing `peek` and `poll`.
- Equating `PriorityQueue` with Kafka / SQS / Spark fair scheduler.

## Related patterns

```text
Heap vs sort     — k << u vs k ≈ u
Heap vs HashMap  — HashMap answers “count of x”; heap answers “next best”
```

## Curated problems

| ID | Problem | Status |
| --- | --- | --- |
| HP2 | [Top K Frequent Elements](../problems/medium/top-k-frequent-elements.md) | Documented |
| HP1 | Kth Largest Element in an Array | Planned |
| HP3 | Merge k Sorted Lists | Planned |
| HP4 | Find Median from Data Stream | Planned |

## Revision notes

```text
Pattern: bounded heap for top k
Recognition: k winners, k much smaller than candidates
Core idea: min-heap of size k; poll when size > k
Time: O(u log k) after O(n) count
Space: O(u + k)
Common mistake: PQ does not cap itself
Interview takeaway: justify heap vs full sort
```

## Real engineering connection

In-process scheduling, retries, k-way merge of sorted runs (external sort / Spark shuffle merge), maintain best-k in a stream. Persistence and multi-consumer delivery are **not** properties of `java.util.PriorityQueue`.
