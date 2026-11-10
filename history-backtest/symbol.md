---
document_type: per-symbol-backtest-history
symbol: REPLACE_WITH_BINANCE_SYMBOL
market: Binance USDⓈ-M Perpetual
status: NOT_RUN
---

# Backtest History — SYMBOL

> File ini adalah template/format standar. Setelah backtest benar-benar selesai, buat atau perbarui file khusus simbol, misalnya `history-backtest/BRUSDT.md`. Jangan menyimpan angka hasil yang belum dihitung. Pertahankan seluruh riwayat run; jangan menimpa hasil lama.

## 1. Identitas pengujian

| Field | Value |
|---|---|
| Symbol | NOT SET |
| Contract | Binance USDⓈ-M Perpetual |
| Exchange data source | NOT SET |
| Backtest engine/version | NOT SET |
| Strategy | Parabolic SAR Follow Trend |
| PSAR parameters | Step 0.01 / Maximum 0.10 |
| Trend timeframe | 1H |
| Entry timeframe | 5M |
| Exit inspection timeframe | 1M |
| Volatility formula | (highest high - lowest low) / first open × 100 |
| Volatility lookback | 288 completed 5M candles |
| Loss-streak rule | 3 consecutive losses → 24-hour entry cooldown |
| Timezone for calculations | UTC |

## 2. Riwayat run

Tambahkan satu bagian baru untuk setiap eksekusi. Jangan mengganti hasil run sebelumnya.

### Run YYYY-MM-DD — RUN_ID

| Field | Value |
|---|---|
| Status | NOT_RUN |
| Evaluation start (UTC) | NOT SET |
| Evaluation end (UTC) | NOT SET |
| Data retrieved at (UTC) | NOT SET |
| 1H candles | NOT SET |
| 5M candles | NOT SET |
| 1M candles | NOT SET |
| Missing / duplicate candles | NOT SET |
| Warm-up coverage | NOT SET |
| Fee model | NOT SET |
| Slippage model | NOT SET |
| Funding model | NOT SET |
| Notional per trade | NOT SET |
| Raw trade log | NOT SET |
| Skipped-signal log | NOT SET |

#### 2.1 Ringkasan ALL_MARKETS

| Window | TP/SL | Signals | Trades | TP | SL | Ambiguous 1M | Data gaps | Win rate | Gross PnL | Net PnL | Profit factor | Max drawdown |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1 day | 3% / 2% | — | — | — | — | — | — | — | — | — | — | — |
| 1 day | 5% / 3% | — | — | — | — | — | — | — | — | — | — | — |
| 1 day | 7% / 5% | — | — | — | — | — | — | — | — | — | — | — |
| 1 day | 10% / 7% | — | — | — | — | — | — | — | — | — | — | — |
| 7 days | 3% / 2% | — | — | — | — | — | — | — | — | — | — | — |
| 7 days | 5% / 3% | — | — | — | — | — | — | — | — | — | — | — |
| 7 days | 7% / 5% | — | — | — | — | — | — | — | — | — | — | — |
| 7 days | 10% / 7% | — | — | — | — | — | — | — | — | — | — | — |
| 30 days | 3% / 2% | — | — | — | — | — | — | — | — | — | — | — |
| 30 days | 5% / 3% | — | — | — | — | — | — | — | — | — | — | — |
| 30 days | 7% / 5% | — | — | — | — | — | — | — | — | — | — | — |
| 30 days | 10% / 7% | — | — | — | — | — | — | — | — | — | — | — |

#### 2.2 Perbandingan volatilitas

Untuk setiap TP/SL dan window, laporkan semua mode:
- ALL_MARKETS.
- ONLY_THIS_BUCKET: 0–10%, 15–25%, 30–45%, >50%.
- EXCLUDE_THIS_BUCKET: exclude 0–10%, exclude 15–25%, exclude 30–45%, exclude >50%.

| Window | TP/SL | Mode | Bucket | Signals | Trades | TP | SL | Win rate | Gross PnL | Net PnL | Max drawdown |
|---|---|---|---|---:|---:|---:|---:|---:|---:|---:|---:|
| NOT RUN | NOT SET | NOT SET | NOT SET | — | — | — | — | — | — | — | — |

Jangan hanya menyimpan konfigurasi terbaik. Simpan seluruh konfigurasi yang dijalankan, termasuk hasil negatif.

#### 2.3 Breakdown harian

Buat satu baris untuk setiap tanggal UTC dalam jendela 30 hari, termasuk tanggal tanpa trade. Simpan breakdown terpisah untuk setiap kombinasi TP/SL dan mode volatilitas.

| Date UTC | Signals | Trades | TP | SL | Ambiguous 1M | Win rate | Gross PnL | Net PnL | Max loss streak | Cooldown hours |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| YYYY-MM-DD | 0 | 0 | 0 | 0 | 0 | N/A | 0 | 0 | 0 | 0 |

Ulangi tabel untuk periode 1 hari dan 7 hari jika diperlukan. Jangan menghilangkan hari nol trade.

#### 2.4 Breakdown arah

| Window | TP/SL | Direction | Trades | TP | SL | Win rate | Gross PnL | Net PnL |
|---|---|---|---:|---:|---:|---:|---:|---:|
| NOT RUN | NOT SET | LONG | — | — | — | — | — | — |
| NOT RUN | NOT SET | SHORT | — | — | — | — | — | — |

## 3. Audit exit 1M

Laporkan:
- Jumlah trade dengan TP tersentuh lebih dahulu menurut urutan candle 1M.
- Jumlah trade dengan SL tersentuh lebih dahulu menurut urutan candle 1M.
- Jumlah candle 1M yang menyentuh TP dan SL sekaligus.
- Jumlah trade yang tidak dapat dipastikan karena data 1M hilang.
- Jumlah gap harga yang memengaruhi fill.
- Asumsi konservatif yang digunakan.

OHLC 1M tidak menunjukkan urutan tick di dalam menit. Jika TP dan SL berada dalam range candle 1M yang sama, hasil wajib ditandai ambiguous dan dihitung SL-first hanya sebagai asumsi konservatif.

## 4. Trade log dan data mentah

| Artifact | Path / URL | Status |
|---|---|---|
| Full trade log CSV/JSON | NOT SET | NOT SAVED |
| Skipped signals CSV/JSON | NOT SET | NOT SAVED |
| Raw 1M candles | NOT SET | NOT SAVED |
| Raw 5M candles | NOT SET | NOT SAVED |
| Raw 1H candles | NOT SET | NOT SAVED |
| Run configuration | NOT SET | NOT SAVED |

Jangan mengklaim data mentah tersimpan jika file atau URL-nya tidak tersedia.

## 5. Kesimpulan dan keterbatasan

### Hasil observasi
NOT SET — isi hanya setelah simulasi dijalankan.

### Konfigurasi terbaik berdasarkan metrik
NOT SET — jangan memilih hanya berdasarkan PnL. Sertakan jumlah trade, expectancy, profit factor, drawdown, dan biaya.

### Keterbatasan
- Hasil historis bukan jaminan performa masa depan.
- OHLC 1M tidak dapat membuktikan urutan tick di dalam candle.
- Hasil gross belum memperhitungkan biaya jika fee, slippage, dan funding belum dimodelkan.
- Periode 1, 7, dan 30 hari belum cukup untuk menyimpulkan strategi robust.
- Perbedaan implementasi PSAR dapat mengubah sinyal; status verifikasi harus disebutkan.

### Keputusan
NOT SET — pilih PROMISING_FOR_FURTHER_TEST / WEAK / REJECTED / INCONCLUSIVE setelah seluruh hasil diaudit.
