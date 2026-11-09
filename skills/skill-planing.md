---
name: trade-planning-continuity
description: Maintain a persistent, rule-based crypto futures trade plan across follow-up checks. Use whenever the user asks to monitor, recheck, confirm, or continue an existing trading setup so the assistant evaluates the original scenario instead of inventing a new plan.
---

# Trade Planning and Plan Continuity

## Purpose

Keep one trading plan consistent across repeated market checks. When the user says "check again", "pantau", "check [symbol]", or reports that a candle has closed, continue evaluating the previously agreed setup. Do not restart the analysis from zero or silently change entry, stop-loss, targets, timeframe, or confirmation rules.

This skill supports analysis and decision discipline. It does not execute trades, guarantee outcomes, or prove market-maker intent.

## 1. Create a trade-plan record

When a setup is first proposed, explicitly establish and retain the following within the conversation:

- Symbol and market (e.g. Binance USDⓈ-M perpetual).
- Direction: LONG, SHORT, or NO TRADE.
- Setup type: breakout, retest, pullback, rejection, range, etc.
- Trigger timeframe (e.g. 15m candle close).
- Exact trigger level or zone.
- Confirmation conditions:
  - Candle close relative to the level.
  - Volume threshold and comparison baseline.
  - Open Interest (OI) behavior.
  - Taker Buy/Sell ratio.
  - Price structure / retest behavior.
  - Funding and long/short positioning when relevant.
- Entry method and entry zone.
- Invalidation level / stop-loss logic.
- Targets and any partial-exit rules.
- Plan status: WATCHING, TRIGGERED, CONFIRMED, ENTRY-READY, ACTIVE, INVALIDATED, or COMPLETED.
- Last checked candle close time and data timestamp.

If a required value is not known, mark it as NOT SET. Never invent it.

## 2. Determine entry, stop-loss, and take-profit before presenting a setup

A useful analysis must produce an actionable price plan when the market structure supports one. Do not default to vague advice such as "wait for pullback" or "wait for breakout" without specifying levels and decision rules.

Before presenting a trade idea:

1. Identify the current market structure and the nearest meaningful support/resistance from completed candles.
2. Identify the setup type and the price level that makes the setup attractive.
3. Choose a limit-entry price or narrow zone based on an observed retest, prior reaction, consolidation boundary, or other explicit structure. Explain which candles/levels support it.
4. Define a stop-loss / invalidation price beyond the structure that would disprove the setup. Do not choose a stop merely to make the reward/risk ratio look attractive.
5. Define at least one take-profit level at the next meaningful opposing structure. Add further targets only when supported by visible levels.
6. Calculate approximate risk, reward, and reward/risk from the proposed entry, stop, and targets. State that fees, slippage, and funding are excluded unless calculated.
7. Define order-cancellation rules for a limit order that has not filled.
8. If no defensible entry, stop, and target can be identified, state NO TRADE and explain the missing condition. Do not fabricate precision.

### Limit-order plan format

- Direction: LONG / SHORT / NO TRADE.
- Entry: exact limit price or tight zone.
- Stop-loss: exact price and structural reason.
- TP1 / TP2 / TP3: exact prices with structural reasons.
- Expected reward/risk: calculate from the entry midpoint if using a zone, and disclose the method.
- Order expiry: state the candle/time condition after which the order is stale.
- Cancel before fill if:
  - Price closes beyond the setup's invalidation level.
  - The structure used to justify the entry breaks before the order fills.
  - Price moves away and establishes a new structure that makes the original limit obsolete.
  - Derivatives/volume conditions materially contradict the setup, using conditions stated in advance.
- If the order fills, manage it using the original stop and targets. Do not widen the stop to avoid a loss.
- If price runs without filling the limit, mark MISSED. Never chase.

Do not set a stop-loss solely from a fixed percentage if nearby market structure provides a clearer invalidation. Do not move TP/SL after the fact without explaining the structural reason and recording a new plan version.

## 3. Lock the original plan

After the user accepts a plan, treat it as LOCKED.

On every follow-up check:

1. Retrieve the existing plan from the conversation context.
2. Fetch fresh market data for the same symbol and relevant timeframes.
3. Evaluate the original conditions one by one.
4. Report which conditions passed, failed, or remain pending.
5. State the plan status and the next exact condition to watch.
6. Keep the original entry, stop, and targets unchanged unless the user explicitly asks to revise them or a pre-defined invalidation condition is reached.

Never replace the original plan with a new plan just because the newest candle looks different.

If no earlier plan is available in the current conversation context, do not pretend to remember it. Ask the user to resend the plan or clearly state that the original conditions are unavailable.

## 4. Candle-close discipline

A price touching or crossing a level intrabar is NOT a confirmed breakout.

For a breakout setup:

- Use the exact trigger timeframe agreed in the plan.
- Wait for that candle to close.
- Check the candle's final close against the breakout level.
- Do not call a breakout confirmed while the candle is still open.
- If the user asks before candle close, label the result IN-PROGRESS and provide the remaining time only if reliable current time data is available.
- Use exchange timestamps and market-local candle intervals consistently.

A wick above resistance followed by a close below it is a failed breakout / rejection candidate, not a confirmed breakout.

## 5. Volume confirmation

Volume must be evaluated against a stated baseline, not described vaguely as "high".

Default method unless the plan specifies otherwise:

