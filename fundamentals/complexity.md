---
title: "Module 0 — Complexity & Problem-Solving Fundamentals"
description: Big-O notation, complexity analysis, and the interview problem-solving framework.
status: draft
phase: 1
tags: [fundamentals, complexity, big-o]
created: 2026-08-22
updated: 2026-08-22
---

# Complexity & Problem-Solving Fundamentals

Before patterns or data structures, you need a shared vocabulary for **efficiency** and a
repeatable **problem-solving process**. This module establishes both — optimized for senior
interviews where you must explain *why* an approach scales, not just *what* the code does.

## Overview

Every coding interview answer has two layers:

1. **Algorithm design** — is the approach correct and fast enough for the constraints?
2. **Communication** — can you walk the interviewer from brute force to optimization?

Complexity analysis is how you justify (2) from (1). The process below is how you stay
calm on unfamiliar problems.

**Scope:** Asymptotic time/space, common pitfalls, amortized analysis at a practical level,
and the handbook's teaching sequence. Not formal computational complexity theory.

## Learning objectives

After this module you should be able to:

- Express time and space complexity using Big-O notation correctly.
- Compare two approaches using constraints (e.g. n ≤ 10⁵ rules out O(n²)).
- Identify dominant terms and drop constants/low-order terms in interview settings.
- Explain best, average, and worst case when they differ materially.
- Describe amortized complexity for ArrayList append and HashMap operations at a high level.
- Follow the handbook problem-solving sequence without skipping to code.
- Ask clarifying questions that expose constraints and edge cases early.

---

## 1. Why complexity matters in senior interviews

Interviewers at senior levels assume you can implement basic loops. What they probe:

- **Will your solution pass at max input size?**
- **What trade-off did you make** (time vs space, preprocessing vs query)?
- **What breaks at scale** — memory, cache, GC pressure (relevant for backend/data roles)?

A correct O(n²) solution for n = 100 is fine. For n = 10⁵, it is ~10¹⁰ operations — too slow.

**Rule of thumb for Java on typical online judges / interviews:**

| n (approx) | Typical acceptable complexity |
| --- | --- |
| n ≤ 20 | O(n!), O(2ⁿ) backtracking |
| n ≤ 500 | O(n³) |
| n ≤ 5,000 | O(n²) |
| n ≤ 10⁵ | O(n log n) |
| n ≤ 10⁶ | O(n) or O(n log n) with low constant |
| n ≤ 10⁸ | O(n) strict, often O(1) or O(log n) per query |

These are guides, not laws — always tie reasoning to **constraints stated in the problem**.

### Real engineering connection

Big-O reasoning appears everywhere outside interviews:

- **Database query plans** — nested loop join vs hash join scaling.
- **Spark shuffles** — O(n) map-side combine vs O(n log n) sort-merge.
- **Caching** — O(1) lookup vs O(n) scan changes tail latency at scale.
- **Stream processing** — sliding windows trade memory (window size) for per-event work.

---

## 2. Big-O notation (asymptotic upper bound)

**Big-O** describes how resource usage **grows** as input size n grows — ignoring constants
and lower-order terms.

We say f(n) = O(g(n)) when, for large n, f(n) is bounded above by a constant multiple of g(n).

### Common complexities (slowest → fastest growth)

| Complexity | Name | Example |
| --- | --- | --- |
| O(1) | Constant | Hash map get, index into array |
| O(log n) | Logarithmic | Binary search on sorted array |
| O(n) | Linear | Single scan, two pointers on sorted data |
| O(n log n) | Linearithmic | Efficient sorting, heap operations × n |
| O(n²) | Quadratic | Nested loops over all pairs |
| O(2ⁿ) | Exponential | Subsets without pruning |
| O(n!) | Factorial | Permutations |

**Interview habit:** State complexity **after** describing the algorithm structure ("one pass",
"binary search on answer", "DP table n × m").

### What to drop

- Constants: O(3n) → O(n)
- Lower-order terms: O(n² + n) → O(n²)

### What NOT to drop incorrectly

- Different variables: O(n + m) is not O(n) unless you justify m ≤ n.
- Exponential vs polynomial — never hand-wave these away.

---

## 3. Time vs space complexity

**Time complexity** — how operations grow with input size.

**Space complexity** — extra memory beyond input storage (auxiliary space).

Examples:

| Algorithm | Time | Auxiliary space |
| --- | --- | --- |
| Linear scan | O(n) | O(1) |
| Merge sort | O(n log n) | O(n) |
| BFS on graph | O(V + E) | O(V) queue + visited |
| Hash map frequency count | O(n) | O(k) distinct keys |

**Senior talking point:** "I'm using O(n) extra space for a hash map to reduce time from
O(n²) to O(n) — worth it given n up to 10⁵."

Input storage usually is **not** counted in auxiliary space unless the problem asks for total memory.

---

## 4. Best, average, and worst case

Some structures behave differently by case:

| Structure / op | Average | Worst |
| --- | --- | --- |
| HashMap get/put | O(1) | O(n) — rare, heavy collisions |
| Quick sort | O(n log n) | O(n²) — bad pivot |
| Binary search | O(log n) | O(log n) |

In interviews, **state worst case** unless asked otherwise. Mention average when hashing
or quickselect comes up.

---

