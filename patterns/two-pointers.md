---
title: "Pattern — Two Pointers"
description: Two indices move monotonically — especially on sorted data or from both ends.
status: review
phase: 2
tags: [pattern, two-pointers]
created: 2026-08-22
updated: 2026-09-07
---

# Two Pointers

Two indices (`left`, `right`) walk the array without nested O(n²) pair search. This handbook first met the pattern as the **sorted Two Sum** alternative — not as the default for unsorted Two Sum.

## What is the pattern?

Maintain two positions whose movement is **monotonic** (they never reverse). Common shapes:

- Opposite ends on a **sorted** array (pair sum, container with water).
- Fast/slow on a list (later).
- Read/write indices for in-place compacting (arrays module).

## Why does it work?

On a sorted array, if `a[L] + a[R] < target`, increasing `L` is the only way to grow the sum; if too large, decrease `R`. Each step discards an index forever → O(n) after sort.

## Recognition signals

- Array is sorted, or sorting is allowed **and** you do not need original indices (or you stored them).
- Pair / triplet from two ends.
- Palindrome check from outside in.

## When to use

Sorted pair problems; in-place partition; opposite-end geometry (container with water — planned).

## When NOT to use

| Situation | Prefer |
| --- | --- |
| Unsorted; must return **original indices** | [HashMap complement](hashmap-hashset.md) |
| Contiguous **window** constraint | [Sliding window](sliding-window.md) |

**Lesson from Two Sum:** do not automatically choose HashMap if the input already provides ordering and indices are not required.

## Core template

```text
left = 0
right = n - 1
while left < right:
    sum = a[left] + a[right]
    if sum == target → found
    if sum < target  → left++
    if sum > target  → right--
```

If you sort first: **O(n log n)** plus index bookkeeping if the API wants original positions.

## Complexity

O(n) on already-sorted data, O(1) extra space. Sort-first: O(n log n).

## Common variations

- 3Sum: sort, then two-pointer inner loop (planned).
- Remove duplicates in-place (write pointer).

## Common mistakes

- Sorting in place when the caller needed original indices.
- Using two pointers on an **unsorted** pair-sum without a story for correctness.

## Related patterns

```text
Two Pointers vs HashMap          — ordered + values vs unordered + indices
Two Pointers vs Sliding Window   — ends / sort vs contiguous validity
```

## Curated problems

| ID | Problem | Status |
| --- | --- | --- |
| H1 | [Two Sum](../problems/easy/two-sum.md) (sorted alternative) | Documented |
| TP1 | Valid Palindrome | Planned |
| TP2 | 3Sum | Planned |
| TP3 | Container With Most Water | Planned |

## Revision notes

```text
Pattern: two monotonic indices
Recognition: sorted pair; opposite ends
Core idea: too small → left++; too big → right--
Time: O(n) if sorted else O(n log n)
Space: O(1) extra on the array
Common mistake: lose indices by sorting
Interview takeaway: ordering decides HashMap vs two pointers
```

## Real engineering connection

Merging two sorted runs (same “advance the smaller side” idea). Not the same as a sliding time window.
