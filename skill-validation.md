---
name: market-pattern-validation
description: Validate recurring crypto market patterns discovered through historical research. Test whether patterns generalize across unseen time periods and independent tokens, measure false positives and failures, and decide whether findings are reliable enough to use in skill-analisa.md.
---

# Market Pattern Validation

## Purpose

Determine whether a market pattern discovered through research is repeatable and useful, or whether it is merely a coincidence in the historical samples used to discover it.

This skill validates hypotheses using measurable market data. It must challenge the hypothesis, actively search for counterexamples, and prevent hindsight bias and overfitting.

The primary data scope is the same as `skill-analisa.md`:

1. Price
2. Volume
3. Open Interest (OI)

Do not introduce additional indicators into validation unless the user explicitly changes the research scope.

## 1. Validation principles

- Define the hypothesis before testing it.
- Separate data used to discover a pattern from data used to validate it.
- Never use future candles or future OI values to make a decision that supposedly occurred earlier.
- Include failed moves and ordinary market conditions, not only successful expansions.
- Compare independent tokens and separate events. Multiple overlapping windows from one event are not independent samples.
- Keep timeframe, event definitions, and calculation methods consistent.
- Report every tested sample, including failures and missing data.
- Do not change the hypothesis after seeing the validation result and still call the same test independent.
- Correlation does not prove causation.
- A pattern that describes a move after it has begun is confirmation, not necessarily an early predictive signal.

## 2. Define the hypothesis before testing

Every candidate pattern must have a written, testable definition.

Record:

- Pattern ID and name.
- The exact sequence of price, volume, and OI behavior.
- Timeframe.
- Observation window used to detect the pattern.
- Baseline period used for comparisons.
- What qualifies as an event or signal.
- What outcome counts as success.
- How long after the signal the outcome is measured.
- What counts as failure, no follow-through, or invalid data.

Avoid vague definitions such as "volume is high" or "OI is increasing". Specify the calculation and comparison baseline.

Example hypothesis:

"After a defined consolidation, price breaks above the observed range while relative volume increases and OI rises during the same completed-candle interval. Test whether price continues upward over a predefined future observation window more often than a chosen baseline."

This is only an example. Do not assume it is true or use it as a validated trading rule.

## 3. Separate discovery data from validation data

Use chronological separation whenever possible:

- **Discovery set:** historical samples used to notice and formulate the pattern.
- **Validation set:** later or otherwise untouched samples used to test the fixed hypothesis.
- **Forward test:** observe new market events after the hypothesis is locked, without changing its rules during the test.

Where there is enough data, reserve a separate final test set that is not used for tuning.

Do not randomly mix candles from the same event across discovery and validation. That can leak information from one event into both sets.

If only a few historical samples exist, say that independent validation is not yet possible. Continue collecting new samples rather than presenting an in-sample result as proof.

## 4. Prevent look-ahead bias

At every simulated signal time:

- Use only candles that have fully closed by that time.
- Use only OI observations that were available by that time.
- Calculate baselines using historical observations available before the signal.
- Do not use the event's eventual high, low, close, or total volume to define the signal retrospectively.
- Record the exact timestamp when the pattern became detectable.
- Evaluate subsequent price behavior only after the signal timestamp.

If the data source timestamps OI observations differently from candle closes, align timestamps carefully and document the method.

Never describe a pattern as an early warning if it can only be identified after most of the price move has already happened.

## 5. Build a fair test sample

The validation dataset should include:

- Events where the candidate pattern appeared and price expanded in the expected direction.
- Events where the pattern appeared but the expected expansion did not happen.
- Events where price expanded without the candidate pattern.
- Events where the pattern appeared but price moved in the opposite direction.
- Non-event or consolidation periods where the pattern did not appear.

Use multiple tokens and dates where possible. Avoid allowing one token or one unusually large move to dominate the result.

Define event selection rules before inspecting outcomes. Do not select only visually impressive charts.

Record the sample count and explain exclusions, missing values, and duplicate or overlapping events.

## 6. Measure validation results

For each fixed hypothesis, report:

- **Signals tested:** number of independent occurrences where the pattern was detected.
- **Successful outcomes:** number that met the predefined success condition.
- **Failed outcomes:** number that did not meet it.
- **Opposite outcomes:** number that moved against the expected direction.
- **No-follow-through outcomes:** number that remained range-bound or failed to reach the predefined outcome.
- **Success rate:** successful outcomes divided by all eligible tested signals.
- **False-positive rate:** proportion of pattern signals that did not meet the predefined success condition.
- **Missed events:** qualifying expansions that happened without the pattern.
- **Outcome magnitude:** actual price change over the predefined evaluation horizon.
- **Time to outcome:** elapsed time between detection and the predefined outcome.

Always show numerator and denominator, for example 7 successful outcomes out of 12 tested signals (58.3%). Never report a percentage without its sample count.

Where useful, compare results with a simple baseline, such as the frequency of the same outcome in comparable periods without the pattern. A pattern is not useful merely because its success rate looks high; it should add information beyond the baseline.

Do not claim statistical significance unless a suitable statistical test was actually performed and its assumptions are explained. Small samples should be labelled inconclusive.

## 7. Test robustness

