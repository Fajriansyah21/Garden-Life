# FEAT-002 · Tools & Perawatan Tanaman

| Field | Isi |
|---|---|
| Status | DRAFT |
| Versi | v1 |
| Prioritas | Should |
| Fase | 1 Konsep & GDD, kandidat Vertical Slice setelah scope disetujui |
| Penulis | ChatGPT |
| Disetujui oleh | (kosong sampai pemilik setuju) |
| Bergantung pada | Sistem tanaman, pertumbuhan, inventori, dan penyimpanan plot |
| Perkiraan biaya | M (ASUMSI; Claude perlu mengonfirmasi) |

> Spec ini merangkum aturan Tools yang telah dikonfirmasi. Nilai numerik yang belum diputuskan sengaja ditandai BELUM DIPUTUSKAN; spec belum siap implementasi.

## 1. Tujuan pemain

Pemain dapat merawat, memindahkan, menghapus, memperbanyak, dan memanen tanaman dengan alat yang memiliki fungsi berbeda. Tools harus membuat farming terasa praktis dan santai, bukan menjadi kewajiban grind atau menggantikan fokus utama dekorasi kebun.

## 2. Aturan

### 2.1 Prinsip umum
1. Semua perubahan inventori, status tanaman, hasil panen, pertumbuhan, dan konsumsi item divalidasi serta diproses server.
2. Client hanya mengirim permintaan penggunaan dan menampilkan jangkauan, animasi, serta hasilnya.
3. Setiap penggunaan consumable yang berhasil mengurangi jumlah item tepat sesuai biaya penggunaan yang ditentukan pada tabel tuning.
4. Penggunaan yang gagal karena target tidak valid, jarak tidak cukup, atau kondisi tanaman tidak sesuai tidak boleh mengurangi item.
5. Tools permanen tidak berkurang jumlahnya ketika digunakan.

### 2.2 Shovel
1. Shovel digunakan pada satu tanaman yang dipilih untuk menghapus tanaman tersebut dari plot.
2. Shovel adalah alat permanen.
3. Konsekuensi penghapusan terhadap hasil panen, benih, dan item yang sudah ditanam harus ditetapkan dalam aturan sistem tanaman; jangan memberi kompensasi otomatis tanpa aturan tersebut.

### 2.3 Trowel
1. Trowel digunakan untuk memindahkan satu tanaman ke posisi lain di plot yang sama.
2. Trowel adalah alat permanen.
3. Pemindahan tidak menghapus atau mereset progres pertumbuhan, status penyiraman, umur, maupun data tanaman.
4. Posisi tujuan wajib lolos validasi area plot dan aturan collision/placement.
5. Trowel tidak memberi hak untuk memindahkan tanaman milik pemain lain; validasi mengikuti kepemilikan objek dan hak plot yang berlaku.

### 2.4 Watering Can
1. Satu penggunaan Watering Can menghasilkan satu area penyiraman berbentuk lingkaran pada titik yang ditentukan pemain.
2. Semua tanaman yang berada di dalam radius area saat penggunaan diproses menerima efek penyiraman.
3. Satu penggunaan mengonsumsi satu unit Watering Can.
4. Efek penyiraman dapat bertambah melalui penggunaan berulang, tetapi total efek tidak boleh melewati batas maksimum.
5. Penggunaan berulang tidak boleh menghasilkan bonus tanpa batas.
6. Area penyiraman ditentukan berdasarkan posisi titik penggunaan dan radius; tanaman tepat pada batas radius dianggap berada di dalam area.
7. Watering Can bersifat manual dan memberikan efek langsung pada saat digunakan.

