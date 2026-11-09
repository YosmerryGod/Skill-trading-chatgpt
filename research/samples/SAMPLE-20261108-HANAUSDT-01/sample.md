# HANAUSDT — Historical Market Sample

## Identity
- Sample ID: SAMPLE-20261108-HANAUSDT-01
- Symbol: HANAUSDT
- Contract: Binance USDⓈ-M perpetual futures
- Exchange: Binance
- Data source: Binance USDⓈ-M Futures market-data endpoints
- Date: 8–10 November 2026
- Display timezone: WITA (UTC+8), as used in the original analysis
- Start: 2026-11-08 18:30 WITA (2026-11-08T10:30:00Z)
- End: 2026-11-10 04:45 WITA (2026-11-09T20:45:00Z)
- Timeframes: 5m
- Dataset coverage: 412 price candles, 412 OI observations, 412 long/short account-ratio observations, 9 funding records
- Dataset version: 1.0-summary

## Data coverage and quality
- Price coverage: 412 five-minute candles
- Volume coverage and unit: HANA base-asset volume per candle
- OI coverage and unit: 412 observations; raw OI in HANA units, with OI value also available
- Long/short coverage: 412 account-ratio observations
- Funding coverage: 9 records
- Missing intervals: No missing records were reported in the retrieved 412-record series; a separate raw-file audit was not preserved
- Timestamp alignment notes: Original analysis displayed timestamps in WITA (UTC+8)
- Quality flags: This is a summary record. The complete raw candle/OI/ratio series was not committed as CSV/JSON in this record.

## Event overview
- Event classification: Strong upward expansion followed by retracement and partial recovery
- Start close: 0.01329
- Period low: 0.01324 at 8 Nov 18:30 WITA
- Period high: 0.01979 at 9 Nov 12:35 WITA
- Latest close: 0.01700 at 10 Nov 04:45 WITA
- Start-to-latest close change: approximately +27.9%

## Timeline

| Timestamp (WITA) | Price | Volume | OI | Observation |
|---|---:|---:|---:|---|
| 8 Nov 18:30 | Close 0.01329; period low 0.01324 | — | — | Start of observation window |
| 8 Nov 20:00–20:35 | Around 0.01365 to 0.01360 | Intermittent, no sustained expansion | About 401.29M to 400.55M | Before first impulse, no robust leading expansion |
| 8 Nov 20:40 | Close 0.01408 | 6.389M HANA | About 400.55M | First upward impulse begins; OI broadly flat |
| 8 Nov 20:45 | — | 8.16M HANA | About 402.83M | OI begins to rise |
| 8 Nov 20:50 | — | 15.12M HANA | About 404.23M | Volume and OI expand with the move |
| 8 Nov 21:00 | — | 54.90M HANA | About 411.36M | Large activity expansion after impulse began |
| 9 Nov 10:30 | Close 0.01462 | — | 429.29M | Before the stronger second move |
| 9 Nov 10:50 | Close 0.01476 | 1.46M HANA | 429.74M | Gradual price and OI increase |
| 9 Nov 11:00 | Close 0.01475 | 2.77M HANA | 430.37M | Volume and OI continue to rise |
| 9 Nov 11:05 | Close 0.01483 | 3.05M HANA | 431.26M | Gradual expansion remains visible |
| 9 Nov 11:10 | Close 0.01504 | 8.88M HANA | 431.94M | Stronger impulse begins |
| 9 Nov 11:15 | Close 0.01548 | 27.17M HANA | 434.63M | Price, volume, and OI expand together |
| 9 Nov 11:20 | Close 0.01557 | 31.64M HANA | 443.29M | Strong activity and OI expansion |
| 9 Nov 12:35 | Period high 0.01979 | — | 526.93M | High of the observed expansion |
| 10 Nov 04:45 | Latest close 0.01700 | — | — | End of retrieved window |

## Observed sequence
1. The first impulse on 8 November around 20:40 WITA began without a strong, sustained pre-impulse rise in volume and OI. Volume and OI expanded during and after the initial price move.
2. A stronger second expansion began on 9 November. From approximately 10:30 to 11:05 WITA, price rose gradually, volume increased, and OI rose consistently.
3. The stronger price impulse began around 11:10 WITA. By 11:20, price had advanced, volume had expanded substantially, and OI had increased from the pre-move area.
4. Price reached 0.01979 at 12:35 WITA, while OI reached approximately 526.93M.
5. At the end of the window, price had retraced from the high but remained above the starting level.

## Interpretation
- The first impulse is a counterexample to the idea that a gradual price-volume-OI build-up always appears before a strong move. In this case, the initial move began while OI was broadly flat and activity expanded with or after price.
- The second impulse is a candidate example of gradual price + volume + OI expansion preceding a stronger move. The visible build-up was approximately 10–40 minutes before the strongest acceleration, but this is not proof of predictive lead time.
- OI measures total outstanding contracts and cannot identify whether new longs or new shorts initiated the positions.
- The long-account share decreased from about 78.27% at the start toward approximately 74.59% near the high, while long accounts remained the majority.
- Funding remained positive during the observed period; the maximum recorded rate was approximately 0.00109751 (0.109751%) as reported in the original analysis.

## Unknowns and limitations
- The available summary does not include the full 412-row raw series.
- No conclusion about liquidation, absorption, market-maker accumulation, whale intent, or manipulation can be established from price, volume, OI, account ratio, and funding alone.
- The early warning window needs to be tested against other independent markets and failed-move controls.
- Account ratios count accounts, not position size.
- This sample is historical research, not a trading signal.

## Related patterns
- Candidate pattern: Gradual Price + Volume + OI Expansion
- Counterexample: First impulse with no robust pre-impulse OI/volume build-up
- Pattern status: Candidate only; not validated

## Validation / backtest references
- Hypothesis ID and version: Pending cross-market comparison
- Validation report: Not yet available
- Backtest report: Not yet available
- Current status: One market sample; compare with at least 9 additional independent markets before drawing a repeated-pattern conclusion

## Provenance
- Price/volume: Binance USDⓈ-M Futures 5m klines
- OI: Binance USDⓈ-M Futures open-interest statistics, 5m
- Long/short: Binance USDⓈ-M Futures long/short account ratio, 5m
- Funding: Binance USDⓈ-M Futures funding-rate history
- Retrieval window: 8 Nov 2026 18:30 WITA to 10 Nov 2026 04:45 WITA
- Transformations: UTC timestamps displayed in WITA (UTC+8); percentage return calculated from start and latest close
- Analyst note: Summary transcribed from the completed historical analysis. Export and commit raw series separately before quantitative backtesting.
