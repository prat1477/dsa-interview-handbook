---
title: "Contains Duplicate"
description: Detect whether any value appears twice using HashSet membership.
status: review
difficulty: easy
pattern: hashmap-hashset
tags: [arrays, hashset, duplicate-detection]
source: leetcode-217
created: 2026-09-07
updated: 2026-09-07
---

# Contains Duplicate

Studied interactively. Documented here so the reasoning — not only the code — is revisable.

## Problem

Given an integer array `nums`, return `true` if any value appears **at least twice**, otherwise `false`.

Examples:

```text
[1, 2, 3, 1] → true
[1, 2, 3, 4] → false
```

## Constraints

Typical interview bounds: `n` up to ~10⁵, values in a wide integer range.

Why they matter: pairwise comparison is O(n²) and fails at 10⁵. You need a linear scan plus a structure that answers “have I seen this?” in average O(1), or you sort and scan adjacent values.

## Clarifying questions

- Can the array be empty? (Usually `false` — no duplicate.)
- Are we allowed extra memory?
- May we mutate / sort the input?
- Do we only need existence, or the duplicated value / indices?

## Think before coding

1. What question am I answering for each element?
2. If I scan left to right, what do I need from the past?
3. If extra space is forbidden, what other ordering can I impose?

## Brute force

**Intuition:** For each index `i`, scan `i+1 … n-1` for an equal value.

**Algorithm:** Nested loops; return `true` on first match.

**Complexity:** Time O(n²). Auxiliary space O(1).

**Limitations:** Too slow for large `n`. Repeats the same “have I seen this?” search.

Ask: *What work am I repeating that I could avoid?* Searching the prefix again for every element.

## Optimized approach

**Pattern:** Duplicate detection → `HashSet`.

**Intuition:** Remember values already seen. The question becomes a membership test, not a rescan.

**Java insight:** `Set.add(x)` returns `false` if `x` was already present. That return value *is* the duplicate check.

**Correctness:** The first time a value appears a second time, `add` fails and we return `true`. If the loop finishes, every value was unique.

**Complexity:** Time O(n) average-case (each `add` is O(1) average). Auxiliary space O(n) worst case (all distinct). Do **not** say HashSet is guaranteed O(1).

## Java implementation

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();

        for (int num : nums) {
            if (!seen.add(num)) {
                return true;
            }
        }

        return false;
    }
}
```

Prefer `for (int num : nums)` over boxing to `Integer` unless you need a wrapper.

## Dry run

```text
input: [1, 2, 3, 1]

num=1  add → true   seen={1}
num=2  add → true   seen={1,2}
num=3  add → true   seen={1,2,3}
num=1  add → false  return true
```

```text
input: [1, 2, 3, 4]  → all adds succeed → false
```

## Edge cases

- Empty array → `false`
- Single element → `false`
- All values identical → `true` on the second element
- Duplicate at the end vs immediately after first occurrence — same algorithm

## Alternatives

| Approach | Time | Space | Trade-off |
| --- | --- | --- | --- |
| Nested scan | O(n²) | O(1) | Simple; too slow at scale |
| HashSet | O(n) avg | O(n) | Default interview answer |
| Sort + adjacent compare | O(n log n) | depends on sort | Lower extra memory if in-place sort is allowed |

If memory is tight **and** mutation is allowed, sorting is a practical tradeoff. Say that out loud.

## Interview follow-ups

- Find the duplicated value, or all duplicates.
- `nums` contains values in `[1, n]` with n+1 elements — can you use O(1) extra space? (Floyd / index marking — later.)
- Stream of values that do not fit in memory.

## How to explain this in an interview

1. **Observation:** Duplicate means “this value already appeared.”
2. **Data structure:** `HashSet` of seen values.
3. **Algorithm:** Scan once; if `add` returns false, we have a duplicate.
4. **Complexity:** O(n) time average, O(n) space.
5. **Tradeoff:** If extra memory is forbidden, sort then compare neighbors in O(n log n).

## Common mistakes

- `contains` then `add` as two steps when `!seen.add(num)` already expresses both.
- Calling HashSet “guaranteed O(1).”
- Sorting when the interviewer did not restrict space — HashSet is the intended O(n) story.

## Pattern recognition

> If I see **“have I already seen this value?”** → **HashSet**.

Duplicate detection is membership, not pair-search.

## Real engineering connection

Same idea as: unique-key checks, idempotency keys, “already processed event id” in a consumer. A JVM `HashSet` is in-memory membership — not a distributed dedupe store.

## Revision notes

```text
Pattern: duplicate detection → HashSet
Recognition: any value appears twice / unique check
Core idea: seen.add(x) is false iff x already existed
Time: O(n) average
Space: O(n)
Common mistake: guaranteed O(1); nested scan at n=1e5
Interview takeaway: membership beats rescan; sorting is the memory tradeoff
```
