---
name: price-volume-oi-market-classification
description: Classify observable crypto market conditions using price, volume, and Open Interest (OI), with explicit evidence, transition criteria, and uncertainty labels.
---

# Price, Volume, and OI Market Classification

## Purpose

Provide a consistent vocabulary for describing market conditions using only price, volume, and Open Interest (OI).

Classification describes observed behavior. It does not identify who is trading, prove accumulation or distribution, or guarantee the next price movement.

## 1. Approved inputs

Use only:
- Price OHLC, percentage changes, ranges, and visible swing structure.
- Volume and relative volume compared with the same token's recent baseline.
- OI absolute values and percentage changes over aligned intervals.

Use completed candles for confirmed classifications. Mark any live/incomplete observation as provisional.

## 2. Classification rules

A label must be supported by a defined observation window and explicit evidence. If evidence is mixed, use **MIXED/UNCLEAR** rather than forcing a category.

### SIDEWAYS / RANGE
Observable conditions:
- Price remains within a relatively stable range.
- No confirmed sequence of higher highs/higher lows or lower highs/lower lows.
- Volume and OI may rise, fall, or remain stable.

Do not infer accumulation or distribution from sideways price alone.

### COMPRESSION
Observable conditions:
- Candle ranges or overall price range contract relative to a stated prior baseline.
- Price movement becomes narrower over the defined window.
- Volume may contract, but this is not mandatory unless the rule explicitly requires it.
- OI behavior must be reported separately.

Compression describes reduced price movement, not a prediction that expansion must follow.

### UPSIDE EXPANSION
Observable conditions:
- Price moves upward beyond a predefined prior range or makes a clearly measured upward expansion.
- Candle ranges and/or consecutive price changes increase relative to baseline.
- Volume behavior is measured and reported.
- OI behavior is measured and reported independently.

Do not require OI to rise for the label unless defining a narrower subtype.

### DOWNSIDE EXPANSION
Observable conditions:
- Price moves downward beyond a predefined prior range or makes a clearly measured downward expansion.
- Candle ranges and/or consecutive price changes increase relative to baseline.
- Volume and OI are reported independently.

### HIGH ACTIVITY / LOW PRICE PROGRESS
Observable conditions:
- Volume is unusually high relative to the same token's baseline.
- Price makes limited net progress or remains within a relatively narrow range over the same interval.

This describes high activity with limited price movement. It does not prove absorption, hidden orders, or a particular participant's intent.

### OI BUILD-UP DURING RANGE
Observable conditions:
- OI increases by a defined amount or percentage over the selected interval.
- Price remains within the defined range.
- Volume is recorded to describe activity.

This does not reveal whether long or short exposure is dominant.

### OI DECLINE
Observable conditions:
- OI decreases over the defined interval.
- Price direction and volume behavior are recorded separately.

Do not automatically label this liquidation, short covering, or position closure by a specific side.

### EXHAUSTION CANDIDATE
Observable conditions may include:
- Price progress slows after an expansion.
- Candle ranges contract or repeated attempts fail to extend the move.
- Volume changes relative to baseline.
- OI changes are reported independently.

This is a candidate label only. Confirm the subsequent outcome before calling the move exhausted.

### FAILED EXPANSION / RANGE RE-ENTRY
Observable conditions:
- Price moves beyond a predefined range boundary.
- Price subsequently closes back inside the prior range within a predefined period.

Record the boundary, breakout timestamp, re-entry timestamp, volume, and OI. Do not label every wick beyond a range as a confirmed breakout.

### MIXED / UNCLEAR
Use when the observations conflict, data is incomplete, or no category's criteria are met.

## 3. Classification dimensions

Do not collapse all inputs into one directional label. Record separate dimensions:

- Price state: rising, falling, sideways, compression, expansion, or unclear.
- Volume state: contracting, normal, elevated, declining, or unavailable.
- OI state: increasing, decreasing, stable, or unavailable.

This prevents an OI increase from being incorrectly described as bullish or bearish by itself.

## 4. Thresholds and baselines

- Define range boundaries and percentage thresholds before classifying a sample.
- Compare volume with the same token's recent completed candles on the same timeframe.
- Compare OI changes over consistent intervals.
- Record the exact lookback and formulas.
- Do not invent universal thresholds that fit every token and timeframe.
- If thresholds are learned from data, test them through skill-validation.md and skill-backtesting.md before treating them as reliable.

## 5. State transitions

When market conditions change, record:
- Previous classification.
- New classification.
- Timestamp of transition.
- Evidence that triggered the change.
- Whether the transition was confirmed by completed candles.
- What happened afterward.

Example transition:
SIDEWAYS → UPSIDE EXPANSION → FAILED EXPANSION / RANGE RE-ENTRY.

A transition is a chronological description, not proof of a causal mechanism.

## 6. Classification record

For every classified interval, store:

- Sample ID.
- Symbol and contract.
- Timeframe and timezone.
- Start/end timestamp.
- Price state and supporting values.
- Volume state, baseline, and relative value.
- OI state, absolute value, and percentage change.
- Classification label.
- Confidence label: low, medium, or high, with a written reason.
- Data-quality flags.
- Subsequent outcome, if known.
- Related pattern IDs.

Confidence refers to confidence that the descriptive label fits the observed data, not confidence in a future price direction.

## 7. Relationship with learning and validation

- Use classification labels to organize samples for skill-learning.md.
- Test whether transitions or combinations have predictive value through skill-validation.md.
- Test fixed classification-based rules through skill-backtesting.md.
- Do not add a classification as a trading signal merely because it has a descriptive name.
- Only approved, evidence-supported features should be incorporated into skill-analisa.md.

## 8. Interaction rules

- Respond in Bahasa Indonesia by default.
- State the evidence and thresholds behind each label.
- Distinguish confirmed completed-candle states from provisional live states.
- Use MIXED/UNCLEAR when the evidence does not fit.
- Do not infer market participants, manipulation, accumulation, distribution, liquidation, or intent from these three inputs alone.