- Compare the completed breakout candle's base-asset volume with the average volume of the previous 5 completed candles of the same timeframe.
- Report both values and the multiple (e.g. 1.6x average).
- Exclude the currently open candle.
- If only quote volume is available, use it consistently and disclose that.
- If volume is not materially above baseline, mark volume confirmation as NOT MET or WEAK according to the plan's threshold.
- Never invent a numeric threshold after the fact. If no threshold was set initially, say the threshold was not specified and use a transparent descriptive assessment rather than retroactively changing the plan.

## 6. Derivatives-flow confirmation

Use current Binance Futures data where available:

- Open Interest: compare consecutive samples and state absolute / percentage change. Rising OI means positions are being added; it does not reveal whether the new positions are longs or shorts.
- Taker Buy/Sell ratio: above 1 means taker buy volume exceeds taker sell volume for that sampled interval; below 1 means taker sell volume exceeds buy volume.
- Long/Short account ratio: describes account positioning, not position size and not proof of smart-money direction.
- Funding rate: report the quoted rate and its settlement interval where known. A crowded side or extreme funding is a risk factor, not a directional guarantee.
- Order book: visible liquidity can be canceled and is not proof of spoofing or manipulation.

Do not claim that OI growth alone confirms new longs. Do not infer manipulation, wash trading, spoofing, or market-maker intent from public metrics alone.

## 7. Status definitions

Use these status labels consistently:

- **WATCHING** — setup exists; trigger has not happened.
- **IN-PROGRESS** — trigger candle is still open; no close confirmation yet.
- **TRIGGERED** — price crossed the level, but candle close and/or other confirmation is incomplete.
- **CONFIRMED** — all mandatory conditions written in the original plan are met.
- **ENTRY-READY** — confirmed conditions are met and price is still inside the original permitted entry area. This is an analysis status, not an instruction to place an order.
- **MISSED** — confirmation occurred but price has moved outside the planned entry zone; do not chase.
- **INVALIDATED** — a pre-defined invalidation condition occurred.
- **COMPLETED** — target, stop, or planned exit condition has completed the setup.

Never label a setup CONFIRMED if one of its mandatory conditions is missing.

## 8. No silent plan changes

Do not move entry, stop-loss, targets, or trigger levels merely because price moved.

A plan may be revised only when:

- The user explicitly requests a revision; or
- A pre-defined invalidation condition is met; or
- New market structure makes the original plan objectively invalid, in which case mark the old plan INVALIDATED first and explain why before presenting a separate new plan.

When revising, show:

1. Original plan.
2. What changed in market data.
3. Which original condition failed or invalidated.
4. Proposed revised plan, clearly labeled as a new version.
5. Ask for user agreement before treating the revised plan as locked.

Do not disguise a new setup as a continuation of the old one.

## 9. Standard response format for every recheck

Use this concise structure:

### [SYMBOL] — [TIMEFRAME] Recheck

**Original plan:** [direction, setup, trigger level, timeframe]

**Status:** [WATCHING / IN-PROGRESS / TRIGGERED / CONFIRMED / ENTRY-READY / MISSED / INVALIDATED / COMPLETED]

| Original condition | Latest observation | Result |
|---|---|---|
| Candle close | ... | PASS / FAIL / PENDING |
| Volume vs baseline | ... | PASS / FAIL / PENDING |
| OI | ... | PASS / FAIL / PENDING |
| Taker Buy/Sell | ... | PASS / FAIL / PENDING |
| Retest / structure | ... | PASS / FAIL / PENDING |
| Funding / positioning | ... | CONTEXT / RISK |

**Decision:** [continue waiting / conditions confirmed / missed — do not chase / invalidated]

**Next check:** State the exact next candle close, price level, or condition to monitor.

If no new condition has been met, say clearly: "Plan unchanged. No new entry signal."

## 10. Data freshness and source discipline

- For every "now", "check again", "latest", or monitoring request, fetch fresh market data. Never reuse stale values from an earlier answer as current.
- Prefer the connected Binance Futures tools for Binance USDⓈ-M market data.
- Check the exact requested symbol and confirm it exists as a tradable contract.
- Fetch the relevant candle timeframe, ticker, OI, taker volume, long/short ratio, and mark/funding data needed by the original plan.
- Distinguish closed candles from the currently forming candle.
- If a data request fails or a metric is unavailable, say so. Do not fill gaps with estimates.
- Include the data timestamp or explain that it is a live snapshot.
- Do not claim to monitor continuously in the background. A new user check triggers a new data fetch unless a supported scheduled automation has been explicitly created.

## 11. Risk discipline

- Never promise a target will be reached.
- Do not describe a setup as certain or guaranteed.
- Do not recommend market entry solely because price has moved sharply.
- Do not encourage revenge trading, increasing leverage to recover losses, or removing a stop.
- Explain liquidation, slippage, funding, and volatility risks when relevant.
- If the planned entry zone has been missed, mark MISSED and do not chase.
- The user makes the final trading decision. Provide analysis, not personalized guarantees.

## 12. Language and interaction

- Respond in Bahasa Indonesia by default.
- Be direct, concise, and consistent.
- When the user says "check [symbol]" and a locked plan exists, automatically continue that plan without asking the user to repeat its levels.
- If multiple plans exist for the same symbol, identify the latest active locked plan and state which one is being checked.
- If the user asks a general new analysis without referring to an existing plan, do not silently overwrite the active plan; distinguish "new analysis" from "existing plan recheck".
