---
title: "Subarray Sum Equals K"
description: Count contiguous subarrays with sum k via prefix-sum frequencies in a HashMap.
status: review
difficulty: medium
pattern: prefix-sum
tags: [arrays, hashmap, prefix-sum, subarray]
source: leetcode-560
created: 2026-10-18
updated: 2026-10-18
---

# Subarray Sum Equals K

Studied interactively. The lesson is **prefix sum + frequency map** for counting contiguous ranges when negatives break sliding window — not “Two Sum with subarrays.”

## Problem

Given an integer array `nums` and an integer `k`, return the **number** of continuous, non-empty **subarrays** whose sum equals `k`.

A subarray must use **contiguous** elements (not subsequences or arbitrary combinations).

Examples:

```text
nums = [1, 1, 1], k = 2        → 2
nums = [1, 2, 3], k = 3        → 2   ([1,2] and [3])
nums = [0, 0, 0], k = 0        → 6
nums = [1, -1, 1], k = 1       → 3
```

## Constraints

Typical: `n` up to ~2×10⁵.

**Negative numbers and zeros are allowed** — this rules out the usual sum-based sliding window (see below).

Why they matter: brute force is O(n²). With large `n`, you need a single-pass structure. Negatives mean window sums are not monotonic as you expand or shrink.

## Clarifying questions

- Count **subarrays**, not values or index pairs?
- Are elements only non-negative? (If yes, sliding window may apply; this write-up assumes the general case.)
- Can `k` be negative? Can prefix sums repeat?
- Empty subarray counted? **No** — only non-empty contiguous ranges.

## Think before coding

1. Do I need every subarray’s elements, or only how many match?
2. If I fix the **end** index, what earlier **start** would make the sum `k`?
3. Why might sliding window fail here?
4. Should the map store **indexes** or **counts**?

## Brute force

**Intuition:** Every subarray is defined by a start index `i` and end index `j` with `i ≤ j`. Enumerate all pairs and check the sum.

**Algorithm:**

- For each starting index `i`, set `runningSum = 0`.
- For `j` from `i` to `n - 1`, add `nums[j]` to `runningSum`.
- Whenever `runningSum == k`, increment the answer.

Do **not** build a list of all subarrays — only maintain the running sum as `j` advances. Recomputing `sum(nums[i..j])` from scratch each time would repeat work; extending `j` by one updates the sum in O(1).

**Complexity:** Time O(n²). Auxiliary space O(1).

**Limitations:** Quadratic time fails typical constraints. The nested loops also hint that we should reuse **prefix information** instead of restarting from every `i`.

## Why the usual sliding window does not apply (generally)

Sliding window on **sum** assumes that when you move the right end, the window sum moves predictably (usually **non-decreasing** if all elements are non-negative). Then you can compare `currentSum` to `k` and decide to shrink from the left.

With negatives, expanding the window can **increase or decrease** the sum. Example `nums = [1, -1, 1]`, `k = 1`:

- Window `[1]` → sum `1` (valid).
- Expand to `[1, -1]` → sum `0` — sum **dropped** after adding an element.
- Expand to `[1, -1, 1]` → sum `1` again.

You cannot safely move `left` or `right` using only “sum too small / too large” without missing or double-counting cases.

Sliding window remains the right tool when constraints guarantee monotonic behavior (e.g. non-negative nums, or “shortest subarray with sum ≥ k”). For **exact sum k with negatives**, use prefix sums.

See also: [Sliding window](../patterns/sliding-window.md) · [Prefix sum](../patterns/prefix-sum.md) (pattern page still a scaffold).

## Optimized approach

**Pattern:** Prefix sum + HashMap **frequencies**.

### Prefix-sum equation

Let `prefixSum(t)` be the sum of `nums[0..t]` inclusive.

For a subarray from `i` through `j`:

```text
subarraySum(i, j) = prefixSum(j) - prefixSum(i - 1)
```