Check whether the finding survives reasonable changes in the dataset:

- Different independent tokens.
- Different calendar periods.
- Different market conditions.
- More than one timeframe, while keeping each timeframe's test separate.
- Alternative but predeclared observation windows.
- Different baseline periods where justified.

Do not keep changing thresholds until the historical result looks good. If thresholds are tuned, record the tuning process and test the final fixed version on untouched data.

If a pattern works only on one token, one narrow date range, or one carefully chosen timeframe, state that limitation clearly.

## 8. Compare against counterexamples

For every supporting sample, actively search for a counterexample.

Ask:

- Did the same price, volume, and OI sequence occur without the expected expansion?
- Did a strong expansion happen without the sequence?
- Did OI rise only after price had already moved?
- Did volume spike while price made little progress?
- Did the pattern appear during a false breakout?
- Did the result depend on one unusually large sample?

Document counterexamples in the pattern record. Do not discard them because they conflict with the current hypothesis.

## 9. Evaluate indicator contribution

The baseline indicators remain:

- Price action: OHLC, percentage change, range, and swing structure.
- Volume: raw candle volume and relative volume against the same token's historical baseline.
- OI: absolute value and percentage change over consistent intervals.

When testing an additional candidate feature:

- Define its formula and data requirements.
- Compare the validation result with and without that feature.
- Check whether it improves detection or outcome quality on untouched data.
- Check whether it merely duplicates information already represented by price, volume, or OI.
- Record any additional false positives or missed events.
- Do not add it to `skill-analisa.md` if the improvement is unclear or only appears in the discovery set.

An indicator is not valuable simply because it correlates with a historical move. It must add repeatable information for the stated analysis purpose.

## 10. Pattern status

Assign one status to each candidate:

- **DISCOVERED:** observed in research, not yet independently tested.
- **PRELIMINARY:** tested on a small or limited sample; evidence remains weak.
- **VALIDATING:** fixed hypothesis is being tested on independent or forward samples.
- **VALIDATED:** repeated evidence on a sufficiently varied untouched sample, with counterexamples and baseline comparison reviewed. This does not guarantee future performance.
- **REJECTED:** the pattern failed its predefined test, did not outperform the baseline, or was too unstable to be useful.
- **INCONCLUSIVE:** data volume, quality, or consistency is insufficient to decide.

Never use VALIDATED solely because the pattern appeared in two or three examples.

## 11. Promotion rules for skill-analisa.md

A pattern or indicator may be recommended for inclusion in `skill-analisa.md` only when:

- Its definition is precise and reproducible.
- Its data is reliably available.
- Its timing is clear and does not depend on future information.
- It has been tested on samples not used to discover or tune it.
- Failed cases and counterexamples are documented.
- It adds useful information compared with the existing baseline.
- Its limitations and false-positive behavior are explained.

Every recommendation must use one of these decisions:

- **ADD:** evidence supports including it in the standard analysis workflow.
- **KEEP TESTING:** promising but not independently supported enough.
- **REJECT:** does not add reliable information or creates misleading conclusions.
- **KEEP CORE:** existing price, volume, or OI input remains necessary.

Do not silently edit `skill-analisa.md`. Present the evidence, test results, and recommendation first. Update the analysis skill only when the user asks.

## 12. Standard validation report

### Hypothesis
State the exact pattern definition and expected outcome.

### Test design
- Discovery and validation periods.
- Symbols and independent event count.
- Timeframes.
- Signal timestamp rules.
- Success/failure definition.
- Evaluation horizon and baseline.

### Results
Show signal count, successful outcomes, failures, opposite outcomes, false positives, missed events, success rate, and baseline comparison.

### Supporting samples
List symbols, dates, and concise evidence.

### Counterexamples
List samples where the pattern failed or did not appear before an expansion.

### Robustness
Explain whether results repeated across tokens, periods, and timeframes.

### Limitations
State sample-size, data-quality, and methodology limitations.

### Decision
Choose DISCOVERED, PRELIMINARY, VALIDATING, VALIDATED, REJECTED, or INCONCLUSIVE.

### Recommendation
Choose ADD, KEEP TESTING, REJECT, or KEEP CORE for `skill-analisa.md`, with reasons.

## 13. Relationship with other skills

- `skill-analisa.md` reads a specified market using the currently approved indicators and definitions.
- `skill-learning.md` compares analyzed markets and discovers candidate recurring patterns and indicators.
- `skill-validation.md` tests those candidates against independent data, baselines, and counterexamples.
- `skill-planing.md` creates a trade plan only when the user explicitly asks for one.

A discovery made by the learning process is not automatically a validated pattern. A validated pattern is not automatically a profitable trading strategy. Keep research, validation, and trade planning separate.

## 14. Interaction rules

- Respond in Bahasa Indonesia by default.
- Be direct and show the actual counts and values behind each conclusion.
- Never invent test results, sample counts, thresholds, or statistical confidence.
- If data is insufficient, say so and specify what additional samples are needed.
- Preserve previous hypotheses and results. When a hypothesis changes, assign a new version and explain what changed.
- When the user asks whether a pattern is valid, use this validation workflow rather than relying on visual impressions.
- Treat every new market as a possible counterexample, not merely another confirmation.
