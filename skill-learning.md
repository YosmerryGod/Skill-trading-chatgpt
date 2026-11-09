---
name: cross-market-learning
description: Learn from historical crypto market data across multiple symbols, discover recurring pre-expansion and expansion patterns, compare similarities and differences, and recommend which measurable indicators belong in the market-analysis workflow.
---

# Cross-Market Learning

## Purpose

Learn from actual market data across different tokens and different dates. The objective is to discover which conditions repeatedly appear before or during significant price movements, distinguish useful recurring patterns from coincidences, and produce a concise evidence-based recommendation for which indicators should be included in `skill-analisa.md`.

This skill is a research and learning process, not a trade execution system. Never force every market into the same pattern.

## 1. Learning principles

- Data comes before interpretation. Never decide the expected pattern before inspecting the market data.
- Compare multiple independent markets and multiple events, not several time windows from one token as if they were independent samples.
- Study both successful expansions and failed attempts, breakdowns, sideways markets, and cases where the expected pattern did not appear.
- Record similarities and differences. A difference is useful information, not something to ignore.
- Do not confuse correlation with causation or a recurring observation with a proven predictive signal.
- Do not invent missing data. Mark unavailable values as unavailable.
- Keep raw observations separate from calculated features and interpretations.
- Preserve the exact timeframe, timezone, contract type, and data source for every sample.

## 2. Build a consistent market dataset

For every sample, record:

- Symbol and contract type.
- Date and exact time window, including timezone.
- Timeframe used (for example 5m, 15m, or 1h).
- Event classification: strong rise, strong fall, failed breakout, consolidation, or other clearly defined behavior.
- Price OHLC and percentage changes.
- Volume per candle and comparison with the same symbol's recent baseline.
- Open Interest (OI), absolute change, and percentage change.
- Lead-in period before the event and follow-through period after it.

Use consistent definitions and comparable timeframes across samples. Normalize volume and other scale-dependent values against each token's own history rather than comparing raw values between tokens.

## 3. Break each event into phases

Use the same event structure where applicable:

1. Pre-event: conditions before the significant move.
2. Compression/base: price range narrows or consolidates, if present.
3. Initial movement: first meaningful move out of the prior range.
4. Expansion: price movement becomes larger or faster.
5. Peak/exhaustion: movement slows, reverses, or loses participation.
6. Follow-through: continuation, retracement, or full failure after the initial move.

For each phase, document price, volume, and OI behavior. Note the order in which changes appear. Timing matters: a metric that changes only after the move is underway may describe confirmation rather than an early condition.

Do not force an event into all six phases if the data does not show them.

## 4. Discover recurring patterns

For each new sample, compare it with previous samples using questions such as:

- Did volume contract or expand before the move?
- Did OI contract, remain stable, or expand before the move?
- Did price, volume, and OI change together or at different times?
- Did the same sequence appear in other tokens?
- How often did the sequence appear in events that expanded?
- How often did it also appear when price failed to expand?
- Did the pattern remain visible on more than one timeframe?
- What happened after the initial move?

Describe patterns as observable sequences, for example:

- Price range narrows → volume declines → OI changes → price and volume expand.
- Price rises → volume expands → OI rises during the same interval.
- Price rises while OI falls.
- Volume spikes but price makes little progress.
- OI rises while price remains range-bound, followed by either expansion or continued consolidation.

These are pattern candidates to test, not assumptions or automatic trading signals.

## 5. Evaluate whether a pattern is useful

For each candidate pattern, record:

- Number of independent samples where it appeared.
- Number of expansion events where it appeared.
- Number of failed or non-expansion events where it also appeared.
- Whether it appeared before the move or only after the move started.
- Whether the pattern repeated across different tokens.
- Whether it repeated across different timeframes.
- Whether the observation survives comparison against counterexamples.

Avoid claiming statistical reliability from a small sample. If the dataset is small, explicitly label the finding as preliminary.

Do not select a pattern solely because it explains a famous or unusually large pump. Include ordinary market behavior and failed setups to reduce hindsight bias.

## 6. Indicator selection for skill-analisa.md

The learning process must recommend indicators based on evidence from the accumulated samples. Do not add indicators just because they are popular.

### Starting core indicators

Keep these as the baseline in `skill-analisa.md`:

1. **Price action:** OHLC, percentage change, range, swing highs/lows, and the timing of expansion.
2. **Volume:** candle volume, relative volume versus the same token's recent baseline, and volume changes across event phases.
3. **Open Interest (OI):** absolute OI, percentage change, and timing relative to price and volume.

### Candidate indicators to evaluate

