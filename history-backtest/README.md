# History Backtest

Folder ini menyimpan hasil backtest berdasarkan simbol. Setiap simbol harus memiliki file Markdown sendiri dengan nama uppercase:

- `BTCUSDT.md`
- `ETHUSDT.md`
- `BRUSDT.md`

## Aturan

1. Setelah backtest suatu simbol benar-benar selesai, buat atau perbarui file `<SYMBOL>.md` di folder ini.
2. Gunakan struktur laporan dari file simbol yang sudah ada sebagai format standar.
3. Simpan setiap run baru sebagai bagian riwayat baru; jangan menimpa atau menghapus hasil run sebelumnya.
4. Jangan membuat angka atau menyimpan hasil yang belum dihitung dan diverifikasi.
5. Jika backtest belum dijalankan, tulis status `NOT_RUN` dan jangan isi statistik seolah-olah sudah ada.
6. Simpan trade log dan skipped-signal log sebagai artifact terpisah jika tersedia, lalu cantumkan path atau URL-nya di file simbol.

Contoh: hasil backtest BTCUSDT disimpan di `history-backtest/BTCUSDT.md`, bukan di satu file gabungan semua simbol.
