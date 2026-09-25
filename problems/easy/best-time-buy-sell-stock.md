---
title: "Best Time to Buy and Sell Stock"
description: One transaction — track running minimum price and running maximum profit in one pass.
status: review
difficulty: easy
pattern: arrays
tags: [arrays, state-tracking, one-pass]
source: leetcode-121
created: 2026-09-07
updated: 2026-09-07
---

# Best Time to Buy and Sell Stock

Studied interactively. The correction that matters: the second state is **max profit so far**, not “max selling price.”

## Problem

`prices[i]` is the price on day `i`. Choose **one** day to buy and a **later** day to sell. Return the maximum profit. If no profitable transaction exists, return `0`.

Examples:

```text
[7, 1, 5, 3, 6, 4] → 5     (buy 1, sell 6)
[7, 6, 4, 3, 1]    → 0
```

## Constraints

Typical: `n` up to ~10⁵.

Why they matter: checking every `(buy, sell)` pair with `buy < sell` is O(n²). One pass is expected.

## Clarifying questions

- One transaction only, or unlimited / at most k?
- Must buy before sell (same day allowed)? Usually **strictly later** day; profit 0 if you “sell” the same day.
- Negative prices? Usually no.
- Empty array? Confirm; often n ≥ 1.

## Think before coding

1. After seeing a prefix of days, what two numbers let me decide everything about that prefix?
2. Why is “minimum so far” not enough by itself?
3. Why is “maximum price so far” the **wrong** second state?

## Brute force

**Intuition:** For every buy day `i`, try every sell day `j > i`; track `prices[j] - prices[i]`.

**Complexity:** Time O(n²). Space O(1).

**Limitations:** Repeats “what was the cheapest buy before today?” for every pair.

Ask: *What information from the past do we actually need?* Only the **minimum price before today**, plus the **best profit already found**.

## Optimized approach

**Pattern:** Running minimum + running best result → **state tracking**.

**Intuition:** Walk left to right. The best buy for a sell **today** is the cheapest price **on or before** today (same-day profit is 0). You do **not** need the global max price — that max might occur **before** the min buy.

**State:**

```text
minBuyingPrice  = minimum price encountered so far
maxProfit       = best profit achievable using prices seen so far
```

For each `currentPrice`:

1. Update `minBuyingPrice`.
2. `currentProfit = currentPrice - minBuyingPrice`.
3. Update `maxProfit`.

**Correctness:** Every possible sell day is considered exactly once, with the best buy in its prefix. If prices only fall, every `currentProfit` is 0.

**Complexity:** Time O(n). Auxiliary space O(1).

## Java implementation

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minBuyingPrice = prices[0];
        int maxProfit = 0;

        for (int currentPrice : prices) {
            minBuyingPrice = Math.min(minBuyingPrice, currentPrice);
            int currentProfit = currentPrice - minBuyingPrice;
            maxProfit = Math.max(maxProfit, currentProfit);
        }

        return maxProfit;
    }
}
```

First-day initialization: `minBuyingPrice = prices[0]`, `maxProfit = 0` is safe for n ≥ 1.

## Dry run

```text
prices = [7, 1, 5, 3, 6, 4]

price  minBuy  profit  maxProfit
7      7       0       0
1      1       0       0
5      1       4       4
3      1       2       4
6      1       5       5
4      1       3       5
```

If you had tracked `maxPrice = 7` from the start, you would never pair buy `1` with sell `6` correctly as “max minus min of whole array” (that would be `7-1=6`, which is **not** a valid buy-then-sell).

## Edge cases

- Strictly decreasing → `0`
- Strictly increasing → last − first
- Single day → `0`
- Min at the end → profit 0 unless an earlier valley had a later peak (min-at-end still allows earlier pairs)

## Alternatives

| Approach | Time | Space | Notes |
| --- | --- | --- | --- |
| All pairs | O(n²) | O(1) | Correct, slow |
| One-pass state | O(n) | O(1) | Interview default |
| Kadane on diffs | O(n) | O(1) | Same idea; max subarray of daily changes, one transaction |

## Interview follow-ups

- Unlimited transactions (`122`) — greedy: sum all positive diffs.
- At most two / k transactions — DP.
- Cooldown, transaction fee.

## How to explain this in an interview

1. **Observation:** Best sell on day `i` uses the min price in `prices[0..i]`.
2. **State:** Running min buy, running max profit — not max price.
3. **Algorithm:** One scan; update min, then profit.
4. **Complexity:** O(n) time, O(1) space.
5. **Tradeoff:** Extra arrays are unnecessary; two scalars are sufficient.

## Common mistakes

- Tracking **max selling price** instead of **max profit**.
- Allowing sell before buy (global max − global min).
- Starting `minBuyingPrice` at `0` when prices can be positive-only — use first price or `Integer.MAX_VALUE`.

## Pattern recognition

```text
Running best state
→ State tracking / prefix-style reasoning
```

> If I see **one pass, need the best so far given a constraint on order (buy before sell)** → keep a **small running state**, not the whole history.

## Real engineering connection

Same shape as: track min latency so far vs current SLO burn; running minimum watermark; one-pass metrics over a time series. You rarely store the full series if two aggregates answer the query.

## Revision notes

```text
Pattern: running min + running max profit
Recognition: one buy, one later sell, maximize profit
Core idea: don't store max price; max price can be before the min buy
Time: O(n)
Space: O(1)
Common mistake: global max − global min
Interview takeaway: small state beats full history
```
