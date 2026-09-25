# Interview Templates

Reusable communication scaffolds. Practice until natural — not robotic.

---

## 10-step coding interview flow

```text
1. Restate the problem in your own words.
2. Confirm constraints (n, value range, sorted?, mutable?, duplicates?).
3. Walk through a small example and one edge case.
4. Propose brute force — describe algorithm and complexity.
5. Explain why brute force may be too slow (tie to constraints).
6. Identify optimization — name pattern or data structure.
7. Explain optimized approach — invariant, correctness sketch.
8. State time and space complexity.
9. Implement in clean Java — talk through tricky lines.
10. Dry-run example + discuss remaining edge cases.
```

---

## Opening script (example)

> "So we need the longest contiguous subarray with at most k distinct values — I'll
> confirm: n can be up to 10⁵, values are integers, and we return the length not the
> subarray itself. If k is zero or the array is empty, I'd return zero. My first thought
> is check all subarrays — that's O(n²) which likely won't scale; I'm thinking sliding
> window with a frequency map because the constraint is on a contiguous range…"

Adapt wording to the problem; hit steps 1–6 before typing.

---

## When stuck (buy time productively)

- "Let me trace the invariant on this example."
- "What's the bottleneck in the brute force approach?"
- "Can I sort? Can I use extra space?"
- "Is there a monotonic property I can binary search on?"

After ~5–8 minutes without progress, ask for a small hint.

---

## Mock interview scorecard

| Category | /5 |
| --- | ---: |
| Problem understanding | |
| Pattern recognition | |
| Algorithm | |
| Complexity | |
| Code quality | |
| Edge cases | |
| Communication | |
| **Total** | **/35** |

**Feedback sections:**

- What I did well
- What I missed
- Senior-level feedback
- What to improve
- Pattern to revise → link to handbook doc

---

## Post-interview debrief (5 minutes)

```text
Problem (if recallable):
Pattern I recognized:
Pattern I missed:
Communication gap:
Update progress.md / revision-log.md:
Next revision date:
```

See [`interview-strategy.md`](../roadmap/interview-strategy.md) for full mock rules.
