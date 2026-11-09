# Research Records

This directory is reserved for auditable research artefacts created from actual historical market data.

## Suggested organization
```text
research/
├── samples/
│   ├── README.md
│   └── <sample-id>/
│       ├── sample.md
│       ├── price-volume-oi.csv
│       └── metadata.json
├── patterns/
│   ├── README.md
│   └── <pattern-id>.md
├── validation/
│   └── <pattern-id>-<version>.md
├── backtests/
│   └── <rule-id>-<version>.md
└── reviews/
    └── <review-id>.md
```

## Recordkeeping rules
- Only add records based on real retrieved data.
- Keep raw observations and derived calculations distinguishable.
- Include timestamps, units, timeframe, exchange, contract, and source provenance.
- Do not commit API keys, credentials, private account data, or sensitive information.
- Include failed samples and counterexamples.
- Do not fabricate sample counts or test results.
- Use stable sample, pattern, rule, and review IDs.
- Keep large raw datasets in an appropriate data store if repository size becomes unsuitable; link to them only when access and provenance are clear.

No historical market dataset is implied by the presence of this directory. Add records as actual research is completed.
