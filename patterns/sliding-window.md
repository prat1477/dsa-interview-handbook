---
title: "Pattern — Sliding Window"
description: Contiguous range with a constraint — expand right, shrink left, never move pointers backward.
status: review
phase: 2
tags: [pattern, sliding-window]
created: 2026-08-22
updated: 2026-09-07
---

# Sliding Window

When the answer is a **contiguous** subarray or substring plus a **constraint on that range**, maintain a window `[left, right]` instead of restarting a scan at every start index.

## What is the pattern?

Two indices define the current segment. `right` expands to include new elements. When the window **violates** the constraint, `left` shrinks until it is valid again. Track the best window (length, sum, etc.).

Typical structure:

```text
right → expand
left  → shrink when invalid
state → track window condition (set, counts, sum)
result → best window seen
```

## Why does it work?

Each start index in brute force re-scans characters that a previous window already proved unique (or already counted). If both pointers **only move forward**, each index is added and removed a bounded number of times → **O(n)** despite a nested `while`.

## Recognition signals

- **Substring / subarray** (ask: contiguous?)
- Longest or shortest range **satisfying a constraint**
- “No repeating characters,” “at most k distinct,” “sum ≥ target”
- Need the best window, not all windows

## When to use

Contiguous + constraint + optimize length (or count of such windows, with care).

## When NOT to use

| Situation | Prefer |
| --- | --- |
| Non-contiguous subsequence | DP / two pointers on subsequences |
| Arbitrary (non-window) range sums | [Prefix sum](prefix-sum.md) |
| Sorted pair from two ends, not a growing segment | [Two pointers](two-pointers.md) |
| Global “seen anywhere,” not in a range | [HashSet](hashmap-hashset.md) alone |

**Two pointers vs sliding window:** two pointers often move because of **sorted order** (left/right ends). Sliding window moves because a **contiguous segment’s validity** changed.

## Core template

```java
Set<Character> seen = new HashSet<>();
int left = 0;
int max = 0;

for (int right = 0; right < s.length(); right++) {
    while (seen.contains(s.charAt(right))) {
        seen.remove(s.charAt(left));
        left++;
    }
    seen.add(s.charAt(right));
    max = Math.max(max, right - left + 1);
}
```

Use **`while`**, not a single `if`, until the invariant holds.

Remove the character at **old** `left`, **then** increment:

```java
seen.remove(s.charAt(left));
left++;
```

## Complexity

Time **O(n)** if left and right each move at most n times. Space **O(window state)** — O(n) general alphabet, O(1) if alphabet is fixed and tiny.

Nested loops are **not** automatically O(n²).

## Common variations

- At most k distinct characters (map of counts; shrink when `map.size() > k`).
- Minimum window covering a target (harder: shrink while still valid).
- Fixed-size window (only `right` moves; `left = right - k`).
- Last-index map: jump `left` instead of shrinking one-by-one.

## Common mistakes

- Subsequence vs substring.
- `if` shrink when multiple removals are required.
- `left++` before `remove(s.charAt(left))`.
- Calling the nested `while` O(n²) without the monotonic argument.

## Related patterns

```text
Two Pointers     — often sorted; ends move toward each other
Sliding Window   — contiguous; left/right both increase
Prefix Sum       — any range sum, not necessarily a sliding constraint
HashSet          — membership; here the set *is* window state
```

## Curated problems

| ID | Problem | Status |
| --- | --- | --- |
| S2 | [Longest Substring Without Repeating Characters](../problems/medium/longest-substring-without-repeating-characters.md) | Documented |
| SW1 | Maximum Average Subarray I | Planned |
| SW5 | Minimum Size Subarray Sum | Planned |
| S3 | Minimum Window Substring | Planned |

## Revision notes

```text
Pattern: expand right, shrink left, maintain invariant
Recognition: longest/shortest contiguous range with a constraint
Core idea: while invalid; remove then left++; pointers only forward
Time: O(n)
Space: O(window state)
Common mistake: if not while; increment before remove
Interview takeaway: nested monotonic pointers still O(n)
```

## Real engineering connection

Rate limits (events in last T seconds), session windows, streaming “unique keys in the current buffer.” Time windows in production often expire by **timestamp**, not only by count — same shrink/expand idea.
