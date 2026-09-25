---
title: "Two Sum"
description: Find two indices whose values add to target via complement lookup in a HashMap.
status: review
difficulty: easy
pattern: hashmap-hashset
tags: [arrays, hashmap, complement, two-pointers]
source: leetcode-1
created: 2026-09-07
updated: 2026-09-07
---

# Two Sum

Studied interactively. The important lesson is **when** to use a HashMap versus two pointers — not the problem ID.

## Problem

Given `nums` and `target`, return **indices** of two **distinct** elements whose values sum to `target`.

Exactly one valid answer is guaranteed.

Example:

```text
nums = [2, 7, 11, 15]
target = 9
→ [0, 1]
```

## Constraints

Typical: `n` up to ~10⁴–10⁵; return **indices**, not values.

Why they matter: nested search is O(n²). Returning indices means **sorting the array in place loses position** unless you store original indices first.

## Clarifying questions

- Exactly one solution, or zero / many?
- Same element twice (one index used twice)? Usually **no**.
- Are values unique except the pair?
- Is the array already sorted?
- Return any valid pair of indices?

## Think before coding

1. For `nums[i]`, what value must exist elsewhere?
2. Have I already seen that complement?
3. If I put the current element in the map **before** looking up, what goes wrong on `[3, 3]` with target `6`?

## Brute force

**Intuition:** For each `i`, compute `needed = target - nums[i]` and scan the rest of the array.

**Complexity:** Time O(n²). Auxiliary space O(1).

**Bottleneck:** Repeated linear search for the complement.

Ask: *What repeated work am I doing?* Searching earlier elements again.

## Optimized approach

**Pattern:** Complement lookup → `HashMap` (`value → index`).

**Intuition:** Remember previous values. One pass: look up `needed`; if missing, record the current value.

**Invariant:** The map contains **only earlier indices**. That prevents using the same element twice.

**Correctness:** When we see index `i`, every `j < i` is already in the map. If `target - nums[i]` is among them, we return those indices. The problem guarantees one answer.

**Complexity:** Time O(n) average-case. Auxiliary space O(n).

Do **not** insert the current element before the lookup.

## Java implementation

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> seen = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int needed = target - nums[i];

            if (seen.containsKey(needed)) {
                return new int[] { seen.get(needed), i };
            }

            seen.put(nums[i], i);
        }

        return new int[] {};
    }
}
```

`Map<Integer, Integer>` = value → index. `containsKey` then `get` is the usual interview form.

## Dry run

```text
nums = [2, 7, 11, 15]  target = 9

i=0 num=2  needed=7  map={}        miss  put 2→0
i=1 num=7  needed=2  map={2:0}     hit   return [0, 1]
```

```text
nums = [3, 3]  target = 6

i=0 num=3  needed=3  map={}        miss  put 3→0
i=1 num=3  needed=3  map={3:0}     hit   return [0, 1]
```

If we had inserted first at `i=0`, lookup of `3` would find **itself**.

## Edge cases

- Pair uses two equal values (`[3, 3]`, target `6`)
- Negative numbers
- Answer uses first and last indices
- Single pair guaranteed — empty return is defensive, not expected

## Alternatives

| Approach | Time | Space | When |
| --- | --- | --- | --- |
| Nested scan | O(n²) | O(1) | Tiny n |
| HashMap complement | O(n) avg | O(n) | Unsorted; need original indices |
| Sort + two pointers | O(n) if already sorted; else O(n log n) | O(1) extra on the sorted array | Need **values**, or you stored index pairs before sorting |

Sorted two-pointer:

```text
left = 0, right = n - 1
sum == target → found
sum < target  → left++
sum > target  → right--
```

Pointers move monotonically. If you must sort first, **index recovery** is extra work — HashMap is usually cleaner when the API asks for indices.

**Lesson:** Do not automatically choose HashMap if the input **already** provides useful ordering and you do not need original indices.

## Interview follow-ups

- Three Sum (sort + two pointers).
- Two Sum on a stream / BST (`Two Sum III`).
- Multiple pairs; unique pairs of **values**.

## How to explain this in an interview

1. **Observation:** For each number I need `target - x` at a different index.
2. **Data structure:** HashMap of previously seen `value → index`.
3. **Algorithm:** Lookup complement first, then insert current.
4. **Complexity:** O(n) average time, O(n) space.
5. **Tradeoff:** Sorted input without index requirements → two pointers, O(1) extra space.

## Common mistakes

- Inserting into the map **before** the complement check.
- Returning values instead of indices.
- Sorting in place and losing indices.
- Saying HashMap is guaranteed O(1).

## Pattern recognition

```text
Complement + lookup          → HashMap
Sorted pair / two ends       → Two Pointers
```

> If I see **“two values that combine to a target”** and the array is **unsorted**, think HashMap. If it is **sorted**, think two pointers.

## Real engineering connection

Complement lookup is the same idea as join-by-key: one side remembered in a hash table, the other probed. Two-pointer two-sum is closer to a merge of two sorted streams.

## Revision notes

```text
Pattern: complement lookup → HashMap (value → index)
Recognition: two distinct indices sum to target
Core idea: lookup needed first; map holds only earlier indices
Time: O(n) average
Space: O(n)
Common mistake: put before containsKey; lose indices by sorting
Interview takeaway: HashMap vs two pointers depends on ordering and whether indices matter
```
