# Interview Strategy

How to use this handbook in **real senior engineering interviews** — communication,
timing, and mock practice.

## What senior interviews test

Senior coding rounds still test DSA, but evaluators also watch for:

- **Problem decomposition** — breaking an ambiguous prompt into solvable pieces.
- **Trade-off articulation** — why this structure, why this complexity.
- **Correctness under pressure** — edge cases, off-by-one, null/empty inputs.
- **Communication** — thinking out loud without rambling.
- **Engineering maturity** — connecting algorithms to systems when relevant.

This handbook optimizes for those signals, not for ICPC-style speed.

---

## The 10-step communication flow

Practice until this feels natural, not scripted:

1. **Restate the problem** in your own words.
2. **Confirm constraints** — size, value range, sorted?, mutable?, duplicates?
3. **Propose a simple approach** — often brute force or obvious structure.
4. **Explain why it may be too slow** — tie to constraints (e.g. O(n²) vs n = 10⁵).
5. **Identify the optimization** — name the pattern or data structure.
6. **Explain the approach** — invariant, loop structure, why it's correct.
7. **State complexity** — time and space; mention amortized if relevant.
8. **Implement** — clean Java; talk through non-obvious lines.
9. **Test** — dry-run one example; then an edge case.
10. **Discuss edge cases** — empty, single element, duplicates, overflow.

Template copy: [`revision/interview-templates.md`](../revision/interview-templates.md).

---

## Time budget (45-minute round)

| Minutes | Activity |
| ---: | --- |
| 0–5 | Clarify + restate |
| 5–10 | Brute force + complexity |
| 10–15 | Optimized approach + buy-in from interviewer |
| 15–35 | Implementation |
| 35–42 | Test + edge cases |
| 42–45 | Follow-ups, trade-offs |

If stuck after ~8 minutes without progress, ask for a hint — that is normal.

---

## Clarifying questions (always ask)

- Input size and value bounds?
- Sorted or can we sort?
- Duplicates allowed?
- Return value vs mutate input?
- Multiple valid answers or unique?
- Memory limits — in-memory only?

---

## When to name the pattern

**Do** say: "This looks like a sliding window because we need the longest subarray
with a constraint on a running count."

**Don't** say: "This is LeetCode 424" or jump to code without an invariant.

Interviewers want to hear **reasoning**, not problem IDs.

---

## Mock interview rules

Use [`mock-interviews/`](../mock-interviews/) after completing related modules.

### Interviewer (tutor) rules

1. Give **one problem** — do not reveal the pattern.
2. Wait for your approach before hinting.
3. Ask realistic follow-ups ("What if k were unknown?", "Can you do O(1) space?").
4. Hint only when you're stuck ~5+ minutes.
5. Score **reasoning before code**.

### Scoring rubric

| Category | /5 | What "5" looks like |
| --- | ---: | --- |
| Problem understanding | | Restated correctly; constraints confirmed |
| Pattern recognition | | Named technique with justification |
| Algorithm | | Correct invariant / recurrence / traversal |
| Complexity | | Accurate time & space; discussed trade-offs |
| Code quality | | Readable Java; sensible names; no silent bugs |
| Edge cases | | Proactively listed and handled |
| Communication | | Clear narrative; receptive to hints |

### Feedback format

After each mock:

- **What you did well**
- **What you missed**
- **Senior-level feedback** — what a staff engineer would probe next
- **What to improve**
- **Pattern to revise** — link to handbook section

---

## Before a real interview loop

1. Review [`revision/pattern-cheatsheet.md`](../revision/pattern-cheatsheet.md) (15 min).
2. Re-solve 2–3 **medium** problems from weak areas (timed).
3. One full mock ([`mock-interviews/mixed/`](../mock-interviews/mixed/)).
4. Sleep — cramming 20 problems the night before hurts communication.

---

## After a real interview

Log in [`progress/revision-log.md`](../progress/revision-log.md):

- Problems asked (if recallable)
- Patterns you recognized / missed
- Communication gaps
- Topics to revisit

This handbook evolves with your interviews — add notes, not guilt.