We want `prefixSum(j) - previousPrefix = k`, so:

```text
previousPrefix = currentPrefixSum - k
```

**Insight:** At each position (each `j`), count how many **earlier** prefix sums equal `currentPrefixSum - k`. Each such prefix is a valid start boundary for a subarray ending here with sum `k`.

### HashMap stores counts, not indexes

```java
Map<Integer, Integer> prefixCount = new HashMap<>();
```

- **Key:** prefix sum value seen so far.
- **Value:** how many times that prefix sum has occurred.

If `currentPrefixSum - k` appeared three times earlier, there are **three** distinct subarrays ending at the current index with sum `k` (different start positions).

| Goal | Map value |
| --- | --- |
| **Count** matching subarrays | prefix sum → **count** |
| Find **one** subarray / its indexes | prefix sum → **index** |
| List **all** matching subarrays | prefix sum → list of indexes |

This problem asks for a **count** only — indexes are unnecessary.

Contrast [Two Sum](../problems/easy/two-sum.md): complement lookup uses `value → index` because the API returns indices.

### Initialization `0 → 1`

```java
prefixCount.put(0, 1);
```

This represents the **empty prefix** before index `0` — not a claim that the array contains zero.

It counts subarrays that **start at index 0**: when `currentPrefixSum == k`, we need `previousPrefix == 0`, i.e. no elements before the start.

Examples:

- `nums = [3], k = 3` — at the only element, `currentPrefixSum = 3`, need prefix `0` → one subarray `[3]`.
- `nums = [1, 2], k = 3` — at index `1`, `currentPrefixSum = 3`, need prefix `0` → subarray `[1, 2]`.

With `0 → 1` in place, do **not** add a separate `if (currentSum == k)` increment — that **double-counts** the same subarrays starting at `0`.

If the running prefix becomes `0` later (e.g. after `[1, -1]`), that is a **natural** prefix boundary; its frequency is tracked separately from the initial empty prefix entry.

### Processing order: lookup before record

For each `num`:

1. Update `currentSum`.
2. `neededPrefix = currentSum - k`.
3. `count += prefixCount.getOrDefault(neededPrefix, 0)`.
4. Increment `prefixCount` for `currentSum`.

Lookup must use only **strictly prior** prefix boundaries — same discipline as complement-before-`put` in Two Sum.

**Correctness:** Every subarray `[i..j]` corresponds to exactly one pair `(prefix before i, prefix at j)` with difference `k`. Each is counted once when processing index `j`.

**Complexity:** Time O(n) average (HashMap get/put). Auxiliary space O(n) worst case for distinct prefix sums.