## 5. Amortized analysis (practical level)

**Amortized O(1)** — most operations are cheap; occasional expensive ones spread cost so
average per operation stays constant.

Classic example: **ArrayList.add**

- Usually O(1) append to backing array.
- Occasionally O(n) resize and copy when capacity doubles.
- Amortized O(1) per append over a sequence of appends.

**HashMap rehash** — similar story when load factor triggers resize.

You do not need formal proof — say: "Resize happens rarely enough that append is amortized O(1)."

---

## 6. Analyzing code: a checklist

1. **Identify the input size variable** — n, m, V, E, etc.
2. **Find the innermost loop** — what does each iteration cost?
3. **Count nested structure depth** — loops, recursion depth, binary search halving.
4. **Account for hidden costs** — sorting O(n log n), hash ops O(1), set membership O(1).
5. **Recursion** — depth × work per level (e.g. merge sort: log n levels × O(n) merge).

### Worked example

```java
// Return true if any duplicate exists
boolean hasDuplicate(int[] nums) {
    Set<Integer> seen = new HashSet<>();
    for (int x : nums) {           // O(n) iterations
        if (!seen.add(x)) return true;  // O(1) average per add
    }
    return false;
}
```

- Time: O(n) average
- Space: O(n) worst case (all distinct)

Compare to sorting approach: O(n log n) time, O(1) extra if in-place sort allowed.

---

## 7. The problem-solving framework (use every time)

This handbook teaches **discovery**, not answer dumps. Follow this sequence:

```text
1. Read problem — do not code yet
2. Restate in your own words
3. Clarifying questions (size, sorted?, duplicates?, return type?)
4. Examples — including edge cases
5. Brute force — correct but slow; state complexity
6. Bottleneck — why is brute force too slow?
7. Optimization — pattern or data structure; state invariant
8. Complexity — time and space of optimized approach
9. Code — clean Java
10. Dry run — one normal example, one edge case
11. Follow-ups — what if streaming? memory limit?
```

If you propose a wrong approach, the tutor should first honor what's correct, then show
where it breaks — you should do the same for yourself in practice.

### Clarifying questions template

- What are n and value bounds?
- Can I modify the input?
- Are duplicates possible?
- Is input sorted / can I sort?
- One answer or all answers / count?
- Integer overflow possible?

---

## 8. Common misconceptions

| Myth | Reality |
| --- | --- |
| "Big-O is the exact runtime" | It describes growth rate; constants matter for small n |
| "O(2n) is different from O(n)" | Same asymptotic class — drop constants |
| "Recursive always means exponential" | Merge sort is O(n log n) — depends on branching |
| "Space O(1) means no extra memory" | Often means O(1) auxiliary; recursion uses stack O(depth) |
| "Hash map is always O(1)" | Worst case O(n); say average in interviews, acknowledge worst |

---

## 9. Common mistakes in interviews

- Jumping to code before stating brute force and complexity.
- Using O(n²) with n = 10⁵ without noticing constraint.
- Forgetting **recursion stack space** in DFS depth.
- Confusing **number of nodes** with **tree height** in skewed trees (height can be O(n)).
- Saying "optimal" without comparing to a known lower bound or constraint-driven target.

---

## 10. Related topics (coming next)

| Next | Why |
| --- | --- |
| [Arrays](../fundamentals/arrays.md) | Most problems start with sequential data |
| [HashMap / HashSet](../patterns/hashmap-hashset.md) | O(1) lookups change complexity class |
| [Binary Search](../patterns/binary-search.md) | O(log n) on sorted or monotonic structure |

---

## Revision notes

```text
Big-O: upper bound on growth; drop constants and lower-order terms
Time vs space: state both; mention trade-offs explicitly
Constraint trick: n ≤ 10⁵ → avoid O(n²); n ≤ 500 → O(n²) may be OK
Amortized: ArrayList append, HashMap resize — occasional O(n), average O(1)
Process: clarify → brute force → bottleneck → optimize → complexity → code → test
Senior tie-in: same reasoning as query plans, caches, shuffle cost
Common mistake: coding before complexity; ignoring recursion stack space
Interview takeaway: always tie approach to stated constraints
```

---

## Exercises (no solutions — think first)

1. An algorithm runs 3n² + 500n + 10 operations. State Big-O time.
2. n = 10⁶. Can you use an O(n²) algorithm? Explain.
3. DFS on a linked list of n nodes — time and auxiliary space?
4. You sort then scan once. Total complexity?
5. When would O(n) space be unacceptable in a streaming system?

---

## Thought experiments

- If HashMap worst case were common in production, how would you design a cache layer?
- Spark processes data partitioned across executors — where does O(n) vs O(n log n) show up in a join?
- Why do interview constraints encode the intended complexity class?

---

## Key takeaways

1. Complexity is how you **justify** your approach under stated constraints.
2. Always present **brute force first**, then optimize with a named bottleneck.
3. State **time and space** before or immediately after describing the optimized algorithm.
4. The problem-solving **process** is as important as the pattern library that follows.

---

## See also

- [Arrays](../fundamentals/arrays.md) — Module 1
- [Interview strategy](../roadmap/interview-strategy.md)
- [Interview templates](../revision/interview-templates.md)
- [Complexity cheatsheet](../revision/complexity-cheatsheet.md)
