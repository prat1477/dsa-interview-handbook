# DSA Interview Handbook

A long-term, incremental **handbook for senior software engineering coding interviews**
— structured for **pattern mastery**, not LeetCode volume.

> **Status.** Five problems documented from interactive study (HashSet, HashMap,
> one-pass state, bounded heap, sliding window). Next: lock **two pointers** as a
> first-class pattern (3Sum or Container With Most Water).

## Why this exists

You work full-time. DSA is a **secondary** preparation track (~2–3 hours/week). This
handbook optimizes for **high interview ROI**: recognize patterns, reason clearly,
implement clean Java, and discuss trade-offs — without turning into competitive
programming prep.

**Success metric:** Can you walk into a senior interview, see an unfamiliar problem,
stay calm, identify the underlying pattern, and implement a clean solution?

Not: "How many LeetCode problems have I solved?"

You can read the Markdown files in any editor. To browse with **search and a sidebar**, run the local MkDocs site (macOS or Windows).

## Run the handbook locally

**Need:** [Python 3.10+](https://www.python.org/downloads/) (3.12 is fine). Git. A browser.

Confirm Python:

```bash
python3 --version
```

On Windows, if that fails, try `py --version` or `python --version`. Use whichever command works in the steps below (`python3`, `python`, or `py`).

### 1. Clone and enter the repo

```bash
git clone <this-repo-url> dsa-interview-handbook
cd dsa-interview-handbook
```

If you already have the folder, skip clone and `cd` into it.

### 2. Create a virtual environment and install deps

**macOS / Linux**

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

**Windows (Command Prompt)**

```bat
py -m venv .venv
.venv\Scripts\activate.bat
pip install -r requirements.txt
```

**Windows (PowerShell)**

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

If PowerShell blocks the activate script:

```powershell
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
```

Then run `Activate.ps1` again.

### 3. Start the live site

**macOS / Linux**

```bash
mkdocs serve --dev-addr 127.0.0.1:8000
```

**Windows**

```bat
mkdocs serve --dev-addr 127.0.0.1:8000
```

Open **http://127.0.0.1:8000/** in your browser.

The server reloads when you edit Markdown. Stop it with `Ctrl+C`.

Deactivate the venv when you are done: `deactivate`.

### Next time (venv already exists)

**macOS / Linux**

```bash
cd dsa-interview-handbook
source .venv/bin/activate
mkdocs serve --dev-addr 127.0.0.1:8000
```

**Windows (PowerShell)**

```powershell
cd dsa-interview-handbook
.venv\Scripts\Activate.ps1
mkdocs serve --dev-addr 127.0.0.1:8000
```

### Troubleshooting

| Problem | What to do |
| --- | --- |
| `python3` / `py` not found | Install Python 3.10+ and tick **Add python.exe to PATH** on Windows |
| `mkdocs` not found | Activate `.venv` first, then `pip install -r requirements.txt` |
| Port 8000 in use | Use `--dev-addr 127.0.0.1:8001` and open that URL |
| `Activate.ps1` cannot be loaded | `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |
| Site looks empty / 404 | Run `mkdocs serve` from the **repo root** (the folder that contains `mkdocs.yml`) |

## Target roles

- Senior Backend Engineer
- Data Platform Engineer
- Senior Data Engineer
- Distributed Systems Engineer
- Platform Engineer

## Relationship to other preparation

When time is limited, priority order:

```text
Spark / Databricks
        ↓
SQL / Database Internals
        ↓
Distributed Systems
        ↓
System Design
        ↓
DSA  ← this handbook
```

If an interview is scheduled, temporarily increase DSA intensity. Otherwise,
consistency beats volume.

## Learning philosophy

1. **Pattern mastery over memorization** — ~50–60 carefully selected problems, each
   teaching a reusable technique.
2. **Discover, don't dump** — problem → clarifying questions → your thinking → brute
   force → optimization → code → dry run → edge cases.
3. **Senior relevance** — connect patterns to real systems (caching, scheduling,
   streaming, dependency graphs) where it helps.
4. **Sustainable pace** — missed days are fine. Do not inflate workload.

## Repository map

| Path | Purpose |
| --- | --- |
| [`roadmap/`](roadmap/) | Learning order, interview strategy, curated problem index |
| [`fundamentals/`](fundamentals/) | Complexity, arrays, strings, recursion |
| [`patterns/`](patterns/) | High-ROI interview patterns (two pointers, sliding window, …) |
| [`data-structures/`](data-structures/) | Linked lists, trees, graphs, trie, union-find |
| [`algorithms/`](algorithms/) | DFS/BFS, DP, backtracking, shortest path, … |
| [`problems/`](problems/) | Individual problem write-ups (added as we study) |
| [`mock-interviews/`](mock-interviews/) | Timed practice sessions by topic |
| [`revision/`](revision/) | Cheatsheets, common mistakes, interview templates |
| [`progress/`](progress/) | Mastery tracking and revision log |
| [`templates/`](templates/) | Copy-me scaffolds for patterns and problems |
| [`STYLE_GUIDE.md`](STYLE_GUIDE.md) | Document structure contracts |

## Learning roadmap (phases)

| Phase | Focus | Topics |
| --- | --- | --- |
| 1 | Foundations | Complexity, Arrays, Strings, HashMap/HashSet |
| 2 | High-ROI patterns | Two pointers, sliding window, prefix sum, binary search, intervals, stack, heap |
| 3 | Core structures | Linked list, fast/slow pointers, trees, BST, DFS, BFS |
| 4 | Advanced structures | Graphs, topological sort, union-find, trie, shortest path |
| 5 | Techniques | Backtracking, greedy, DP, bit manipulation |
| 6 | Interview mode | Mixed problems, timed practice, mocks, revision |

Full detail: [`roadmap/learning-roadmap.md`](roadmap/learning-roadmap.md).

## Problem count

Target **~50–60 curated problems** across all patterns. See
[`roadmap/problem-index.md`](roadmap/problem-index.md) for the planned list and
status. Problem files appear in [`problems/`](problems/) only after we study them.

## Weekly schedule (2–3 hours)

| Session | Duration | Activity |
| --- | --- | --- |
| 1 | 30–40 min | Learn or revise one pattern |
| 2 | 30–40 min | Solve one problem independently |
| 3 | 30–40 min | Solve a related variation |
| Optional | 30–45 min | Revision or timed problem (weekend) |

## Current progress

Track mastery in [`progress/progress.md`](progress/progress.md). Confidence levels:

`Not Started` → `Learning` → `Practicing` → `Comfortable` → `Interview Ready`

**Solving once ≠ mastery.** Use spaced repetition in [`progress/revision-log.md`](progress/revision-log.md).

| Module | Status |
| --- | --- |
| Module 0 — Complexity | Learning |
| Module 1 — Arrays | Practicing (A1 documented) |
| HashMap / HashSet | Practicing |
| Heap, Sliding Window | Learning (one problem each) |
| Problems documented | 5 / ~60 |

## How to use this handbook

1. **Start here** → [`fundamentals/complexity.md`](fundamentals/complexity.md) (Module 0).
2. **Follow the roadmap** → [`roadmap/learning-roadmap.md`](roadmap/learning-roadmap.md).
3. **Study a pattern** → read the pattern doc, then solve its curated problems from
   the index (problem files added as you go).
4. **Track progress** → update [`progress/progress.md`](progress/progress.md) and
   [`progress/revision-log.md`](progress/revision-log.md).
5. **Before interviews** → [`revision/pattern-cheatsheet.md`](revision/pattern-cheatsheet.md)
   and [`revision/interview-templates.md`](revision/interview-templates.md).

## Mock interview strategy

After completing a major section, run a mock from [`mock-interviews/`](mock-interviews/):

- One problem at a time — pattern not revealed upfront.
- Interviewer asks clarifying questions; hints only when stuck.
- Score reasoning before code (see [`roadmap/interview-strategy.md`](roadmap/interview-strategy.md)).

## Teaching sequence (every problem)

```text
Problem → Clarifying questions → Your thinking → Brute force → Optimization
       → Code → Dry run → Edge cases → Pattern recognition
```

See [`STYLE_GUIDE.md`](STYLE_GUIDE.md) for the full problem and pattern contracts.

## License

Documentation: [CC BY 4.0](LICENSE). Code snippets: MIT.
