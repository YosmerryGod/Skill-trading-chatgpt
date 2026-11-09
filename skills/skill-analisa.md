---
name: market-analysis-research
description: Analyze historical crypto futures market movements using only price, volume, and Open Interest (OI) to identify observable conditions before and during major price expansions. Use when the user wants to study a symbol over a specified date/time window, compare multiple market cases, or test whether a market behavior repeats.
---

# Market Analysis Research

## Purpose

Study actual historical market data before, during, and after a price expansion using only three core inputs:

1. **Price**
2. **Volume**
3. **Open Interest (OI)**

The goal is to identify repeatable relationships across multiple market samples without adding unsupported narratives or relying on extra indicators.

This skill is for research and market-structure analysis. It does not execute trades, identify private participants, or prove manipulation.

## 1. Confirm the research window

- Confirm exact symbol and contract market (prefer Binance USDⓈ-M perpetual when requested).
- Confirm date, start time, end time, and timezone. Default to WIB (Asia/Jakarta) only when the conversation establishes it; otherwise ask.
- Convert the local window to UTC correctly before requesting exchange data.
- Fetch a lead-in period before the requested start so the analysis includes conditions preceding the move. A practical default is 2–6 hours before the window, adjusted to the event.
- Fetch enough data after the move to see whether the expansion continued, stalled, or reversed when useful.
- Verify the contract existed and data is available for the requested period.

## 2. Data to collect — only three inputs

Use Binance USDⓈ-M historical endpoints where available:

- **Price:** OHLC candles (open, high, low, close) and percentage change. Use 5m for detailed event timing and 15m for overall structure. Use 1h for broader context when useful.
- **Volume:** candle volume for the same timeframes. Compare volume with the token's own recent baseline, preferably the previous 5 completed candles of the same timeframe.
- **Open Interest (OI):** absolute contracts/value and percentage change over the same intervals.

Do not add funding, taker buy/sell, long/short ratios, basis, liquidation data, order-book data, or other indicators to the analysis. The user wants conclusions based only on price, volume, and OI.

Never imply a metric was checked when the endpoint did not return it. Clearly distinguish unavailable historical data from a zero value.

## 2A. Establish volatility and trend context

Before interpreting the market, determine its volatility regime from price history and state the observed trend separately.

- Use a reproducible price-derived measure such as rolling standard deviation of log returns or ATR/range percentage.
- State the formula, timeframe, lookback, baseline window, and whether the estimate is based only on completed candles.
- Classify volatility as low / medium / high / mixed / unclassified using the symbol's own historical distribution or another justified baseline. Do not apply universal thresholds blindly.
- Report both the current/recent volatility regime and how it compares with the lead-in period.
- Classify observed price trend independently as bullish, bearish, sideways, or mixed/unclear.
- Explain whether volatility is contracting, stable, expanding, or transitioning.
- Volatility is context derived from price; it does not replace Price, Volume, and OI and does not establish market direction.

## 3. Structure the event timeline

Break the window into observable phases, for example:

1. Pre-move / compression.
2. Initial downside or local low, if visible.
3. Base / consolidation.
4. First price expansion.
5. Acceleration / high-volume phase.
6. Exhaustion, continuation, or retracement.

For each phase report:

- WIB timestamp.
- Price open/high/low/close and percentage change.
- Volume and its multiple/percentage relative to the stated baseline.
- OI absolute value and percentage change.
- Whether price, volume, and OI rose, fell, or stayed relatively flat together.

Do not use an unfinished candle as if it were closed. Mark it as in-progress.

## 4. Interpret price, volume, and OI correctly

- Rising OI means the number/value of open contracts increased; it does not identify whether the added exposure is long or short. Every futures contract has both sides.
- Falling OI means open contracts decreased; it does not by itself prove short covering or long liquidation.
- Price rising while OI rises means open contracts increased during the price rise. It does not reveal who opened them or their intent.
- Price rising while OI falls means open contracts decreased during the price rise. Do not automatically label it a short squeeze.
- Price falling while OI rises means open contracts increased during the decline; it does not identify which side initiated the positions.
- Price falling while OI falls means open contracts decreased during the decline; do not automatically label it long liquidation.
- Volume expansion shows increased trading activity, not buying pressure by itself.
- Read the three inputs together and compare their timing. Do not treat one metric in isolation as proof of direction or intent.
- Compare volume against the same token's recent baseline. Do not compare raw volume across different tokens as if the values were directly equivalent.

