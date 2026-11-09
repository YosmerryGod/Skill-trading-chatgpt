---
name: market-research-dataset
description: Define, normalize, validate, and preserve consistent historical market datasets using price, volume, and Open Interest (OI) for cross-market research.
---

# Market Research Dataset

## Purpose

Create a consistent, auditable record for every market sample so analyses can be compared across symbols, dates, and timeframes without losing the original evidence.

The core data scope is strictly:
1. Price
2. Volume
3. Open Interest (OI)

This file defines the dataset format and data-quality rules. It does not interpret patterns or generate trade recommendations.

## 1. Dataset identity

Every sample must have a unique sample ID and record:

- Sample ID.
- Symbol and contract type.
- Exchange and data source.
- Date and exact start/end timestamps.
- Timezone used for display and UTC timestamps used for storage.
- Candle timeframe(s).
- Lead-in period and follow-through period.
- Event classification, if already known.
- User target direction: pre-bullish / pre-bearish / exploratory-both.
- Actual observed pre-event trend: bullish / bearish / sideways / mixed / unclear.
- Actual event outcome: upside expansion / downside expansion / failed move / range / unclear.
- Volatility regime before event and during event, with calculation metadata.
- Data retrieval date.
- Dataset version and any processing notes.

Never combine spot and perpetual-futures data without explicitly labelling the difference.

## 2. Required observations

### Price
For each candle, preserve:
- Open timestamp and close timestamp.
- Open, high, low, close.
- Percentage change.
- Candle range, both absolute and percentage.
- Candle completion status.

### Volume
For each candle, preserve:
- Raw volume exactly as returned by the exchange.
- Volume unit (base asset, quote asset, or contracts).
- Quote volume when supplied and clearly identified.
- Relative volume calculation and its baseline definition, if calculated.

Never compare raw volume across different tokens without normalization. Do not mix base-asset volume with quote-asset volume.

### Open Interest
For each OI observation, preserve:
- Timestamp.
- Raw OI value.
- Unit (contracts, base asset, or quote currency).
- Absolute change from the prior observation.
- Percentage change from the prior observation.
- Observation interval and source endpoint.

Do not silently convert units. Keep raw values alongside any derived values.

## 3. Time alignment

- Store timestamps in UTC and display them in the requested local timezone, usually WIB when established by the conversation.
- Align price, volume, and OI by explicit timestamps and documented intervals.
- Do not assume OI timestamps exactly match candle boundaries.
- Document resampling or forward/backward alignment rules.
- Do not fill missing OI observations with zero.
- Do not treat unfinished candles as completed candles.
- Avoid mixing intervals in a single comparison table without labelling them.

## 4. Derived features

Derived values must be reproducible and must retain their formula and lookback period.

### Volatility context (required classification)

For every sample, calculate and record a price-derived volatility measure. Suitable choices include rolling standard deviation of log returns (realized volatility) or ATR/range percentage. The chosen measure must be consistent within a comparison cohort.

Record:
- Measure name and exact formula.
- Candle timeframe and lookback length.
- Pre-event volatility value and event-period volatility value.
- Baseline period/distribution used to classify low / medium / high volatility.
- Classification thresholds or quantile boundaries and the reason for choosing them.
- Any annualization factor, if used.
- Data sufficiency and quality flags.

Prefer relative, symbol-specific historical distributions (for example quantile-based regimes) rather than universal fixed percentage cutoffs. Do not compare raw volatility values across tokens unless the measure and normalization make them comparable. If history is insufficient, label the regime unclassified.

Volatility is a contextual feature derived from price. It does not change the approved core inputs (Price, Volume, OI), does not indicate bullish/bearish direction by itself, and must not be treated as a predictive signal without separate validation.

Examples:
- Price return: (close / prior close - 1) × 100%.
- Candle range percentage: (high - low) / prior close × 100%.
- OI percentage change: (current OI / prior OI - 1) × 100%.
- Relative volume: current completed-candle volume divided by the mean volume of a predefined number of prior completed candles of the same timeframe.

The baseline must exclude the current candle when the goal is to determine whether current activity is unusual. State the number of lookback candles and handle zero or missing baselines explicitly.

Do not add new indicators to the core dataset without approval through the learning and validation workflow.

## 5. Data quality checks

Before analysis, check:
- Missing candles or duplicate timestamps.
- Unexpected gaps or irregular intervals.
- Zero, negative, or malformed values.
- Contract listing date and whether the requested period is valid.
- Unit consistency.
- Timestamp alignment.
- Incomplete final candle.
- Missing OI records or changes in endpoint coverage.

Flag suspicious observations. Do not silently repair or discard them. If a correction is necessary, preserve the raw value and document the transformation.

## 6. Sample phase labels

Phase labels are descriptive annotations, not exchange-provided facts:

- Pre-event.
- Compression/base.
- Initial movement.
- Expansion.
- Peak/exhaustion candidate.
- Follow-through.
- Retracement or failure.

Only assign a label when the relevant evidence is visible. Do not force every sample into every phase.

## 7. Standard sample record

Use this logical structure for each sample:

### Metadata
- sample_id:
- symbol:
- contract:
- exchange:
- source:
- date:
- timezone:
- start_utc:
- end_utc:
- timeframes:
- lead_in:
- follow_through:
- retrieval_time:
- dataset_version:

### Data coverage
- price_coverage:
- volume_coverage:
- oi_coverage:
- missing_intervals:
- quality_flags:

### Event notes
- event_type:
- target_direction:
- observed_pre_event_trend:
- actual_event_outcome:
- pre_event_volatility:
- event_volatility:
- volatility_measure_formula:
- volatility_lookback_and_baseline:
- volatility_regime:
- phase_boundaries:
- analyst_notes:

### Observations
A time-indexed table or structured record containing price OHLC, volume, OI, units, and derived changes.

### Provenance
- raw endpoint/source references:
- retrieval parameters:
- transformations:
- known limitations:

This is a logical schema. Store the actual raw series in a machine-readable format such as CSV or JSON when available; do not replace detailed time series with a short narrative summary.

## 8. Dataset versioning and preservation

- Never overwrite original raw observations when recalculating derived features.
- Version schema changes.
- Record the formula change when a derived field changes.
- Preserve previous sample conclusions so future research can audit them.
- Correct an error by recording the correction and reason.
- Keep sample IDs stable when only annotations change.
- Create a new version when raw data, alignment, or calculation methodology materially changes.

## 9. Interaction rules

- Respond in Bahasa Indonesia by default.
- If required data is missing, state exactly what is missing.
- Do not invent candles, OI values, timestamps, units, or sample metadata.
- Keep price, volume, and OI as the approved core inputs.
- Make every analysis reproducible from its stored sample and provenance.
- A dataset is not a validated pattern. Pass samples to skill-learning.md for cross-market comparison and skill-validation.md for hypothesis testing.
