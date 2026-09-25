# Common Mistakes

Interview mistakes to watch for — add your own as you practice.

## Process mistakes

| Mistake | Fix |
| --- | --- |
| Coding before clarifying constraints | Ask n, bounds, sorted?, in-place? |
| No brute force stated | Always name naive approach + complexity first |
| Silent coding | Narrate invariant and index movement |
| Skipping dry run | Test normal + edge case out loud |
| Ignoring follow-ups | Interviewer extensions are often planned |

## Complexity mistakes

| Mistake | Fix |
| --- | --- |
| O(n²) with n = 10⁵ | Re-read constraints |
| Forgetting recursion stack | Count DFS depth as space |
| "Hash is O(1)" without caveat | Say average; mention worst case briefly |
| Ignoring sort cost | O(n log n) dominates if you sort first |

## Array / index mistakes

| Mistake | Fix |
| --- | --- |
| Off-by-one in subarray | Define inclusive/exclusive; draw indices |
| Subarray vs subsequence | Clarify contiguous requirement |
| int overflow | Use `long` for sums/products |
| Modify while iterating | Use read/write pointer pattern |

## Pattern confusion

| Mistake | Fix |
| --- | --- |
| Two pointers vs sliding window | Window maintains contiguous segment + expand/shrink rule |
| Prefix sum vs sliding window | Prefix for arbitrary range; window for contiguous constraint |
| BFS vs DFS | BFS = shortest unweighted path / levels; DFS = paths, backtracking |
| Greedy without proof | State why local choice is safe or give counterexample risk |

## Communication mistakes

| Mistake | Fix |
| --- | --- |
| Naming LeetCode number | Describe pattern instead |
| No complexity after optimization | State time/space before coding |
| Defensive on hints | Treat hints as collaboration |

## From problems studied (2026-09-07)

| Mistake | Fix |
| --- | --- |
| Two Sum: `put` before complement lookup | Lookup `needed` first so `[3,3]` cannot match itself |
| Stock: track max **price** | Track min buy + max **profit** (max price can precede min buy) |
| Window: `if` when shrinking | `while` until the invariant holds (`ABC` + second `B`) |
| Window: `left++` then `remove(s.charAt(left))` | Remove **old** left character, then increment |
| Nested `for`+`while` called O(n²) | If `left` and `right` only move forward, time is O(n) |
| “HashMap is O(1)” | O(1) **average-case** |
| “Top K always heap” | Heap when k ≪ u; sort is fine when k ≈ u |
| Expect `PriorityQueue` size k | Explicit `if (size() > k) poll()` |
