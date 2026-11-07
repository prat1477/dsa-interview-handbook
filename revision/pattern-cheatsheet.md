# Pattern Cheatsheet

Only rows you have actually used. Unstudied patterns stay as a one-liner pointer — do not treat them as mastered.

## Learned

| Pattern | One-line idea | Typical time | Recognition | Doc |
| --- | --- | --- | --- | --- |
| HashSet | Membership / duplicates | O(n) avg | “Have I seen this value?” | [hashmap-hashset.md](../patterns/hashmap-hashset.md) |
| HashMap | Complement or frequency | O(n) avg | Need `target - x` or counts | [hashmap-hashset.md](../patterns/hashmap-hashset.md) |
| State tracking | Running min + running best | O(n) | One pass; order constraint (buy before sell) | [arrays.md](../fundamentals/arrays.md), [LC 121](../problems/easy/best-time-buy-sell-stock.md) |
| Two pointers | Ends on **sorted** data | O(n) | Pair sum when ordered; indices not required | [two-pointers.md](../patterns/two-pointers.md) |
| Bounded min-heap | Keep k candidates | O(n + u log k) | Top k and **k ≪ u** | [heap-priority-queue.md](../patterns/heap-priority-queue.md) |
| Sliding window | Contiguous + constraint | O(n) | Longest/shortest valid substring/subarray | [sliding-window.md](../patterns/sliding-window.md) |
| Prefix sum + HashMap | Prefix difference → count | O(n) avg | Count subarrays with sum k; negatives OK | [subarray-sum-equals-k.md](../problems/medium/subarray-sum-equals-k.md) |

**If I see X, think Y**

```text
Complement + lookup                         → HashMap
Duplicate / seen before                     → HashSet
Running best state                          → Two scalars, not full history
Sorted pair                                 → Two pointers (not automatic HashMap)
Top K + K << unique count                   → Bounded min-heap
Contiguous range + constraint + best length → Sliding window
Count subarrays, exact sum k, negatives allowed → Prefix sum + frequency map
```

## Not yet studied (do not fake fluency)

Binary search · intervals · stack · graphs · DP · …

Full stub list remains in git under `patterns/` and `algorithms/` for navigation only.