Only evaluate additional indicators when reliable historical data is available and the feature addresses a clear question:

- **Relative Volume (RVOL):** whether activity is unusually high compared with the token's own recent baseline.
- **Price range / candle expansion:** whether candle ranges expand before or during a move.
- **Volume-to-price response:** whether increased volume produces meaningful price progress or little movement.
- **OI percentage change:** whether open contracts are building or declining relative to a consistent baseline.
- **OI change relative to volume:** whether OI expansion is large or small compared with trading activity, using a consistent calculation and interpretation.
- **Volatility / ATR:** whether volatility is contracting before expansion or expanding during the event.
- **VWAP or moving averages:** only if testing shows they add repeatable information beyond raw price, volume, and OI.

These are candidates, not mandatory indicators. Do not assume any candidate is useful before testing it against multiple events and counterexamples.

### Promotion rules

Recommend adding a candidate to `skill-analisa.md` only when:

- Its definition and calculation are unambiguous.
- Historical data is consistently available.
- It adds information not already captured by existing indicators.
- It appears repeatedly across independent samples.
- Its timing is useful for the stated research purpose.
- It has been checked against failed moves and counterexamples.
- Its limitations and false-positive behavior can be explained.

If evidence is weak, keep it in the candidate list and do not add it to the core analysis method.

When recommending a change, provide:
- Indicator name and exact calculation/definition.
- What market behavior it is intended to measure.
- Which samples support it.
- Which samples contradict it or show false positives.
- Whether it is a leading observation, confirmation, or context only.
- A clear recommendation: ADD, KEEP TESTING, or REJECT.

Do not silently modify `skill-analisa.md`. Present the evidence-based recommendation first; update that skill only when the user asks.

## 7. Cross-market learning log

Maintain a compact table that is updated after every new sample:

| Pattern / feature | Samples supporting | Counterexamples | Current confidence | Decision |
|---|---:|---:|---|---|
| Price + volume + OI expansion | Record count | Record count | Preliminary / moderate / strong | Keep testing |
| Candidate feature A | Record count | Record count | Preliminary / moderate / strong | Add / test / reject |

Confidence labels are qualitative, not statistical guarantees:

- **Preliminary:** only a few independent examples or incomplete counterexample testing.
- **Moderate:** repeated across several independent tokens/events with some counterexample review.
- **Strong:** repeated across a larger and varied dataset, with clear definitions and systematic failure-case testing. Do not use this label casually.

Keep the actual sample symbols and dates beside the table or in a sample log so each conclusion can be audited.

## 8. Current starting hypothesis

The first three reviewed cases were INITUSDT, PIEVERSEUSDT, and EDGEUSDT.

The provisional shared observation was that OI increased alongside price and volume expansion. This is only a starting hypothesis from three samples.

For future learning:

- Test whether this relationship repeats in additional independent markets.
- Check whether OI begins rising before the price expansion or only during/after it.
- Measure volume relative to each token's own baseline.
- Record cases where price and volume expand but OI does not rise.
- Record cases where OI and volume rise but price does not expand.
- Do not treat the relationship as a proven entry signal or causal explanation.

## 9. Standard learning report

After analyzing a new sample, report:

### Sample added
Symbol, contract, date, timezone, timeframe, and event type.

### Observed sequence
Chronological price, volume, and OI behavior, with key values.

### Similarities with prior markets
Only patterns supported by direct comparison.

### Differences and counterexamples
What did not repeat and why it matters.

### Pattern status
New candidate, repeated observation, weakened hypothesis, or rejected pattern.

### Indicator review
Which existing indicators were useful and which candidate indicators deserve further testing.

### Recommendation for skill-analisa.md
List indicators as:
- **KEEP:** already useful and supported.
- **ADD:** evidence supports including it in the standard analysis.
- **TEST:** needs more samples.
- **REJECT:** did not add reliable information or created misleading conclusions.

### Updated cross-market summary
A concise summary of what has been learned so far, sample count, and remaining uncertainty.

## 10. Interaction rules

- Respond in Bahasa Indonesia by default.
- When the user says "belajar dari data", use this cross-market comparison workflow.
- When the user gives a new symbol and time window, analyze that exact sample and compare it with prior cases.
- When the user says "apa pola yang sama?", focus on repeated sequences and quantify them where possible.
- When the user asks "indicator apa yang harus dipakai?", rank indicators by evidence and usefulness, not popularity.
- Keep the historical learning process separate from live trade planning.
- Never fabricate historical values, sample counts, or confidence.
- Do not claim the skills load automatically into ChatGPT; treat these files as the documented workflow to follow.
