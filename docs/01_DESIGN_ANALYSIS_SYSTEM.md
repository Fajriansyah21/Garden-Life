# 01 · Sistem Desain & Analisis

Panduan bagi Perancang (ChatGPT) untuk menganalisis dan menimbang setiap keputusan desain. Dipakai juga oleh Claude untuk memahami *kenapa* sebuah angka dipilih.

## 1. Kerangka analisis satu fitur

Setiap fitur dianalisis dengan 8 pertanyaan ini sebelum berstatus `READY`:

| # | Pertanyaan | Isi |
|---|---|---|
| 1 | **Masalah / tujuan** | Apa yang ingin dirasakan atau dilakukan pemain? |
| 2 | **Pemain target** | Pemula, menengah, atau veteran? Solo atau bersama? |
| 3 | **Mekanik** | Aturan tepat (input -> proses -> hasil) |
| 4 | **Dampak core loop** | Memperkuat, memperpanjang, atau mengganggu loop utama? |
| 5 | **Dampak ekonomi** | Sumber uang baru? Penguras (sink) baru? Selisihnya? |
| 6 | **Risiko** | Exploit, inflasi, grind berlebihan, lag, kompleksitas UI |
| 7 | **Biaya implementasi** | S / M / L (perkiraan Claude, dikonfirmasi saat HANDOFF) |
| 8 | **Metrik sukses** | Angka yang bisa diukur setelah playtest |

Prioritas fitur memakai **MoSCoW** (Must / Should / Could / Won't) dikalikan skor **Dampak ÷ Biaya**.

## 2. Core loop (kerangka awal, ubah di GDD)

```
Beli bibit -> Tanam -> Tunggu (tumbuh) -> Panen -> Jual -> Dapat uang -> Upgrade/beli lebih banyak
       ^                                                                          |
       +--------------------------------------------------------------------------+
```

Tiga lapis loop:
- **Detik-ke-detik (±30 dtk):** tanam, siram, panen. Harus terasa responsif.
- **Menit-ke-menit (±5 mnt):** satu siklus tanaman cepat sampai uang masuk.
- **Hari-ke-hari (sesi berikutnya):** progres permanen: lahan, level, koleksi, dekorasi.

## 3. Analisis ekonomi

### Istilah
- **Source:** tempat uang masuk (jual panen, quest, hadiah harian).
- **Sink:** tempat uang keluar (bibit, upgrade lahan, alat, dekorasi).
- **Inflasi:** uang pemain tumbuh lebih cepat daripada hal bermakna untuk dibeli.

### Rumus dasar tanaman

```
Untung per tanaman   = HargaJual x JumlahPanen - HargaBibit
Untung per menit     = Untung per tanaman / WaktuTumbuhMenit
ROI (%)              = Untung per tanaman / HargaBibit x 100
Waktu balik modal    = HargaBibit / (Untung per menit)   (kasar)
```

### Tabel tanaman (contoh format; angka ASUMSI, diganti di spec)

| ID | Tanaman | Level buka | Harga bibit | Waktu tumbuh (mnt) | Jumlah panen | Harga jual | Untung/mnt | ROI % |
|---|---|---|---|---|---|---|---|---|
| CROP-01 | Wortel | 1 | 10 | 1 | 1 | 18 | 8.0 | 80 |
| CROP-02 | Jagung | 3 | 40 | 4 | 2 | 45 | 12.5 | 125 |
| CROP-03 | Tomat | 6 | 120 | 10 | 3 | 70 | 9.0 | 75 |

> Angka di atas hanya contoh cara menghitung. Perancang wajib menyetel ulang agar kurva progres terasa adil.

### Aturan keseimbangan
1. Tanaman level lebih tinggi harus **lebih menguntungkan per menit aktif**, atau lebih nyaman untuk pemain yang sering offline (waktu tumbuh panjang).
2. Pastikan ada pilihan menarik untuk dua gaya main: *aktif* (sering panen cepat) dan *santai* (tanam lalu pergi).
3. Setiap tier unlock harus bisa dicapai dalam target waktu (lihat bagian 4).
4. Harga penguras (sink) naik lebih curam daripada pendapatan, agar uang tidak menumpuk tanpa tujuan.
5. Simulasikan di spreadsheet atau skrip: 0-10 menit, 1 jam, 5 jam, 20 jam bermain.

## 4. Kurva progres (target awal, ASUMSI)

| Tonggak | Target waktu main |
|---|---|
| Panen pertama | < 60 detik |
| Beli lahan ke-2 | ±5 menit |
| Level 5 | ±20 menit |
| Unlock fitur besar pertama | ±30-45 menit |
| Konten "akhir" tahap 1 | ±10-20 jam |

## 5. Metrik & cara mengukur

Metrik yang dikumpulkan dari playtest (manual) atau analytics Roblox:

| Metrik | Arti | Target awal (ASUMSI, sesuaikan) |
|---|---|---|
| D1 retention | Pemain kembali hari ke-1 | ≥ 20% |
| D7 retention | Kembali hari ke-7 | ≥ 5% |
| Panjang sesi rata-rata | Menit per sesi | ≥ 10 menit |
| Waktu ke panen pertama | Detik | < 60 |
| Titik drop-off | Di langkah mana pemain keluar | tidak ada lonjakan di tutorial |
| Rasio uang menumpuk | Uang tidak terpakai / pendapatan per jam | < 3x |

Hal yang tidak bisa diketahui tanpa data nyata harus ditandai **ASUMSI** dan diverifikasi setelah playtest.

## 6. Pola analisis yang dipakai

- **Player journey map:** langkah demi langkah dari masuk game sampai jam ke-10, tulis emosi tiap titik (senang, bosan, bingung).
- **Sink/Source ledger:** tabel semua sumber dan penguras uang per fase; jumlahnya harus seimbang.
- **Risk register:** daftar risiko + kemungkinan + dampak + tindakan.
- **Playtest log:** tanggal, penguji, temuan, keputusan.

## 7. Format laporan analisis

Laporan analisis disimpan sebagai `docs/design/ANALYSIS-XXX_judul.md`:

```
# ANALYSIS-001 · Judul
Tanggal · Pembuat · Terkait: FEAT-..., D-...
## Pertanyaan
## Data / asumsi
## Analisis
## Kesimpulan & rekomendasi (satu rekomendasi utama)
## Dampak ke spec / angka
```

## 8. Pertimbangan khusus Roblox

- Kebanyakan pemain Roblox usia muda dan bermain di ponsel: UI harus besar, sederhana, ramah sentuhan.
- Sesi bisa pendek dan sering terputus: progres harus tersimpan sering dan aman.
- Interaksi sosial (kunjungi kebun teman, trading, co-op) sering menaikkan retensi, tapi menambah risiko exploit dan moderasi. Putuskan secara sadar di GDD.
- Monetisasi (Game Pass, Developer Product) harus adil: jangan membuat pemain gratis macet total. Catat strategi monetisasi di GDD, bukan di kode.
