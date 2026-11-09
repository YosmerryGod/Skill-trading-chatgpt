# BRUSDT — Historical Market Sample

## Identity
- Sample ID: SAMPLE-20261109-BRUSDT-01
- Symbol: BRUSDT
- Contract: USDⓈ-M perpetual futures
- Exchange: Binance
- Data source: Binance USDⓈ-M Futures market-data endpoints
- Date: 9–10 November 2026
- Display timezone: WIB (UTC+7)
- Start (UTC): 2026-11-08T18:00:00Z
- End (UTC): 2026-11-09T20:45:00Z (latest completed 15m candle in retrieved dataset)
- Timeframes: 15m
- Lead-in period: Not separately retrieved
- Follow-through period: Not separately retrieved
- Dataset version: 1.0-summary
- Retrieval time: 10 November 2026, approximately 03:49 WIB

## Data coverage and quality
- Price coverage: 15m candles, 9 Nov 01:00 WIB through 10 Nov 03:45 WIB; 108 records returned
- Volume coverage and unit: Base-asset volume in BRU; quote volume in USDT also returned in candle records
- OI coverage and unit: 15m observations, 108 records; raw OI in BRU contracts/base units as returned by endpoint; OI value also returned in quote currency
- Taker buy/sell: 15m data available; last returned record at 10 Nov 03:30 WIB
- Long/short account ratio: 15m data available
- Funding: seven records in the retrieved period, each +0.00005 (0.005%)
- Missing intervals: Not independently audited
- Duplicate timestamps: Not independently audited
- Incomplete candles: Final candle is the latest completed candle returned; do not treat live price as a completed candle
- Timestamp alignment notes: Binance endpoint timestamps are UTC; values below are displayed in WIB
- Quality flags: This is a summary record, not a complete raw-data archive. The complete 108-row candle/OI/taker series was not committed in this record. Preserve this limitation; do not treat summary statistics as a substitute for raw CSV.

## Event overview
- Event classification: Strong recovery / upward expansion after an earlier sharp downside wick
- Start price (close): 0.4241 at 9 Nov 01:00 WIB
- End price (close): 0.4751 at 10 Nov 03:45 WIB
- Close-to-close change: approximately +12.02%
- Period high: 0.4759 at 10 Nov 03:45 WIB
- Period low: 0.4010 at 9 Nov 04:45 WIB
- OI start: 12,401,048
- OI minimum: 12,189,928 at 9 Nov 11:00 WIB
- OI maximum: 12,465,940 at 9 Nov 01:45 WIB
- OI end: 12,283,186 at 10 Nov 03:45 WIB
- OI start-to-end change: approximately -0.95% in raw OI units

## Timeline
| Timestamp (WIB) | Price / event | Volume / taker activity | OI | Notes |
|---|---|---|---:|---|
| 9 Nov 01:00 | Close 0.4241 | 15m volume 144,477 BRU | 12,401,048 | Starting observation |
| 9 Nov 01:45 | Price still around 0.4278 close | High early-period activity; candle later had a sharp downside wick | 12,465,940 | Maximum OI in the sample |
| 9 Nov 04:45 | Low 0.4010; candle close 0.4236 | 15m volume 1,038,072 BRU | OI already declining | Largest volume candle; sharp intraperiod wick |
| 9 Nov 11:00 | Price around 0.4299 close | Taker buy/sell ratio in adjacent 15m records reached 2.72 at 11:30 WIB | 12,189,928 | Minimum OI in the sample |
| 9 Nov 13:45 | Price close 0.4309 | Taker buy/sell ratio 3.1784 | OI recovering | Strong taker-buy imbalance in this interval |
| 9 Nov 14:00 | Price close 0.4299 | Taker buy 165,049 BRU; sell 65,999 BRU; ratio 2.5008 | OI recovering | High buy-side taker activity |
| 9 Nov 18:30 | Price close 0.4585 | Volume 225,728 BRU | OI around 12.38M | Price expansion |
| 9 Nov 19:00 | Price close 0.4576 | Mixed taker activity | OI 12,407,999 | OI near local recovery high |
| 10 Nov 03:30 | Price close 0.4732 | Taker buy 118,750 BRU; sell 81,004 BRU; ratio 1.466 | OI 12,273,060 at 03:00 WIB sample | Late price strength while OI was easing |
| 10 Nov 03:45 | Close 0.4751; high 0.4759 | 15m volume 52,440 BRU | 12,283,186 | Last completed candle in retrieved dataset |

## Observed sequence
1. Price began near 0.4241 while OI was about 12.40M.
2. During the early period, OI reached a local maximum around 12.466M.
3. A large-volume 15m candle printed a deep wick to 0.4010 at 9 Nov 04:45 WIB.
4. OI continued declining and reached its sample minimum around 9 Nov 11:00 WIB while price was recovering from the wick.
5. From around 9 Nov midday onward, OI recovered alongside price, with strong taker-buy imbalances at selected intervals.
6. In the late portion, price continued higher toward 0.4759 while OI no longer expanded consistently and was lower at the end than at the start.

## Interpretation
- The first recovery phase occurred while OI was still falling. This is consistent with a market recovery during net reduction in open contracts, but OI alone cannot identify whether long or short positions were closed.
- The later phase showed price rising while OI recovered, consistent with new positions being added during part of the advance. OI does not identify which side initiated those positions.
- The final price advance did not have continuous OI expansion. This is a useful counterexample to any overly simple rule that rising price must always be accompanied by rising OI.
- Selected intervals showed strong taker-buy imbalance, but this was intermittent rather than continuous.

## Unknowns and limitations
- OI is the total outstanding contracts; every contract has both a long and a short side. OI alone does not reveal directional positioning or trader identity.
- Long/short account ratio is account count proportion, not position size.
- Positive funding does not establish that all market participants were net long.
- No conclusion about liquidation, absorption, market-maker accumulation, whale intent, or manipulation can be established from these fields alone.
- Relative-volume baselines and a complete 5m lead-in study have not yet been calculated.
- This record contains summarized observations, not the complete raw 108-row dataset.

## Related patterns
- Supporting pattern IDs: None assigned yet
- Counterexample pattern IDs: None assigned yet
- New candidate pattern: Recovery after OI contraction, followed by partial OI re-expansion; late price strength without continuous OI growth
- Research status: Observation only; not a validated pattern and not a trading signal

## Validation / backtest references
- Hypothesis ID and version: Pending cross-market comparison
- Validation report: Not yet available
- Backtest report: Not yet available
- Current status: Awaiting comparison with at least 9 additional independent market samples

## Provenance
- Price/volume: Binance USDⓈ-M Futures klines, BRUSDT, interval 15m
- OI: Binance USDⓈ-M Futures open-interest statistics, BRUSDT, period 15m
- Taker activity: Binance USDⓈ-M Futures taker buy/sell volume, BRUSDT, period 15m
- Long/short: Binance USDⓈ-M Futures global long/short account ratio, BRUSDT, period 15m
- Funding: Binance USDⓈ-M Futures funding-rate history, BRUSDT
- Retrieval parameters: startTime 2026-11-08T18:00:00Z; endTime approximately 2026-11-09T20:49:45Z
- Transformations: UTC timestamps displayed as WIB (UTC+7); close-to-close return calculated from 0.4241 and 0.4751
- Analyst note: Revisit this record if the complete raw time series is later exported and committed as CSV/JSON.
