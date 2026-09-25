# Style Guide

The contract every **pattern document** and **problem document** in this handbook
follows. Its job is to make the handbook read like one coherent preparation system —
deep enough for senior interviews, practical enough for 2–3 hours per week.

When in doubt, copy the shape of [`fundamentals/complexity.md`](fundamentals/complexity.md)
(fundamentals) or [`templates/pattern.md`](templates/pattern.md) / [`templates/problem.md`](templates/problem.md).

## Design goals

- **Pattern mastery, not volume** — every page teaches recognition and reasoning.
- **Discover, don't dump** — problems do not reveal the answer before guiding questions.
- **Senior relevance** — connect to backend, data platforms, and distributed systems when useful.
- **Java-first** — clean Java 17+ implementations; Python only when it adds insight.
- **Incremental** — stubs are fine until a topic is actively studied.

---

## Pattern document structure

Every file under `patterns/`, and topic docs under `fundamentals/`, `data-structures/`,
and `algorithms/` when they teach a reusable technique, must contain these sections **in order**:

| # | Section | Purpose |
| --- | --- | --- |
| 1 | Front matter | YAML metadata (see below) |
| 2 | `# Title` | Exactly one H1 |
| 3 | Lead paragraph | BLUF: what the pattern is and when it matters |
| 4 | What is the pattern? | Simple explanation |
| 5 | Why does it work? | Intuition before formulas or code |
| 6 | Recognition signals | Clues in problem statements |
| 7 | When to use | Typical situations |
| 8 | When NOT to use | Similar-looking cases where another technique wins |
| 9 | Core template | Generic algorithm / pseudocode / Java skeleton |
| 10 | Complexity | Typical time and space |
| 11 | Common variations | How interviewers modify the pattern |
| 12 | Common mistakes | Especially under time pressure |
| 13 | Related patterns | Explicit comparisons (e.g. two pointers vs sliding window) |
| 14 | Curated problems | Problems from the index used to master this pattern |
| 15 | Revision notes | Short summary for quick recall |
| 16 | Real engineering connection | Optional but encouraged for senior roles |

Required front matter:

```yaml
---
title: "Pattern — Name"
description: One sentence describing the pattern.
status: draft            # draft | review | stable
phase: 2                 # roadmap phase number
tags: [pattern, ...]
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

---

## Problem document structure

Every file under `problems/` must follow this order. **Do not reveal the optimized
solution before the "Think before coding" section.**

| # | Section | Purpose |
| --- | --- | --- |
| 1 | Front matter | YAML metadata |
| 2 | `# Title` | Problem name |
| 3 | Problem | Clear statement — no solution |
| 4 | Constraints | Important limits; why they matter |
| 5 | Clarifying questions | What to ask the interviewer |
| 6 | Think before coding | Guiding questions only — space for your reasoning |
| 7 | Brute force | Intuition, algorithm, complexity, limitations |
| 8 | Optimized approach | Pattern, intuition, correctness, complexity |
| 9 | Java implementation | Clean Java 17+ |
| 10 | Python | Only when implementation differs meaningfully |
| 11 | Dry run | Realistic walkthrough |
| 12 | Edge cases | Important edge cases |
| 13 | Alternatives | Trade-offs |
| 14 | Interview follow-ups | Likely extensions |
| 14b | How to explain this in an interview | Senior verbal script: observation, structure, algorithm, complexity, tradeoff |
| 15 | Common mistakes | What candidates get wrong |
| 16 | Pattern recognition | How to spot this next time |
| 17 | Real engineering connection | Optional systems tie-in |
| 18 | Revision notes | Condensed recall block |

Revision notes block format:

```text
Pattern:
Recognition:
Core idea:
Time:
Space:
Common mistake:
Interview takeaway:
```

Problem front matter:

```yaml
---
title: "Problem Name"
description: One-line summary.
status: draft
difficulty: easy          # easy | medium | hard
pattern: two-pointers
tags: [arrays, ...]
source: leetcode-XXX      # optional external id
created: YYYY-MM-DD
updated: YYYY-MM-DD
---
```

---

## Teaching philosophy

When the author (or AI tutor) walks through a problem:

1. If you propose an incorrect approach, do **not** immediately replace it.
2. First explain what is correct, where it breaks, which assumption is wrong, and
   what observation leads toward the better solution.
3. Follow the sequence: Problem → Clarifying → Thinking → Brute force → Optimization
   → Code → Dry run → Edge cases → Pattern recognition.

---

## Interview communication template

For important problems, reinforce this flow (see [`revision/interview-templates.md`](revision/interview-templates.md)):

1. Restate the problem.
2. Confirm constraints.
3. Give a simple approach.
4. Explain why it may be too slow.
5. Identify the optimization.
6. Explain the data structure / pattern.
7. State expected complexity.
8. Implement.
9. Test using an example.
10. Discuss edge cases.

---

## Mock interview scoring

| Category | Score |
| --- | ---: |
| Problem understanding | /5 |
| Pattern recognition | /5 |
| Algorithm | /5 |
| Complexity | /5 |
| Code quality | /5 |
| Edge cases | /5 |
| Communication | /5 |

Then: what went well, what was missed, senior-level feedback, what to improve, which
pattern to revise.

---

## File naming

- Lowercase kebab-case: `sliding-window.md`, `two-sum.md`.
- Problem files: `problems/{easy|medium|hard}/NN-short-slug.md` when numbered helps order.

---

## What not to do

- Do not create dozens of problem files upfront.
- Do not optimize for LeetCode count.
- Do not include competitive-programming tricks without senior interview relevance.
- Do not duplicate Python when Java is sufficient.
