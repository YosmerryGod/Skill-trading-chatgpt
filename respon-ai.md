# AI Response & Workflow Entry Point

This document is the mandatory entry point for an AI assistant using this repository. Read it before responding to a new research request, then read the specific skill documents required by the selected mode.

## 1. First response: identify the user's intent

When the user's intent is not already explicit in the current request, ask this question before requesting market data or starting analysis:

**Mau melakukan apa?**

1. **Analisa Market**
2. **Belajar & Menambah Sampel**

Do not choose a mode on the user's behalf. If the user has already clearly selected a mode, do not ask the question again.

## 2. Mode A — Analisa Market

When the user selects **Analisa Market**:

1. Ask the user to send the market symbol only, for example: `HANAUSDT`.
2. Resolve the correct Binance market and contract type from available market metadata. If more than one relevant market/contract is possible, ask one clarification before proceeding.
3. Ask for a date/time window only if the analysis cannot be meaningfully performed without one. If the user says "now", "latest", or gives a time window, use that scope explicitly.
4. Read and follow:
   - `skills/skill-analisa.md`
   - `skills/skill-dataset.md` when collecting or interpreting historical data
   - `skills/skill-market-classification.md` when classifying observable market state, if relevant
5. Analyze the requested market. The approved core inputs are Price, Volume, and Open Interest (OI).
6. First establish the market's volatility regime from historical price candles before interpreting its behavior. Report the measured volatility level (low / medium / high / mixed or unclassified), calculation, lookback, timeframe, and comparison baseline. Use a consistent, reproducible price-derived measure such as realized volatility or ATR/range percentage; treat volatility as market context, not a new directional signal.
7. Describe the current price trend separately (bullish, bearish, sideways, mixed/unclear) and distinguish trend from volatility. A highly volatile market is not necessarily bullish or bearish.
8. Clearly separate observed facts, interpretations, and unknowns.
9. Do **not** automatically add the result to the research sample count or commit a research sample to GitHub. This mode is analysis only unless the user separately asks to save it.

Example prompt:
> Kirim symbol market yang ingin dianalisis, contoh: `HANAUSDT`.

## 3. Mode B — Belajar & Menambah Sampel

When the user selects **Belajar & Menambah Sampel**:

1. Collect these required inputs:
   - Symbol, for example: `HANAUSDT`
   - Start candle timestamp/date and time
   - End candle timestamp/date and time
   - Candle timeframe, for example: `5m`, `15m`, or `1h`
   - Target direction/behavior to study: **pre-bullish expansion**, **pre-bearish expansion**, or **both / exploratory**
2. Ask for missing inputs before retrieving data. Accept natural-language dates/times, but confirm the timezone if it is not clear. Never silently assume a timezone.
3. Read and follow:
   - `skills/skill-learning.md`
   - `skills/skill-dataset.md`
   - `skills/skill-pattern-library.md`
   - `skills/skill-validation.md` when validation is relevant
   - `skills/skill-market-classification.md` when classifying the sample
4. Retrieve the requested historical data and inspect the exact candle window. Include a suitable lead-in period before the event and follow-through after it; record source, contract, timeframe, timezone, units, coverage, and limitations.
5. Measure and record volatility level before the target move and during the event. State the formula, lookback, timeframe, baseline, and classification method. Also record the observed trend direction separately from the user's target direction.
6. Compare the new market with existing research samples and candidate patterns.
7. Classify the sample based on evidence:
   - Supports an existing candidate pattern
   - Contradicts or is a counterexample to an existing candidate pattern
   - Shows a different/new candidate pattern
   - Insufficient evidence / unclear classification
8. Save every completed learning sample to the appropriate GitHub research folder, following the repository dataset standard. Do not wait until a pattern reaches 10 samples.
9. Report the GitHub file link and commit result after the write succeeds. Never claim it was saved if GitHub did not confirm success.

Example request format:
```text
Symbol: HANAUSDT
Start candle: 09-11-2026 08:00
End candle: 09-11-2026 16:00
Timeframe: 5m
Target direction: Pre-bullish expansion
Timezone: WITA (UTC+8)
```

## 4. Sample counting rules

**A market sample and a same-pattern sample count are different things.**

- Every independently studied market event may be saved as a research sample.
- A sample counts toward a pattern's target only if it matches that pattern's written definition and required conditions.
- Do not combine different patterns to reach the target of 10.
- Supporting samples, counterexamples, and unclear samples must be labeled separately.
- A market may contain more than one distinct event or phase. Do not assume the entire observation window represents one pattern.
- Compare samples within relevant volatility regimes (low / medium / high) and target directions (pre-bullish / pre-bearish). Do not assume a pattern transfers across regimes or directions.
- Volatility classification must include its calculation, lookback, timeframe, baseline, and threshold method. Prefer relative, symbol-specific baselines or distribution-based thresholds over universal fixed cutoffs.
- Keep the user's target direction separate from the direction that actually occurred. Record failed or opposite-direction outcomes as counterexamples, not as if they matched the target.
- Ten samples are an initial research threshold, not statistical proof or automatic validation.
- After collecting comparable samples, evaluate the pattern using the validation and backtesting skills, including failed/non-rally control cases where appropriate.

For each sample, report both:
- Total research samples studied.
- Number of samples assigned to the specific candidate pattern (for example, `1/10`).

Never report a combined total as progress toward a pattern-specific target.

## 5. Repository and evidence rules

- Read the relevant skill documents before starting work.
- Use Binance market data as the source when the research workflow requires Binance data.
- The core analysis inputs are Price, Volume, and OI. Do not silently add indicators to the core method.
- Volatility is a required context/classification dimension derived from price (for example realized volatility or ATR/range percentage); it is not automatically a new directional indicator or a replacement for the approved core inputs.
- Always state volatility regime and observed trend direction separately. Never equate high volatility with bullishness or bearishness.
- OI increasing does not by itself prove that new longs are opening; every futures contract has both a long and a short side.
- Volume increasing alone is not bullish.
- Do not claim liquidation, absorption, manipulation, whale activity, market-maker accumulation, or participant intent without direct evidence.
- Preserve counterexamples; do not cherry-pick supportive samples.
- Preserve raw observations whenever available. A narrative summary is not a substitute for a complete raw dataset.
- Mark summaries clearly when raw CSV/JSON data has not been committed.
- Keep historical research separate from trade recommendations. Do not create a trade plan unless the user asks for one.

## 6. GitHub write discipline

Before creating or updating a research record:

1. Check the existing repository structure and relevant sample/pattern records.
2. Use the established naming convention and dataset template.
3. Do not overwrite an existing sample or pattern record without inspecting its current content and obtaining the correct current file SHA.
4. Include the data provenance, exact window, timeframe, timezone, units, observations, interpretation, limitations, and classification.
5. Commit only after the record is complete enough to be useful.
6. After a successful commit, provide the exact GitHub link and commit confirmation.

## 7. Required interaction examples

**User:** "Mau belajar market."

**AI:** "Kita masuk mode Belajar & Menambah Sampel. Kirim symbol, waktu candle awal, waktu candle akhir, dan timeframe candle."

**User:** "Analisa market."

**AI:** "Kirim symbol market yang ingin dianalisis, contoh: `HANAUSDT`."

**User:** "HANAUSDT"

If the mode is still unknown, do not infer it from the symbol. Ask the user to choose **Analisa Market** or **Belajar & Menambah Sampel** first.

---

This file controls request routing and interaction. The selected skill documents control the detailed research and analysis methodology.
