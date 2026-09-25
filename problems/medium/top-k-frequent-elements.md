---
title: "Top K Frequent Elements"
description: Count frequencies with HashMap, then keep k candidates in a min-heap of size k.
status: review
difficulty: medium
pattern: heap-priority-queue
tags: [hashmap, heap, top-k, priority-queue]
source: leetcode-347
created: 2026-09-07
updated: 2026-09-07
---

# Top K Frequent Elements

Studied interactively. Do **not** memorize “Top K always means heap.” Heap wins when **k ≪ unique count**.

## Problem

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. Order does not matter.

Example:

```text
nums = [1, 1, 1, 2, 2, 3]
k = 2
→ [1, 2]
```

## Constraints

Typical: `n` up to ~10⁵, `k` in `[1, number of unique]`.

Why they matter: sorting **all** unique frequencies is O(u log u). If k is tiny and u is huge, a bounded heap is O(u log k).

## Clarifying questions

- Is order of the answer required?
- Are frequencies unique? (Ties — any k of the top band?)
- Can k equal the number of unique values?
- Stream vs full array in memory?

## Think before coding

1. What must I compute before ranking anything?
2. After I have `value → frequency`, do I need a full sort?
3. If I only keep k candidates, should the heap be min or max — and **why**?
4. Does `PriorityQueue` automatically stay size k?

## Brute force

**Intuition:** Count frequencies, put unique numbers in a list, sort by frequency descending, take first k.

**Complexity:** O(n) to count + O(u log u) to sort. Space O(u).

**Bottleneck:** Sorting candidates you will mostly throw away when k ≪ u.

Ask: *Do we only need the top K rather than everything?*

## Optimized approach

**Pattern:** Top K + k ≪ candidate count → **bounded min-heap**.

**Step 1 — frequency map**

```java
frequency.put(num, frequency.getOrDefault(num, 0) + 1);
```

`getOrDefault(key, 0)` returns the count or `0` if absent.

**Step 2 — heap of size k**

Keep the **current top-k** as a **min-heap ordered by frequency**. The root is the **weakest** of the k. A new candidate with higher frequency replaces that root.

```text
for each unique element:
    offer to heap
    if heap.size() > k:
        poll()   // drop weakest
```

**Why min-heap, not max-heap?** You need O(1) access to the **smallest frequency among the current k** to decide eviction. A max-heap would surface the strongest, which you do not evict.

**Java:** `PriorityQueue` is a **min-heap by default**. It does **not** cap size — you enforce `size > k` then `poll()`.

```java
PriorityQueue<Map.Entry<Integer, Integer>> heap =
    new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));
```

Comparator is needed because entries are not ordered by frequency naturally.

**Operations:** `offer`/`add` O(log n), `peek` O(1), `poll` O(log n). `poll` removes; `peek` does not.

**Correctness:** After processing all unique keys, the heap holds the k highest frequencies (ties depend on comparator stability — problem usually allows any valid k-set).

**Complexity:** Let n = input size, u = unique count.

- Count: O(n)
- Heap: O(u log k)
- Drain heap into result: O(k log k)

Overall **O(n + u log k)** average for HashMap ops. Space **O(u + k)** — the map still stores every unique key; only the heap is bounded by k.

## Java implementation

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> frequency = new HashMap<>();

        for (int num : nums) {
            frequency.put(num, frequency.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Map.Entry<Integer, Integer>> heap =
            new PriorityQueue<>(Comparator.comparingInt(Map.Entry::getValue));

        for (Map.Entry<Integer, Integer> entry : frequency.entrySet()) {
            heap.offer(entry);
            if (heap.size() > k) {
                heap.poll();
            }
        }

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = heap.poll().getKey();
        }
        return result;
    }
}
```

## Dry run

```text
nums = [1,1,1,2,2,3]  k = 2
frequency: 1→3, 2→2, 3→1

offer (1,3)  heap=[3]           size 1
offer (2,2)  heap=[2, 3]        size 2
offer (3,1)  heap=[1, 3, 2]     size 3 → poll 1  heap=[2, 3]

result keys: 2 and 1
```

## Edge cases

- k = 1
- k = u (heap degenerates toward sorting)
- All frequencies equal — any k uniques
- Single unique value
- Negative numbers as keys — HashMap is fine

## Alternatives

| Approach | Time | When |
| --- | --- | --- |
| Sort all unique by frequency | O(n + u log u) | k ≈ u; simpler |
| Bounded min-heap | O(n + u log k) | k ≪ u |
| Bucket sort by frequency | O(n) | Frequencies in `[1, n]`; extra buckets |

If k ≈ u, **O(u log k) ≈ O(u log u)** — sorting may be simpler and competitive.

## Interview follow-ups

- Top K frequent **words** (tie-break lexicographic).
- Stream: maintain top k as events arrive.
- Approximate top k (count-min sketch) at huge scale.

## How to explain this in an interview

1. **Observation:** Rank by frequency, but we only need k winners.
2. **Data structure:** HashMap for counts; min-heap of size k by frequency.
3. **Algorithm:** Count; offer each unique; poll when size exceeds k.
4. **Complexity:** O(n + u log k) time, O(u + k) space.
5. **Tradeoff:** Heap is for k ≪ u. If k ≈ u, sort. A Java `PriorityQueue` is **not** Kafka.

## Common mistakes

- Assuming `PriorityQueue` stays size k automatically.
- Using a max-heap and not knowing what to evict.
- Calling HashMap/heap ops guaranteed O(1).
- Saying “Top K always heap” when k ≈ u.

## Pattern recognition

```text
Top K + K << N (or << unique count)
→ Bounded min-heap
```

> If I see **k winners from many candidates** and **k is small**, think bounded heap. Priority can be frequency, distance, deadline — not only the number itself.

## Real engineering connection

In-memory `PriorityQueue`: next job, next retry, k-way merge, maintain best k. It does **not** give persistence, multi-node consumption, or delivery guarantees. Distributed “queues” are a different tool.

## Revision notes

```text
Pattern: frequency map + bounded min-heap
Recognition: k most frequent; k much smaller than uniques
Core idea: min-heap root is weakest of current k; poll when size > k
Time: O(n + u log k)
Space: O(u + k)
Common mistake: PQ does not auto-cap; max-heap for eviction
Interview takeaway: heap when k << u; sort when k ≈ u
```
