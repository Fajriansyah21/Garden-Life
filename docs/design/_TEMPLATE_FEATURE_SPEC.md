# FEAT-XXX · Nama Fitur

| Field | Isi |
|---|---|
| Status | DRAFT |
| Versi | v1 |
| Prioritas | Must / Should / Could |
| Fase | 2 Vertical Slice / 3 Produksi / ... |
| Penulis | ChatGPT |
| Disetujui oleh | (kosong sampai pemilik setuju) |
| Bergantung pada | FEAT-... |
| Perkiraan biaya | S / M / L (dikonfirmasi Claude) |

## 1. Tujuan pemain
Apa yang dirasakan atau dilakukan pemain, dalam 1-2 kalimat.

## 2. Aturan (harus tepat dan bisa diuji)
Tulis sebagai daftar bernomor. Pakai angka dan satuan konkret.
1. Saat [pemain melakukan X], maka [sistem melakukan Y].
2. ...

## 3. Data & angka tuning
Semua angka di tabel. Claude akan memindahkannya ke `src/shared/`.

| Parameter | Nilai | Satuan | Catatan |
|---|---|---|---|
| | | | |

## 4. Kondisi tepi & kegagalan
- Uang tidak cukup:
- Inventori penuh:
- Pemain keluar saat proses berjalan:
- Dua pemain berinteraksi dengan objek yang sama:
- Pemain mencoba curang (kirim remote palsu):

## 5. Data yang disimpan
Field apa yang harus masuk ke profil pemain (nama, tipe, nilai awal).

## 6. UI yang dibutuhkan
Elemen layar, teks, tombol, umpan balik (suara/efek). Sketsa teks boleh.

## 7. Asset yang dibutuhkan
Nama sesuai `04_ASSET_PIPELINE.md`, status placeholder dulu.

## 8. Analisis dampak
- Dampak core loop:
- Source/sink ekonomi (+/- per jam bermain):
- Risiko:
- Metrik sukses:

## 9. Kriteria selesai (acceptance criteria)
Kalimat yang bisa dicentang saat tes:
- [ ] Pemain dapat ...
- [ ] Ketika ..., maka ...
- [ ] Tidak ada error di Output saat ...

## 10. Riwayat revisi

| Versi | Tanggal | Perubahan | Alasan |
|---|---|---|---|
| v1 | | Dibuat | |
