---
name: market-research-performance-review
description: Periodically review the quality and progress of crypto market research, pattern discovery, validation, backtesting, and indicator selection using documented evidence and failure cases.
---

# Market Research Performance Review

## Purpose

Review whether the market research process is improving as more independent samples are collected.

This review evaluates the quality of evidence, repeatability of patterns, usefulness of indicators, and reliability of the research workflow. It is not a way to celebrate only successful predictions or to guarantee trading performance.

Approved data scope:
1. Price
2. Volume
3. Open Interest (OI)

## 1. Review cadence

Run a review:
- After a meaningful batch of new independent market samples.
- After a pattern completes a validation or backtesting stage.
- When new counterexamples materially change an existing conclusion.
- When the user requests a research progress review.

Do not imply a fixed schedule or sample threshold is statistically sufficient without evidence.

## 2. Review the dataset

Check:
- Number of new samples and independent events.
- Symbols, dates, and timeframes represented.
- Price, volume, and OI coverage.
- Missing or low-quality data.
- Consistency of units, timestamp alignment, and baselines.
- Whether failed and ordinary market conditions are represented.

Highlight concentration risks, such as most samples coming from one token, one date, or one market regime.

## 3. Review pattern performance

For each tracked pattern, report:
- Pattern ID, version, and current status.
- New supporting samples.
- New counterexamples.
- Independent signal count.
- Successful and failed outcomes.
- False positives and missed events.
- Success rate with numerator and denominator.
- Comparison against the defined baseline.
- Out-of-sample or forward-test status.
- Whether evidence strengthened, weakened, or stayed unchanged.

Never combine results from different rule versions without clearly separating them.

## 4. Review indicator usefulness

For every core or candidate indicator, ask:
- Was the data consistently available?
- Was its calculation reproducible?
- Did it provide information beyond existing price, volume, and OI inputs?
- Did it help identify a condition before the move, or only confirm it afterward?
- Did it increase false positives or missed events?
- Did its usefulness repeat across independent tokens and periods?

Use these decisions:
- **KEEP CORE:** continue using as a required input.
- **ADD:** evidence supports adding a tested feature to skill-analisa.md.
- **KEEP TESTING:** insufficient independent evidence.
- **REMOVE/REJECT:** does not add useful information or creates misleading conclusions.

Do not recommend adding an indicator because it is popular or because it fits one successful example.

## 5. Review analysis quality

Audit a selection of prior analyses:

- Did the analysis use the exact requested time window and timezone?
- Were all price, volume, and OI values sourced correctly?
- Were units and intervals clear?
- Were completed candles distinguished from incomplete candles?
- Were interpretations separated from direct observations?
- Were uncertainty and missing data disclosed?
- Were unsupported narratives avoided?
- Were conclusions consistent with the recorded data?

Record errors and corrections. Do not silently rewrite prior conclusions.

## 6. Review prediction timing

For patterns presented as early signals, determine:
- When the signal first became detectable.
- How much of the price move had already occurred by then.
- Whether the signal preceded, coincided with, or followed expansion.
- Whether the remaining move was meaningful over the predefined horizon.

A pattern that appears only after most of the move is confirmation, not an early warning. Label it accordingly.

## 7. Review research biases

Explicitly check for:
- Selection bias: only choosing dramatic pumps or dumps.
- Survivorship bias: excluding tokens or events that failed.
- Look-ahead bias: using future observations to define a past signal.
- Overfitting: repeatedly adjusting thresholds to fit old data.
- Duplicate samples: counting one event many times.
- Confirmation bias: recording supporting evidence but not contradictions.
- Regime concentration: testing only one type of market condition.

State which risks were found and what corrective action is needed.

## 8. Progress dashboard

Maintain a compact summary with actual documented values:

| Measure | Current period | Previous review | Change |
|---|---:|---:|---:|
| Independent samples | Actual count | Actual count | Difference |
| Symbols represented | Actual count | Actual count | Difference |
| Patterns discovered | Actual count | Actual count | Difference |
| Patterns validating | Actual count | Actual count | Difference |
| Patterns validated | Actual count | Actual count | Difference |
| Patterns rejected | Actual count | Actual count | Difference |
| Candidate indicators tested | Actual count | Actual count | Difference |

Do not invent missing counts. If the repository does not contain structured records to calculate a value, mark it as not tracked.

## 9. Review conclusions and actions

Each review must end with:

### Stronger evidence
Patterns or findings supported by additional independent samples.

### Weaker evidence
Patterns undermined by counterexamples or poor out-of-sample results.

### New questions
Specific hypotheses that deserve testing.

### Indicator decisions
KEEP CORE, ADD, KEEP TESTING, or REMOVE/REJECT, with evidence.

### Documentation changes
Proposed updates to skill-analisa.md, skill-learning.md, skill-validation.md, skill-backtesting.md, or the pattern library.

### Next research priorities
The most useful next samples to collect, especially those that can challenge current assumptions.

Do not update skill files silently. Present recommendations and wait for the user's instruction before changing the documented methodology.

## 10. Review history

For every review, record:
- Review ID and date.
- Dataset version.
- Pattern library version.
- Rule versions tested.
- Summary of findings.
- Decisions made.
- User-approved changes.
- Open questions.

Preserve earlier reviews so changes in confidence and methodology can be audited.

## 11. Interaction rules

- Respond in Bahasa Indonesia by default.
- Be direct, evidence-based, and transparent about sample size.
- Show actual counts and denominators for rates.
- Do not claim research quality improved merely because more samples were added.
- Give equal attention to failed patterns and successful patterns.
- Keep research performance separate from live trading PnL unless the user explicitly asks to review strategy performance.
- Never imply automated monitoring or scheduled reviews unless the user has explicitly configured them.
