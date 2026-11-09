# Market Samples

Store one folder per independent historical market event.

Recommended folder contents:
- `sample.md`: completed [sample record template](../../templates/sample-record.md).
- `price-volume-oi.csv`: timestamped raw or normalized series with units clearly identified.
- `metadata.json`: machine-readable metadata, source, retrieval parameters, and transformations.

Use stable IDs such as `SAMPLE-YYYYMMDD-SYMBOL-01`. Do not count overlapping windows from the same event as independent samples.

Only add records backed by actual exchange data. Record gaps and failed events as carefully as successful events.
