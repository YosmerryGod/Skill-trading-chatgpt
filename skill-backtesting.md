---
name: historical-market-backtesting
description: Backtest explicitly defined crypto market patterns or rules over historical price, volume, and Open Interest data using chronological simulation, realistic signal timing, and transparent performance metrics.
---

# Historical Market Backtesting

## Purpose

Evaluate how a precisely defined market rule would have behaved across historical data, using only information available at each simulated point in time.

Backtesting is distinct from pattern discovery:
- skill-learning.md finds candidate recurring behavior.
- skill-validation.md tests whether a hypothesis generalizes to independent data.
- This skill simulates a fixed rule across a chronological historical series and measures its outcomes.

A good backtest does not prove future profitability.

## 1. Require a fixed rule before testing

Before running a test, document:

- Rule ID and version.
- Exact signal conditions using price, volume, and OI.
- Timeframe and candle-close requirement.
- Baseline and lookback calculations.
- Signal timestamp.
- Evaluation horizon.
- Outcome definition.
- Any entry/exit assumptions, if the user explicitly requests a strategy test.
- Data period, symbols, and exclusions.

Do not tune a rule after viewing results and report the same data as an independent test.

## 2. Data requirements

Use the standardized dataset defined in skill-dataset.md:

- Price OHLC candles.
- Volume with clear units.
- OI observations with timestamps and units.
- Data provenance and quality flags.

Check missing candles, irregular intervals, incomplete candles, OI alignment, and contract listing dates before testing.

If data coverage is insufficient, stop or clearly mark the affected test as incomplete.

## 3. Chronological simulation

For each candle or observation time:

1. Make only completed data available up to that timestamp.
2. Calculate features using prior observations and the current completed interval only.
3. Determine whether the fixed rule triggered.
4. Record the signal timestamp and values available then.
5. Evaluate the predefined future outcome using only subsequent data.
6. Move forward chronologically and repeat.

Never use future high/low/close, future volume, or future OI to determine whether a historical signal existed.

When a signal requires a candle close, the earliest simulation time is after that candle closes. Do not assume execution at a price that was only known after the candle completed.

## 4. Avoid duplicate and overlapping signals

- Define a cooldown or event-grouping rule before testing if repeated adjacent signals describe the same event.
- Do not count every candle in one continuous expansion as a separate independent success.
- Keep both raw signal count and independent event count.
- Document how overlapping evaluation windows are handled.
- Do not remove losing or inconvenient signals after the test.

## 5. Outcome measurement

For research-only pattern tests, measure:

- Whether the predefined price outcome occurred within the evaluation horizon.
- Maximum favorable movement after signal.
- Maximum adverse movement after signal.
- Time to outcome.
- Whether price continued, stalled, or reversed.
- Volume and OI behavior during follow-through.

If testing a trading strategy, additionally define execution assumptions explicitly:
- Entry timing and fill assumptions.
- Fees and slippage assumptions.
- Funding only if the user explicitly expands the approved data scope.
- Stop and target handling where both could be touched in the same candle.
- Position sizing and risk constraints.

Do not claim a trade was filled merely because a candle touched a limit price. If intrabar order is unknown, use conservative assumptions or higher-resolution data.

## 6. Required metrics

For pattern/event backtests, report:
- Total signals.
- Independent events.
- Successful outcomes.
- Failed outcomes.
- False-positive rate.
- Missed qualifying events.
- Success rate with numerator and denominator.
- Average and median forward price change.
- Distribution of favorable and adverse movement.
- Time to outcome.

For strategy backtests, only when explicitly requested, report:
- Net return after modeled fees and slippage.
- Profit factor.
- Maximum drawdown.
- Average win and loss.
- Expectancy per trade.
- Trade count and exposure time.
- Sensitivity to fees and slippage.

Do not report metrics that were not calculated. Explain all formulas and assumptions.

## 7. Baselines and comparisons

Compare the tested rule against a simple, clearly defined baseline, such as:
- Unconditional frequency of the target outcome.
- Same event windows without the pattern.
- A simple price-only rule, if useful and predefined.

Use the same evaluation horizon and sample selection for fair comparison.

A rule is not useful merely because it has a positive success rate. It should provide measurable improvement over a reasonable baseline and remain stable on untouched data.

## 8. Out-of-sample and walk-forward testing

Where sufficient history exists:

- Use earlier data for discovery and rule development.
- Use a later untouched period for out-of-sample testing.
- Optionally use walk-forward testing: define the rule using only past data, freeze it, then evaluate the next chronological period.
- Roll forward and repeat without using future observations to revise earlier decisions.
- Keep a final holdout period untouched until the rule is fully specified.

If data is too limited, report that no meaningful out-of-sample test is available.

## 9. Robustness and sensitivity

Test whether results depend excessively on:
- One token or one unusually large event.
- One narrow date range.
- One timeframe.
- One threshold or lookback length.
- Optimistic fill assumptions.
- Small changes in the evaluation horizon.

Only test a limited, predeclared set of parameter alternatives. Report all tested variants, not just the best result.

## 10. Failure analysis

Review failed and missed events:

- Which condition triggered too early or too late?
- Did volume rise without meaningful price progress?
- Did OI rise without subsequent expansion?
- Did price expand without OI confirmation?
- Did the rule trigger repeatedly during sideways movement?
- Did the pattern fail in particular tokens, timeframes, or periods?

Do not rewrite the rule to fit failures and reuse the same test set as proof. A revised rule needs a new version and a fresh test.

## 11. Standard backtest report

### Rule definition
Rule ID, version, exact conditions, timeframe, and outcome horizon.

### Dataset
Symbols, dates, data coverage, independent event count, and exclusions.

### Simulation method
Signal timing, candle completion, OI alignment, duplicate-signal handling, and assumptions.

### Results
All required counts and calculated metrics, with formulas and baseline comparison.

### Out-of-sample results
Report separately from discovery/in-sample results.

### Failure analysis
Examples of false positives, missed events, and adverse outcomes.

### Robustness
Results across tokens, timeframes, periods, and predefined parameter variations.

### Limitations
Data gaps, sample size, execution assumptions, and unresolved uncertainties.

### Decision
Choose:
- **PROMISING:** worth further independent testing.
- **ROBUST IN TESTED DATA:** stable across the stated out-of-sample tests; not a guarantee.
- **WEAK:** little improvement over baseline or unstable results.
- **REJECTED:** failed the predefined criteria.
- **INCONCLUSIVE:** insufficient or poor-quality data.

## 12. Interaction rules

- Respond in Bahasa Indonesia by default.
- Do not fabricate backtest results or imply a test was run when it was not.
- Separate pattern-event research from strategy profitability testing.
- Do not turn historical analysis into a trade recommendation unless asked.
- Preserve rule versions and all prior results.
- Never claim future performance is guaranteed.
- A backtest result alone does not automatically promote a pattern into skill-analisa.md.