### 2.5 Sprinkler
1. Sprinkler adalah perangkat consumable yang ditempatkan pada plot.
2. Area jangkauan Sprinkler berbentuk lingkaran.
3. Selama durasi aktif, Sprinkler secara otomatis menerapkan efek penyiraman kepada tanaman di dalam area jangkauannya.
4. Sprinkler juga meningkatkan ukuran buah tanaman yang terkena efek; besaran dan aturan ukuran buah belum ditentukan.
5. Ketika durasi aktif berakhir, perangkat Sprinkler dikonsumsi dan dihapus dari plot.
6. Efek penyiraman dari Sprinkler mengikuti batas maksimum efek penyiraman yang sama dengan Watering Can, kecuali keputusan lanjutan menetapkan aturan khusus.
7. Penumpukan dari beberapa sumber efek tidak boleh melampaui batas maksimum.

### 2.6 Seed Extractor
1. Seed Extractor digunakan pada satu tanaman atau pohon yang valid.
2. Penggunaan mengorbankan dan menghapus tanaman target.
3. Sebagai gantinya, pemain menerima benih yang dihasilkan dari tanaman tersebut.
4. Jumlah benih, peluang hasil tambahan, dan aturan tanaman yang dapat diekstrak BELUM DIPUTUSKAN.

### 2.7 Harvest Basket
1. Satu penggunaan Harvest Basket menargetkan satu tanaman atau pohon.
2. Penggunaan mengambil seluruh buah yang sudah tersedia/siap dipanen pada tanaman target dalam satu aksi.
3. Satu penggunaan mengonsumsi satu unit Harvest Basket.
4. Panen manual satu buah pada satu waktu tetap tersedia tanpa Harvest Basket.
5. Harvest Basket adalah alat kenyamanan, bukan syarat untuk melakukan panen.
6. Jika tidak ada buah siap panen, penggunaan gagal dan item tidak dikonsumsi.

### 2.8 Plant Sprayer
1. Plant Sprayer adalah alat permanen.
2. Cairan atau bahan aplikasi Plant Sprayer merupakan item consumable.
3. Satu aplikasi cairan menargetkan satu tanaman.
4. Efek yang direncanakan meliputi mutasi, peningkatan ukuran, atau variasi khusus tanaman.
5. Jenis cairan, efek spesifik, peluang mutasi, durasi, stacking, dan biaya item BELUM DIPUTUSKAN.
6. Alat permanen tidak dikonsumsi; hanya cairan yang digunakan yang berkurang.

### 2.9 Pupuk
1. Starter Kit memberikan satu item Pupuk.
2. Pupuk direncanakan untuk mempercepat pertumbuhan tanaman.
3. Target penggunaan, konsumsi, besar bonus, durasi, stacking, dan apakah Pupuk memiliki tier BELUM DIPUTUSKAN.
4. Konsep lima tier pupuk dari diskusi lama tidak dianggap sebagai keputusan atau scope aktif.

## 3. Data & angka tuning

| Parameter | Nilai | Satuan | Catatan |
|---|---:|---|---|
| Starter Shovel | 1 | alat | Permanen, D-010 |
| Starter Trowel | 1 | alat | Permanen, D-010 |
| Starter Watering Can | 10 | unit | Consumable, D-010 |
| Starter Pupuk | 1 | item | Efek dan penggunaan belum diputuskan |
| Watering Can area | Lingkaran | bentuk | D-011 |
| Watering Can radius | BELUM DIPUTUSKAN | studs | Perlu keputusan |
| Watering Can konsumsi | 1 | unit/penggunaan | Satu penggunaan menghabiskan satu unit |
| Batas maksimum efek penyiraman | BELUM DIPUTUSKAN | nilai efek | Efek bertambah hingga batas ini, D-011 |
| Sprinkler area | Lingkaran | bentuk | Mengikuti keputusan area |
| Sprinkler radius | BELUM DIPUTUSKAN | studs | Perlu keputusan |
| Sprinkler durasi | BELUM DIPUTUSKAN | menit | Perlu keputusan |
| Interval aplikasi otomatis Sprinkler | BELUM DIPUTUSKAN | detik/menit | Perlu keputusan |
| Bonus ukuran buah Sprinkler | BELUM DIPUTUSKAN | % atau multiplier | Perlu keputusan |
| Seed Extractor hasil | BELUM DIPUTUSKAN | benih/penggunaan | Tanaman dikorbankan |
| Harvest Basket konsumsi | 1 | unit/penggunaan | Untuk satu tanaman |
| Plant Sprayer cairan | 1 | aplikasi/tanaman | Jenis dan efek belum diputuskan |
| Pupuk bonus pertumbuhan | BELUM DIPUTUSKAN | % atau waktu | Perlu keputusan |

