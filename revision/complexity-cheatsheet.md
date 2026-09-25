# Complexity Cheatsheet

## Growth rates (fast → slow for large n)

O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!)

## Constraint → complexity hint

| n | Usually need |
| --- | --- |
| ≤ 20 | O(2ⁿ), O(n!) OK |
| ≤ 500 | O(n³) |
| ≤ 5,000 | O(n²) |
| ≤ 10⁵ | O(n log n) or O(n) |
| ≤ 10⁶ | O(n) or O(n log n), tight constants |

## Common operations

| Operation | Time |
| --- | --- |
| Array index | O(1) |
| ArrayList append | O(1) amortized |
| HashMap get/put | O(1) **average** (not guaranteed) |
| HashSet add/contains | O(1) **average** |
| PriorityQueue offer/poll | O(log n) |
| Sliding window (monotonic L/R) | O(n) even with nested while |
| Sequential loops O(n)+O(n)+O(n) | Still O(n) |
| TreeMap get/put | O(log n) |
| Sort | O(n log n) |
| Binary search | O(log n) |
| BFS/DFS graph | O(V + E) |

## Space reminders

- Recursion depth = stack space O(depth)
- BFS queue O(width)
- DP table O(states)
- Hash map O(distinct keys)

## Interview phrases

- "Dominant term is n log n from the sort."
- "Trading O(n) space for O(n) time instead of O(n²)."
- "O(1) average-case HashMap lookup, not guaranteed."
- "Both pointers only move forward, so the nested while is still O(n)."
- "k ≪ uniques → bounded heap; k ≈ uniques → sorting is competitive."

See [Module 0 — Complexity](../fundamentals/complexity.md) for full treatment.
