---
name: market-analysis-research
description: Analyze historical crypto futures market movements to identify observable conditions before and during major price expansions. Use when the user wants to study a symbol over a specified date/time window, compare multiple market cases, or test whether a market behavior repeats.
---

# Market Analysis Research

## Purpose

Study actual historical market data before, during, and after a price expansion. The goal is to build evidence across multiple market samples, not to force a market-maker or smart-money narrative onto incomplete public data.

This skill is for research and market-structure analysis. It does not execute trades, identify private participants, or prove manipulation.

## 1. Confirm the research window

- Confirm exact symbol and contract market (prefer Binance USDⓈ-M perpetual when requested).
- Confirm date, start time, end time, and timezone. Default to WIB (Asia/Jakarta) only when the conversation establishes it; otherwise ask.
- Convert the local window to UTC correctly before requesting exchange data.
- Fetch a lead-in period before the requested start so the analysis includes conditions preceding the move. A practical default is 2–6 hours before the window, adjusted to the event.
- Fetch enough data after the move to see whether the expansion continued, stalled, or reversed when useful.
- Verify the contract existed and data is available for the requested period.

## 2. Data to collect

Use Binance USDⓈ-M historical endpoints where available:

- OHLCV candles: 5m for detailed event timing and 15m for the overall structure. Use 1h for broader context when useful.
- Open Interest (OI): absolute contracts/value and percentage changes.
- Taker Buy/Sell volume: buy volume, sell volume, and ratio.
- Long/Short account ratio: long account share, short account share, and ratio.
- Funding history: exact funding rate and funding timestamps.
- Mark/index price or basis when relevant and available.
- Liquidation history, order-book history, or top-trader positioning only when a valid historical source exists.

Never imply a metric was checked when the endpoint did not return it. Clearly distinguish unavailable historical data from a zero value.

## 3. Structure the event timeline

Break the window into observable phases, for example:

1. Pre-move / compression.
2. Initial downside or liquidity sweep, if visible.
3. Base / consolidation.
4. First price expansion.
5. Acceleration / high-volume phase.
6. Exhaustion, continuation, or retracement.

For each phase report:

- WIB timestamp.
- Price open/high/low/close and percentage change.
- Volume relative to a stated baseline, preferably the previous 5 completed candles of the same timeframe.
- OI absolute and percentage change.
- Taker buy/sell ratio and which side was more aggressive.
- Long/short account distribution.
- Funding context.

Do not use an unfinished candle as if it were closed. Mark it as in-progress.

## 4. Interpret derivatives data correctly

- Rising OI means open contracts increased; it does not identify whether the added exposure is long or short. Every futures contract has both sides.
- Falling OI means open contracts decreased; it does not by itself prove short covering or long liquidation.
- Price rising while OI rises is consistent with new positions being added during the rise, but direction and participant identity remain unknown.
- Price rising while OI falls is consistent with position reduction/deleveraging during the rise; do not automatically label it a short squeeze without liquidation evidence.
- Taker Buy/Sell ratio above 1 means taker buy volume exceeded taker sell volume in that sample. Below 1 means taker sell volume exceeded taker buy volume.
- Long/Short account ratio measures account counts/shares, not position size or capital weight.
- Positive funding means longs pay shorts under the quoted convention; negative funding means shorts pay longs. Funding is context, not a directional signal by itself.
- Basis and premium can help show whether perpetual price traded above or below index/mark, but do not prove manipulation.

## 5. Evidence discipline

Separate every conclusion into:

- **Observed data:** directly returned by the exchange endpoints.
- **Interpretation:** what the combination of observations may indicate.
- **Unknown / not proven:** what the available data cannot establish.

Never claim market-maker accumulation, whale buying, stop hunting, spoofing, wash trading, coordinated manipulation, or a short squeeze without specific evidence. Public aggregate data generally cannot identify who opened a position or why.

Avoid causal language such as "this caused the pump" unless the evidence supports causation. Prefer phrasing such as "occurred before", "coincided with", or "is consistent with".

## 6. Compare multiple market cases

Maintain a consistent comparison table across samples:

- Did OI decrease before expansion?
- Did OI increase during price expansion?
- Did volume expand relative to baseline?
- Was taker flow persistently buy- or sell-dominant?
- Was funding positive, negative, or near neutral?
- Were long or short accounts dominant, and did their share change?
- Was there observable liquidation evidence?
- What was the price behavior after expansion?

Do not declare a reliable pattern from only two or three examples. Record counterexamples and differences. A pattern is stronger when it repeats across independent samples and timeframes.

Do not compare raw volume across different tokens without normalizing or contextualizing it. Compare each token against its own recent baseline.

## 7. Standard response format

### [SYMBOL] — [DATE], [START–END TIMEZONE]

**Price summary**
- Start/end close.
- Period high/low.
- Percentage change.

**Timeline**
A chronological table with price, volume, OI, taker flow, and key events.

**Derivatives positioning**
Summarize OI, long/short accounts, funding, and basis if available.

**What the data shows**
List only direct observations.

**Possible interpretation**
Explain plausible readings without overstating certainty.

**What cannot be concluded**
State missing evidence and unknown participant intent.

**Comparison with prior samples**
Update the shared pattern table without rewriting earlier observations.

## 8. Research discipline and user interaction

- Respond in Bahasa Indonesia by default.
- Be concise but include enough figures for the user to audit the conclusion.
- If the user provides a specific symbol and historical time window, analyze that exact window; do not substitute a current-market scan.
- Keep the same metric definitions and timeframes across market cases wherever possible.
- When the user says "lanjut analisa", continue the multi-market research rather than jumping straight to a live trade recommendation.
- Do not turn a historical research request into an entry recommendation unless the user asks for a trading plan.
- When the user asks to compare cases, explicitly distinguish common patterns from differences.
- Preserve uncertainty. The purpose is to learn from the data, not to confirm a preconceived theory.


## 9. Current cross-market finding (provisional)

Record this finding from the first three analyzed samples: INITUSDT, PIEVERSEUSDT, and EDGEUSDT.

**Most consistent observation so far:** Open Interest (OI) increased alongside price and volume expansion.

**Funding and long/short account dominance did not show the same consistent pattern** across the three samples:
- INITUSDT had negative funding and short-account dominance.
- PIEVERSEUSDT had positive funding and long-account dominance.
- EDGEUSDT had positive funding and long-account dominance.

### How to use this finding

- Treat the OI + price + volume relationship as the leading recurring observation to test in future samples.
- Do not treat it as a proven predictive signal or a cause of price expansion.
- Do not require funding to be negative or positive as a universal condition.
- Do not require long accounts or short accounts to dominate as a universal condition.
- Keep recording counterexamples. Update this finding only when additional independent market samples support or contradict it.
- In each new market analysis, explicitly check whether OI rose during the same interval as price and volume expansion, and quantify the changes against the pre-expansion baseline.

This is a provisional observation based on only three markets, not a statistically validated trading rule.
