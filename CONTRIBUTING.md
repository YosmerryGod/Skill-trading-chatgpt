# Contributing

Thank you for helping improve this market-research framework.

## Before proposing a change

1. Read the [README](README.md) and [research workflow](docs/WORKFLOW.md).
2. Identify which skill or research record the change affects.
3. Keep the core data scope limited to price, volume, and Open Interest (OI), unless the project owner explicitly changes it.
4. Define every new metric or rule precisely, including formula, units, timeframe, baseline, and data requirements.

## Evidence standards

- Include reproducible source data references and timestamps.
- Separate raw observations, derived calculations, and interpretations.
- Include failed cases and counterexamples.
- Do not claim validation without independent testing.
- Do not use future information to define historical signals.
- Do not invent sample counts, performance statistics, or confidence levels.
- Explain limitations and known false positives.

## Documentation changes

- Update the relevant skill document.
- Keep links and the repository structure current.
- If a methodology change affects other skills, update the workflow documentation too.
- Preserve previous conclusions and explain material changes.
- Do not promote candidate indicators into the core analysis workflow without evidence and explicit approval.

## Research records

Use the [sample record template](templates/sample-record.md). Never commit API keys, credentials, private account information, or other secrets. Large raw datasets should be stored appropriately rather than bloating the repository.

## Tone and scope

Prefer clear, concise, technical writing. Avoid unsupported claims about whales, market makers, manipulation, accumulation, distribution, or participant intent based only on public aggregate price, volume, and OI data.
