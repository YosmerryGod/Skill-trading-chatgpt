# Research Workflow

This document explains how the skills in this repository work together.

## 1. Capture a market sample

Use [skill-dataset.md](../skills/skill-dataset.md) to define the symbol, contract, time window, timezone, timeframes, raw price candles, volume units, OI observations, data coverage, and provenance.

Preserve raw observations. Do not fill missing data with invented values.

## 2. Analyze the sample

Use [skill-analisa.md](../skills/skill-analisa.md) to describe the exact market window using the currently approved indicators. Separate direct observations, interpretation, and unknowns.

## 3. Classify observable behavior

Use [skill-market-classification.md](../skills/skill-market-classification.md) to label states such as compression, range, expansion, or failed expansion. Labels describe the data; they do not identify participants or intent.

## 4. Learn across markets

Use [skill-learning.md](../skills/skill-learning.md) to compare independent samples, identify repeated sequences, record differences, and propose candidate indicators.

## 5. Preserve candidate patterns

Use [skill-pattern-library.md](../skills/skill-pattern-library.md) to create or update versioned pattern records. Every record must include supporting samples and counterexamples.

## 6. Validate hypotheses

Use [skill-validation.md](../skills/skill-validation.md) to freeze the definition, separate discovery and validation data, prevent look-ahead bias, compare with a baseline, and report failures.

## 7. Backtest explicit rules

Use [skill-backtesting.md](../skills/skill-backtesting.md) after the rule and outcome criteria are fixed. Simulate chronologically and report assumptions, missed events, and out-of-sample results separately.

## 8. Review research quality

Use [skill-performance-review.md](../skills/skill-performance-review.md) to assess data quality, pattern stability, indicator contribution, and research biases.

## 9. Update analysis methodology

A proposed indicator or pattern does not enter the standard analysis method automatically. Present:
- Exact definition and calculation.
- Supporting sample IDs.
- Counterexamples.
- Validation and backtest results.
- Limitations and false-positive behavior.

Only update [skill-analisa.md](../skills/skill-analisa.md) after the user approves the change.

## 10. Trade planning is separate

Use [skill-planing.md](../skills/skill-planing.md) only when a trade plan is requested. Historical research and pattern discovery must not automatically turn into a live entry recommendation.