## 5. Evidence discipline

Separate every conclusion into:

- **Observed data:** directly returned price, volume, and OI values.
- **Interpretation:** what the combination and timing of those observations may indicate.
- **Unknown / not proven:** what these three inputs cannot establish.

Never claim market-maker accumulation, whale buying, stop hunting, spoofing, wash trading, coordinated manipulation, or a short squeeze based only on price, volume, and OI. These inputs cannot identify participants or prove intent.

Avoid causal language such as "this caused the pump" unless the evidence supports causation. Prefer phrasing such as "occurred before", "coincided with", or "is consistent with".

## 6. Compare multiple market cases

Maintain a consistent comparison table across samples:

- Price behavior before and during expansion.
- Whether volume expanded relative to its own baseline.
- Whether OI decreased, stayed flat, or increased before expansion.
- Whether OI increased or decreased during price and volume expansion.
- Whether price, volume, and OI changes occurred at the same time or in separate phases.
- What price did after the expansion: continued, stalled, or retraced.

Do not declare a reliable pattern from only two or three examples. Record counterexamples and differences. A pattern is stronger when it repeats across independent samples and timeframes.

## 7. Standard response format

### [SYMBOL] — [DATE], [START–END TIMEZONE]

**Market context**
- Volatility level/regime, formula, timeframe, lookback, and historical baseline.
- Whether volatility is contracting, stable, expanding, or transitioning.
- Observed trend direction (bullish / bearish / sideways / mixed).

**Price summary**
- Start/end close.
- Period high/low.
- Percentage change.

**Volume summary**
- Volume during the key phases.
- Comparison with the token's recent baseline.
- Time of the strongest volume expansion.

**OI summary**
- Starting and ending OI.
- Highest/lowest OI in the window when relevant.
- Percentage change and timing relative to price movement.

**Timeline**
A chronological table with timestamp, price change, volume, OI, and the relationship between the three.

**What the data shows**
List only direct observations from price, volume, and OI.

**Possible interpretation**
Explain plausible readings of how the three inputs interacted, without overstating certainty.

**What cannot be concluded**
State clearly that these inputs do not identify participant intent or prove manipulation, accumulation, liquidation, or a squeeze.

**Comparison with prior samples**
Update the shared pattern table using only price, volume, and OI. Preserve earlier observations and include counterexamples.

## 8. Research discipline and user interaction

- Respond in Bahasa Indonesia by default.
- Always establish volatility level and observed trend direction before interpreting the Price, Volume, and OI relationship.
- Be concise but include enough figures for the user to audit the conclusion.
- If the user provides a specific symbol and historical time window, analyze that exact window; do not substitute a current-market scan.
- Keep the same metric definitions and timeframes across market cases wherever possible.
- When the user says "lanjut analisa", continue the multi-market research rather than jumping straight to a live trade recommendation.
- Do not turn a historical research request into an entry recommendation unless the user asks for a trading plan.
- When the user asks to compare cases, explicitly distinguish common patterns from differences.
- Do not introduce additional indicators or derivatives metrics. The analysis must stay limited to price, volume, and OI.
- Preserve uncertainty. The purpose is to learn from the data, not to confirm a preconceived theory.

## 9. Current cross-market finding (provisional)

Record this finding from the first three analyzed samples: INITUSDT, PIEVERSEUSDT, and EDGEUSDT.

**Most consistent observation so far:** OI increased alongside price and volume expansion.

### How to use this finding

- Treat the OI + price + volume relationship as the leading recurring observation to test in future samples.
- Do not treat it as a proven predictive signal or a cause of price expansion.
- In each new market analysis, explicitly check whether OI rose during the same interval as price and volume expansion, and quantify the changes against the pre-expansion baseline.
- Keep recording counterexamples. Update this finding only when additional independent market samples support or contradict it.

This is a provisional observation based on only three markets, not a statistically validated trading rule.
