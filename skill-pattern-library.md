---
name: cross-market-pattern-library
description: Maintain a versioned library of recurring crypto market patterns discovered from price, volume, and Open Interest (OI), including supporting samples, counterexamples, definitions, and validation status.
---

# Cross-Market Pattern Library

## Purpose

Maintain a durable, auditable catalogue of candidate and tested market patterns found across independent tokens and historical events.

The library stores what has been observed and how strongly it is supported. It must not turn an interesting chart resemblance into a trading rule.

Core evidence is limited to:
1. Price
2. Volume
3. Open Interest (OI)

## 1. Pattern record requirements

Every pattern must have:

- Unique pattern ID.
- Short descriptive name.
- Version.
- Exact rule/sequence definition.
- Timeframe and observation horizon.
- Required price, volume, and OI conditions.
- Detection timestamp rule.
- Supporting sample IDs.
- Counterexample sample IDs.
- Number of independent events tested.
- Known limitations.
- Current status.
- Date last reviewed.
- Change history.

A pattern definition must be precise enough that another analyst can identify it from the same data.

## 2. Pattern status

Use the following statuses:

- **DISCOVERED:** candidate noticed in one or more samples; not independently tested.
- **PRELIMINARY:** repeated in a small number of samples but evidence remains limited.
- **VALIDATING:** fixed definition is undergoing independent or forward testing.
- **VALIDATED:** has passed the criteria in skill-validation.md on sufficiently varied untouched data. This does not guarantee future results.
- **REJECTED:** failed testing or did not add useful information.
- **INCONCLUSIVE:** evidence or data quality is insufficient.

Do not promote a pattern based only on how visually convincing it looks.

## 3. Pattern description format

Each record should include:

### Pattern identity
- ID:
- Name:
- Version:
- Status:
- First discovered:
- Last reviewed:

### Definition
Describe the exact sequence of price, volume, and OI behavior. Specify timeframe, baseline, thresholds, and how the signal timestamp is determined.

### Expected behavior
State the outcome being investigated and its predefined evaluation horizon. Avoid promises or certainty.

### Supporting evidence
List sample IDs, symbols, dates, and the observed sequence.

### Counterexamples
List cases where the same sequence did not produce the expected outcome, and cases where the expected market move occurred without the pattern.

### Validation summary
Include number of independent signals, successful outcomes, failures, false positives, missed events, baseline comparison, and validation reference.

### Limitations
State market regimes, tokens, timeframes, and data conditions where the pattern may not apply.

### Change history
Record each change to definition, thresholds, evidence, or status. A material rule change requires a new version and fresh validation.

## 4. Pattern families

Patterns may be grouped descriptively by behavior, for example:

- Compression before expansion.
- Price and volume expansion.
- Price expansion with rising OI.
- Price expansion with falling OI.
- OI expansion during sideways price.
- High volume with limited price progress.
- Failed expansion and retracement.
- Downside expansion.

These are catalogue categories, not claims about participant intent. Terms such as accumulation or distribution must be labelled as hypotheses, not facts inferred from price, volume, and OI alone.

## 5. Compare patterns fairly

- Compare like timeframes and clearly defined event windows.
- Normalize volume against each token's own historical baseline.
- Do not count overlapping windows from the same event as independent evidence.
- Keep supporting and contradicting cases visible.
- Record whether the pattern is detectable before, during, or after the move.
- Separate descriptive patterns from predictive candidates.
- Never hide failed samples to improve the apparent success rate.

## 6. Pattern search and reuse

When analyzing a new sample:

1. Check whether it resembles an existing pattern.
2. Compare the exact definition, not just the visual shape.
3. Add the new sample as support, counterexample, or neutral observation.
4. Do not change the pattern definition merely to make the new sample fit.
5. If the new sample suggests a different sequence, create a new candidate or a new pattern version.
6. Send predictive claims through skill-validation.md before promotion.

## 7. Library overview

Maintain a summary table:

| Pattern ID | Name | Status | Independent samples | Supporting cases | Counterexamples | Last reviewed |
|---|---|---|---:|---:|---:|---|

The table must be backed by individual pattern records. Never invent counts or status.

## 8. Promotion and retirement

- A pattern becomes eligible for use in skill-analisa.md only after validation criteria are met and the user approves the update.
- A validated pattern may be downgraded if new counterexamples weaken its evidence.
- Retired patterns remain in the library with their history; do not erase failed hypotheses.
- If the definition changes materially, create a new version and validate it independently.

## 9. Relationship with other skills

- skill-dataset.md defines and preserves consistent market samples.
- skill-analisa.md analyzes one market using approved inputs.
- skill-learning.md discovers candidate patterns across samples.
- skill-validation.md tests candidate hypotheses.
- skill-backtesting.md tests explicit rules over historical sequences.
- This library preserves pattern definitions, evidence, counterexamples, and status.

## 10. Interaction rules

- Respond in Bahasa Indonesia by default.
- Cite sample IDs and dates when discussing a pattern.
- Distinguish observation from prediction.
- Do not call a pattern validated unless its evidence meets skill-validation.md.
- Treat every new market as a possible counterexample.
- Preserve uncertainty and historical change records.