## 4. Kondisi tepi & kegagalan

- Target tanaman sudah dihapus atau tidak lagi valid: batalkan aksi tanpa mengonsumsi item.
- Inventori tidak memiliki consumable yang dibutuhkan: tampilkan pesan item tidak tersedia; jangan jalankan efek.
- Watering Can digunakan tanpa tanaman di dalam radius: tentukan apakah penggunaan tetap mengonsumsi satu unit; BELUM DIPUTUSKAN.
- Tanaman berada tepat di batas radius: dianggap masuk area.
- Tanaman menerima beberapa sumber penyiraman pada waktu yang sama: hitung efek gabungan secara server dan clamp pada batas maksimum.
- Sprinkler dihancurkan, disimpan, atau plot mengalami unload sebelum durasi habis: perilaku penghentian dan pengembalian item BELUM DIPUTUSKAN.
- Pemain disconnect saat Sprinkler aktif: efek harus tetap mengikuti waktu server dan status plot tersimpan; detail persistence perlu dikonfirmasi.
- Dua pemain menggunakan alat pada tanaman yang sama: server memproses aksi secara berurutan dan mencegah panen/ekstraksi ganda atas hasil yang sama.
- Pemain mengirim remote palsu atau mengubah target/radius dari client: server mengabaikan parameter yang tidak sah dan menghitung area/hasil secara otoritatif.
- Pemain tidak memiliki izin pada tanaman target: aksi ditolak tanpa mengonsumsi item.

## 5. Data yang disimpan

| Field | Tipe | Keterangan |
|---|---|---|
| ToolId | string | Identitas jenis alat/item |
| Quantity | integer | Jumlah consumable dalam inventori |
| IsPermanent | boolean | Menandai alat permanen |
| OwnerUserId | integer/string | Pemilik objek tanaman atau perangkat sesuai model data |
| PlantId | string | Identitas tanaman |
| GrowthState | struktur | Progres pertumbuhan yang sudah ada pada sistem tanaman |
| WateringEffectValue | number | Nilai efek penyiraman aktif |
| WateringEffectExpiresAt | timestamp | Waktu berakhir efek jika efek berbatas durasi |
| SprinklerPlacedAt | timestamp | Waktu perangkat mulai aktif |
| SprinklerExpiresAt | timestamp | Waktu perangkat berakhir |
| FruitSizeModifier | number | Modifier ukuran buah, jika sistem ukuran buah diterapkan |

Catatan: skema final mengikuti sistem tanaman/inventori yang dirancang engineer. Jangan menyimpan nilai yang dapat dihitung ulang jika tidak diperlukan. Status waktu harus menggunakan waktu server, bukan timer client.

## 6. UI yang dibutuhkan

- Hotbar/inventori menampilkan ikon, nama, jumlah consumable, dan penanda alat permanen.
- Saat Watering Can dipilih, tampilkan preview lingkaran jangkauan di tanah sebelum pemain mengonfirmasi penggunaan.
- Preview lingkaran membedakan area valid dan tidak valid serta menampilkan tanaman yang akan terkena efek.
- Saat Sprinkler ditempatkan, tampilkan preview lingkaran jangkauan dan konfirmasi posisi.
- Sprinkler aktif menampilkan indikator durasi tersisa yang mudah dibaca.
- Seed Extractor menampilkan konfirmasi bahwa tanaman akan dikorbankan untuk menghasilkan benih.
- Harvest Basket menampilkan jumlah buah siap panen sebelum pemain mengonfirmasi.
- Plant Sprayer menampilkan pilihan cairan yang tersedia dan ringkasan efeknya setelah jenis cairan ditetapkan.
- Pesan gagal harus singkat dan menjelaskan penyebab, misalnya target tidak valid atau item habis.
- UI harus mendukung mouse dan layar sentuh.

