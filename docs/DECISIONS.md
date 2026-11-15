# DECISIONS · Log Keputusan

Aturan: **hanya ditambah, tidak dihapus.** Untuk mengubah keputusan, tulis entri baru yang menyebut "Menggantikan D-0xx".
Entri terbaru di paling atas.

## Format

```
### D-XXX · Judul singkat
- Tanggal:
- Diputuskan oleh: Pemilik / ChatGPT disetujui / Claude disetujui
- Status: Aktif / Digantikan oleh D-YYY
- Konteks: kenapa ini perlu diputuskan
- Keputusan: apa yang dipilih
- Alternatif yang ditolak: dan alasannya
- Dampak: ke desain / kode / asset
```

---

### D-004 · Sistem Hybrid Placement untuk tile dan objek kebun
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Menetapkan fondasi penempatan agar penyusunan area kebun tetap rapi tanpa membatasi kreativitas dekorasi.
- Keputusan:
  - Farm Tile dan Build Tile menggunakan grid placement dengan ukuran grid 5×5.
  - Dekorasi, bangunan, dan tanaman menggunakan free placement; objek tersebut tidak wajib berada pada titik grid dan tidak memerlukan tile sebagai alas/slot.
  - Pemain dapat mengaktifkan atau menonaktifkan Snap to Grid sebagai bantuan opsional untuk objek free placement.
  - Rotasi objek menggunakan interval 90° sebagai aturan awal.
- Alternatif yang ditolak: Mewajibkan semua objek mengikuti grid, karena membatasi kebebasan menata kebun; menempatkan tile secara bebas, karena menghilangkan struktur dasar area.
- Dampak: Build Mode perlu membedakan kategori penempatan tile dan objek free placement. UI harus menyediakan kontrol Snap to Grid dan rotasi. Batas area, tabrakan, batas jumlah objek, pemindahan, serta penyimpanan layout masih memerlukan perincian sebelum implementasi.

### D-002 · Identitas Garden Life: dekorasi kebun sebagai fokus utama
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Menentukan arah utama agar fitur farming, sosial, dan ekonomi tidak membuat game kehilangan identitas.
- Keputusan: Garden Life berfokus pada pengalaman santai membangun dan mendekorasi kebun. Manajemen dan ekonomi hadir dalam porsi ringan sebagai pendukung pengalaman tersebut.
- Alternatif yang ditolak: Farming simulator dengan manajemen/ekonomi mendalam sebagai fokus utama.
- Dampak: Prioritas desain adalah dekorasi dan ekspresi personal, lalu pengalaman sosial/co-op, farming santai, dan terakhir manajemen/ekonomi ringan. Fitur yang menambah grind atau tekanan ekonomi harus dievaluasi terhadap identitas ini.

### D-003 · Fondasi plot, tile, ekspansi, dan Shared Savings
- Tanggal: 2026-09-13 (diskusi desain; dicatat ke repo 2026-11-15)
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Menetapkan fondasi kebun pribadi dan kolaborasi agar sistem dekorasi dan ekonomi bersama punya aturan kepemilikan yang jelas.
- Keputusan:
  - Satu server menyediakan 4 plot persisten.
  - Setiap plot memiliki Original Owner permanen dan Active Owner untuk kendali aktif.
  - Kapasitas awal plot adalah 2 pemain dan dapat ditingkatkan menjadi maksimal 3 pemain.
  - Pemain yang menerima undangan berpindah dari plot miliknya sendiri ke plot pengundang; plot asalnya menjadi tersedia.
  - Jika Active Owner terputus, kendali berpindah ke anggota lain sesuai aturan transfer; ketika Original Owner kembali, kendali kembali kepadanya.
  - Farm Tile dan Build Tile berukuran 5×5, dibeli dan masuk inventori sebelum ditempatkan. Dekorasi tidak memerlukan tile.
  - Ukuran plot: Stage 1 = 80×80, Stage 2 = 160×160, Stage 3 = 240×240, Stage 4 = 320×320.
  - Setiap upgrade menambah +40 area kiri, +40 kanan, +80 belakang, dan +0 depan. Objek yang sudah ditempatkan tetap pada posisi tetap.
  - Saldo awal pribadi adalah 1.000 Life Coin.
  - Shared Savings dimiliki plot dan terpisah dari saldo pribadi.
  - Anggota yang sudah berada di plot saat Shared Savings dibuat mendapat akses otomatis. Anggota yang bergabung kemudian membayar biaya administrasi 5.000 Life Coin dan harus disetujui Original Owner.
  - Spending Limit mingguan berlaku pada seluruh pembelian yang memakai Shared Savings. Original Owner dapat mengubah atau menghapus batas tersebut (Unlimited).
- Alternatif yang ditolak: Menyamakan Active Owner dengan pemilik permanen; menjadikan dekorasi bergantung pada tile; mencampur saldo pribadi dengan saldo plot.
- Dampak: Sistem data harus memisahkan identitas pemilik permanen, kendali aktif, saldo pribadi, saldo bersama, inventori, dan hak akses. Detail transfer Active Owner, transaksi, serta biaya upgrade masih memerlukan spec.

### D-001 · Repo GitHub sebagai sumber kebenaran
- Tanggal: [ISI]
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Dua AI (ChatGPT dan Claude) bekerja di proyek yang sama dan perlu konteks yang identik.
- Keputusan: Semua dokumen, spec, kode, dan daftar asset disimpan di repo ini. Pembagian peran: ChatGPT = Perancang, Claude = Engineer, Pemilik = penyetuju.
- Alternatif yang ditolak: Menyalin konteks manual antar chat (rawan selisih).
- Dampak: Semua alur kerja mengikuti `00_WORKFLOW.md`.