## Java implementation

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> prefixCount = new HashMap<>();
        prefixCount.put(0, 1);

        int currentSum = 0;
        int count = 0;

        for (int num : nums) {
            currentSum += num;

            int neededPrefix = currentSum - k;
            count += prefixCount.getOrDefault(neededPrefix, 0);

            prefixCount.put(
                currentSum,
                prefixCount.getOrDefault(currentSum, 0) + 1
            );
        }

        return count;
    }
}
```

## Dry run

`nums = [1, -1, 1], k = 1` → answer **3**.

| Step | Element | `currentSum` | `neededPrefix` | Found in map | `count` after lookup | Map after update |
| --- | --- | ---: | ---: | ---: | ---: | --- |
| init | — | 0 | — | — | 0 | `{0:1}` |
| 1 | `1` | 1 | 0 | 1 | 1 | `{0:1, 1:1}` |
| 2 | `-1` | 0 | -1 | 0 | 1 | `{0:2, 1:1}` |
| 3 | `1` | 1 | 0 | 2 | **3** | `{0:2, 1:2}` |

The three subarrays with sum `1`:

1. `[1]` — indices `0..0` (step 1: `neededPrefix = 0` from the initial empty prefix).
2. `[1]` — index `2` alone (step 3: `neededPrefix = 0` matches the prefix sum `0` recorded after `[1, -1]`).
3. `[1, -1, 1]` — indices `0..2` (step 3: second match for prefix `0` from the empty prefix before index `0`).

**Note:** Two stored occurrences of prefix sum `0` (`{0:2}` before the final update) are different **start boundaries** — empty prefix vs prefix after index `1` — so both contribute when index `2` closes a valid subarray.

## Edge cases

- All zeros, `k = 0` — many overlapping subarrays (combinatorics on runs).
- `k = 0` with mixed signs — prefix repeats drive count.
- Single element equal / not equal to `k`.
- Negative `k`.
- Large magnitude sums — watch `int` overflow in other variants (use `long` if needed).

## Alternatives

| Approach | Time | Space | Trade-off |
| --- | --- | --- | --- |
| Nested loops + running sum | O(n²) | O(1) | Simple; too slow |
| Prefix + frequency map | O(n) avg | O(n) | General; negatives OK |
| Sliding window on sum | O(n) | O(1) | Only when monotonicity holds (e.g. non-negative) |

## Interview follow-ups

- Subarray sum **divisible** by `k` (mod arithmetic on prefix sums).
- **Longest** subarray with sum `k` (map stores index, not count).
- 2D version / matrix subarray sums.
- Return **all** subarrays — store lists of indexes; output size can be O(n²).

## How to explain this in an interview

1. **Observation:** Fix the end index; starts are determined by earlier prefix sums.
2. **Data structure:** HashMap from prefix sum → **frequency** of that prefix.
3. **Algorithm:** For each element, add to running sum; add `count` of `(currentSum - k)`; then record `currentSum`. Initialize `0 → 1` for subarrays starting at index `0`.
4. **Complexity:** O(n) average time, O(n) auxiliary space.
5. **Tradeoff:** Sliding window is O(1) space but needs non-negative (or similar) constraints; prefix + hash handles general integers.

**Short form:**

> For each position, I maintain a running prefix sum. A subarray ending at this position has sum `k` if an earlier prefix sum equals `currentSum - k`. I use a HashMap to store the frequency of previously seen prefix sums, allowing me to count all matching subarrays in one pass.

## Common mistakes

- Treating it like **Two Sum** (values / indices) instead of **prefix differences**.
- Materializing every subarray in a list.
- Using **sliding window** despite negative numbers.
- Storing **indexes** when only a **count** is required.
- Forgetting **`prefixCount.put(0, 1)`**.
- Adding **`if (currentSum == k)`** on top of `0 → 1` — **double-counts** starts at index `0`.
- **Recording** the current prefix in the map **before** the lookup.
- Confusing **subarray** (contiguous) with **subsequence**.

## Pattern recognition

```text
Count subarrays with exact sum k + negatives allowed
→ Prefix sum + HashMap frequencies

currentSum - k seen before?  → add that frequency to answer
Initialize 0 → 1 for subarrays starting at index 0
Lookup before incrementing current prefix count
```

- **Prefix Sum + HashMap:** count subarrays with target sum, including negative numbers.
- **HashMap frequency:** multiple occurrences of a required prefix → multiple valid subarrays ending here.
- **Sliding window:** only when constraints support monotonic window sums.
- **Requirement-driven map:** counts for counting; indexes for locating; index lists for enumerating all matches.

## Real engineering connection

Prefix aggregates appear in stream windows, billing periods, and metrics (“how many intervals had net change X?”). Frequency maps are the same idea as counting prior states for event correlation — not storing every interval explicitly.

## Revision notes

```text
Pattern: prefix sum + HashMap (prefix → count)
Recognition: count contiguous subarrays with sum k; negatives in array
Core idea: at j, add frequency of (prefixSum(j) - k); init 0→1; lookup before put
Time: O(n) average
Space: O(n) distinct prefixes
Common mistake: sliding window with negatives; 0→1 + extra currentSum==k; put before lookup
Interview takeaway: prefix difference equation; counts not indexes for counting problem
```