## 7. Asset yang dibutuhkan

| Asset | Kebutuhan |
|---|---|
| Shovel | Model alat + animasi penggunaan |
| Trowel | Model alat + animasi memindahkan tanaman |
| Watering Can | Model alat, animasi tuang, preview lingkaran |
| Sprinkler | Model perangkat, animasi/efek air, preview lingkaran |
| Seed Extractor | Model alat + efek ekstraksi |
| Harvest Basket | Model alat + animasi panen massal |
| Plant Sprayer | Model alat, cairan, dan efek aplikasi |
| Pupuk | Model item dan efek aplikasi setelah aturan disetujui |

Seluruh asset berstatus placeholder sampai masuk pipeline asset.

## 8. Analisis dampak

- **Dampak core loop:** Tools memperkaya loop tanam–rawat–panen dan memberi pilihan antara interaksi manual, otomatis, dan kenyamanan. Watering Can mendukung sesi singkat; Sprinkler mendukung pemain yang ingin menata kebun sambil membiarkan tanaman dirawat.
- **Source/sink ekonomi:** Consumable Watering Can, Sprinkler, cairan Plant Sprayer, Seed Extractor, Harvest Basket, dan Pupuk berpotensi menjadi sink Life Coin jika dijual di toko. Harga dan sumber pendapatan belum ditentukan; tidak boleh menganggap semuanya berbayar.
- **Risiko:** bonus pertumbuhan berlebihan, stacking tanpa batas, buah besar menciptakan inflasi hasil jual, penggunaan otomatis menambah beban server, serta exploit remote.
- **Metrik sukses:** persentase pemain yang memakai alat; jumlah penggunaan rata-rata per sesi; waktu dari menanam ke panen; jumlah tanaman yang terkena efek; frekuensi penggunaan Sprinkler; dan perubahan pendapatan panen dibanding pemain yang tidak memakai booster. Target angka ditetapkan setelah baseline playtest.

## 9. Kriteria selesai (acceptance criteria)

- [ ] Shovel dan Trowel tetap tersedia setelah digunakan.
- [ ] Trowel memindahkan tanaman tanpa mereset progres pertumbuhannya.
- [ ] Watering Can menghasilkan area lingkaran dan memengaruhi semua tanaman di dalam radius.
- [ ] Efek penyiraman dari beberapa penggunaan bertambah tetapi tidak melewati batas maksimum.
- [ ] Sprinkler bekerja otomatis di area lingkaran selama durasi yang ditetapkan dan hilang setelah durasi berakhir.
- [ ] Efek Sprinkler tidak membuat efek penyiraman melewati batas maksimum.
- [ ] Seed Extractor menghapus tanaman target dan memberi benih sesuai tabel hasil.
- [ ] Harvest Basket memanen seluruh buah siap panen pada satu tanaman dalam satu penggunaan.
- [ ] Panen manual tetap dapat dilakukan tanpa Harvest Basket.
- [ ] Plant Sprayer tidak habis karena digunakan, sedangkan cairan aplikasinya berkurang sesuai aturan.
- [ ] Aksi tidak valid tidak mengurangi consumable.
- [ ] Server memvalidasi semua target, kepemilikan, jumlah item, dan hasil.
- [ ] Tidak ada error di Output saat seluruh skenario uji dijalankan.

## 10. Riwayat revisi

| Versi | Tanggal | Perubahan | Alasan |
|---|---|---|---|
| v1 | 2026-11-15 | Dibuat sebagai spec DRAFT; mencatat Tools yang telah dikonfirmasi dan keputusan area lingkaran serta stacking berbatas maksimum | Melanjutkan desain Tools Garden Life |
