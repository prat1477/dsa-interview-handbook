---
title: "Longest Substring Without Repeating Characters"
description: Sliding window — expand right, shrink left with while until the window has unique characters.
status: review
difficulty: medium
pattern: sliding-window
tags: [strings, sliding-window, hashset]
source: leetcode-3
created: 2026-09-07
updated: 2026-09-07
---

# Longest Substring Without Repeating Characters

Studied interactively. Substring means **contiguous**. Nested `for` + `while` is still O(n) when both pointers only move forward.

## Problem

Given a string `s`, return the length of the longest **substring** with all unique characters.

Examples:

```text
"abcabcbb" → 3    ("abc")
"bbbbb"    → 1
"pwwkew"   → 3    ("wke")
```

## Constraints

Typical: `n` up to ~10⁵; characters may be ASCII or a larger alphabet.

Why they matter: try-every-substring is O(n²) or worse. Alphabet size affects **space**, not the pointer argument for time.

## Clarifying questions

- Substring (contiguous) vs subsequence?
- Empty string → `0`?
- Character set (lowercase only vs Unicode)?
- Return the substring or only its length?

## Think before coding

1. When a duplicate appears at `right`, do I restart from scratch?
2. Can I shrink from the left until the window is valid again?
3. Why might a single `if` (not `while`) fail?
4. If I write `left++` then `remove(s.charAt(left))`, which character did I remove?

## Brute force

**Intuition:** For every start index, grow a `HashSet` forward until a duplicate; record length.

**Complexity:** Time O(n²) — many characters are scanned from many starts. Space O(min(n, alphabet)).

**Bottleneck:** Restarting the scan discards a still-valid suffix of the previous window.

Ask: *When a duplicate appears, don't restart the entire scan. Can we maintain a window?*

## Optimized approach

**Pattern:** Contiguous range + constraint + longest valid window → **sliding window**.

**Window:** `[left, right]` always contains **unique** characters (the invariant).

- `right` expands (for-loop).
- On duplicate, `left` shrinks until the new character can enter.
- Track `max = right - left + 1` after each valid expansion.

**Why `while`, not `if`:** One removal may not clear the duplicate. Example `A B C B`: after removing `A`, `B` is still in the set.

```java
while (seen.contains(current)) {
    seen.remove(s.charAt(left));
    left++;
}
```

**Pointer complexity:** `right` moves ≤ n times; `left` moves ≤ n times; never backward. Nested loops still **O(n)**.

**Bug (from study):** Remove **then** increment.

```java
// wrong — skips the old left character
left++;
seen.remove(s.charAt(left));

// correct
seen.remove(s.charAt(left));
left++;
```

**Complexity:** Time O(n). Space O(n) in the general alphabet case. If the alphabet is fixed (e.g. 26 lowercase letters), space is O(1) in that alphabet — for the general problem, say O(n).

## Java implementation

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> seen = new HashSet<>();
        int max = 0;
        int left = 0;

        for (int right = 0; right < s.length(); right++) {
            while (seen.contains(s.charAt(right))) {
                seen.remove(s.charAt(left));
                left++;
            }
            seen.add(s.charAt(right));
            max = Math.max(max, right - left + 1);
        }

        return max;
    }
}
```

**Variation (not required here):** `Map<Character, Integer>` last-seen index can jump `left` in one assignment; still O(n). The while-shrink version makes the invariant obvious.

## Dry run

```text
s = A B C B
    0 1 2 3

R=0 A  set={A}           window A     max=1
R=1 B  set={A,B}         window AB    max=2
R=2 C  set={A,B,C}       window ABC   max=3
R=3 B  B in set
       remove A, left=1  set={B,C}    still B
       remove B, left=2  set={C}
       add B             set={C,B}    window CB  max=3
```

```text
input          pointer/state     structure     result
"abcabcbb"     L,R expand/shrink HashSet       max length
```

## Edge cases

- Empty string → `0`
- All unique → `n`
- All same character → `1`
- Duplicate at the start of the window vs in the middle — `while` covers both

## Alternatives

| Approach | Time | Space | Notes |
| --- | --- | --- | --- |
| Restart HashSet each start | O(n²) | O(n) | Correct, slow |
| Sliding window + HashSet | O(n) | O(n) or O(alphabet) | Default |
| Last-index map, jump left | O(n) | O(alphabet) | Fewer inner-loop steps |

## Interview follow-ups

- Longest substring with **at most k distinct** characters.
- Minimum window covering a target (harder shrink rule).
- Stream of characters; emit current longest unique window.

## How to explain this in an interview

1. **Observation:** Longest **contiguous** unique-character span.
2. **Data structure:** HashSet of chars in `[left, right]`.
3. **Algorithm:** Expand right; while invalid, drop `s[left]` and `left++`; then add and update max.
4. **Complexity:** O(n) time because both pointers move forward at most n times; space O(n) general.
5. **Tradeoff:** `if` vs `while` — `while` until the invariant holds.

## Common mistakes

- Treating subsequence as substring.
- `if` instead of `while` when shrinking.
- Increment `left` before removing `s.charAt(left)`.
- Calling nested loops O(n²) without checking monotonic pointers.

## Pattern recognition

```text
Contiguous sequence
+ constraint on the current window
+ longest / shortest valid window
→ Sliding Window

right  → expand
left   → shrink when invalid
state  → track window condition
result → track best window
```

> If I see **contiguous + uniqueness / budget / sum constraint + best length**, think sliding window.

## Real engineering connection

Same skeleton as: events in a time window, rate limiting (count in last T seconds), streaming “unique keys in current buffer.” The JVM set is the **window state**, not a distributed log.

## Revision notes

```text
Pattern: sliding window + HashSet
Recognition: longest substring (contiguous) with unique chars
Core idea: invariant [L,R] unique; while-shrink; remove then left++
Time: O(n) even with nested while (monotonic pointers)
Space: O(n) general alphabet
Common mistake: if not while; left++ before remove
Interview takeaway: nested loops ≠ O(n²) if pointers never go backward
```
