# FEAT-002 · Tools & Perawatan Tanaman

| Field | Isi |
|---|---|
| Status | DRAFT |
| Versi | v7 |
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
4. Efek bonus pertumbuhan dari penyiraman dapat bertambah melalui penggunaan berulang, tetapi totalnya tidak boleh melewati batas maksimum D-011.
5. Area penyiraman ditentukan berdasarkan posisi titik penggunaan dan radius; tanaman tepat pada batas radius dianggap berada di dalam area.
6. Watering Can bersifat manual dan memberikan efek langsung pada saat digunakan.
7. Penyiraman menaikkan WaterLevel tanaman dalam skala integer 0-5. Nilai penambahan per penggunaan BELUM DIPUTUSKAN dan hasil wajib di-clamp maksimum 5.
8. Sistem wajib membedakan WaterLevel dari WateringEffectValue (bonus pertumbuhan). Keduanya tidak boleh disimpan atau dihitung sebagai satu nilai yang sama.
9. WaterLevel 4 berarti Overwatered; WaterLevel 5 berarti Flooded (D-017).
10. Tanaman pulih hanya ketika WaterLevel turun ke level 3 atau lebih rendah. Turun dari 5 ke 4 tidak memulihkan tanaman.
11. Timer kematian dimulai saat WaterLevel naik dari level 0-3 ke level 4 atau 5. Timer terus berjalan selama WaterLevel >= 4; perpindahan antara level 4 dan 5 tidak memulai ulang timer.
12. Rentang kadar air ideal dapat berbeda menurut jenis tanaman pada level 0-3. Level 4 dan 5 selalu kondisi berbahaya bagi semua tanaman.
13. Bonus pertumbuhan penyiraman tetap mengikuti cap D-011 dan tidak meningkat tanpa batas. Perilaku pertumbuhan dasar saat Overwatered/Flooded masih BELUM DIPUTUSKAN.
14. Kadar air berkurang secara alami dari waktu ke waktu. Laju pengurangan alami masih BELUM DIPUTUSKAN.

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

### 2.10 Soil Aerator
1. Soil Aerator adalah item consumable yang membantu mengurangi kadar air berlebih secara aktif (D-014, D-015).
2. Satu penggunaan berhasil mengonsumsi satu unit Soil Aerator dan mengaktifkan satu zona pengeringan berbentuk lingkaran pada titik tanah yang dipilih pemain.
3. Semua tanaman yang berada di dalam radius zona menerima pengurangan WaterLevel secara bertahap melalui tick berkala server.
4. Setiap tick yang berhasil mengeringkan tanaman mengurangi WaterLevel tepat 1 level. WaterLevel tidak boleh turun di bawah 0 (D-017).
5. Tanaman yang masuk ke area saat zona masih aktif mulai menerima pengurangan pada tick berikutnya. Tanaman yang keluar dari area tidak lagi menerima pengurangan dari zona tersebut.
6. Jika WaterLevel turun dari 5 ke 4, status tanaman berubah dari Flooded menjadi Overwatered; timer kematian tetap berjalan.
7. Jika WaterLevel turun dari 4 ke 3 atau lebih rendah, tanaman pulih dan timer kematian dibatalkan sesuai D-013.
8. Soil Aerator tidak mengubah WateringEffectValue dan tidak memberikan bonus pertumbuhan. Fungsinya hanya mengurangi kadar air.
9. Item dikonsumsi ketika zona berhasil diaktifkan, bukan pada setiap tick pengeringan. Aktivasi gagal karena lokasi/izin tidak valid tidak mengonsumsi item.
10. Durasi zona ditetapkan 180 detik (3 menit) sejak aktivasi berhasil (D-016). Radius, interval tick, aturan zona yang saling tumpang tindih, batas jumlah zona aktif, dan apakah zona diwujudkan sebagai perangkat fisik yang terlihat masih BELUM DIPUTUSKAN.
11. Seluruh perhitungan area, pengurangan kadar air, konsumsi item, dan pemulihan dilakukan server-authoritative. Client hanya menampilkan preview, animasi, dan hasil.

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
| Batas maksimum bonus pertumbuhan penyiraman | BELUM DIPUTUSKAN | nilai efek | Cap bonus pertumbuhan, D-011; terpisah dari kadar air |
| Penambahan WaterLevel Watering Can | BELUM DIPUTUSKAN | level/penggunaan | Menambah WaterLevel tiap tanaman yang terkena; clamp maksimum 5 |
| Penambahan WaterLevel Sprinkler | BELUM DIPUTUSKAN | level/tick | Menambah WaterLevel pada setiap tick penyiraman; clamp maksimum 5 |
| Pengurangan alami WaterLevel | BELUM DIPUTUSKAN | level/menit | Mengurangi WaterLevel dari waktu ke waktu |
| Rentang air ideal tanaman | Per jenis tanaman dalam level 0-3 | level | Level 4/5 selalu overwater/flooded; D-017 |
| Durasi Overwatered/Flooded sebelum mati | BELUM DIPUTUSKAN | menit | Timer berjalan selama WaterLevel >= 4; D-013, D-017 |
| Pemulihan Overwatered/Flooded | WaterLevel <= 3 | kondisi | Menghapus OverwateredSince dan mengembalikan status normal; D-013, D-017 |
| Pengulangan Overwatered | Timer episode baru | aturan | Episode baru dimulai jika kadar air kembali melewati toleransi setelah pulih |
| Pemulihan dari Overwatered | Ya | aturan | Pulih jika WaterLevel kembali ke/bawah toleransi sebelum timer kematian habis, D-013 |
| Sprinkler area | Lingkaran | bentuk | Mengikuti keputusan area |
| Sprinkler radius | BELUM DIPUTUSKAN | studs | Perlu keputusan |
| Sprinkler durasi | BELUM DIPUTUSKAN | menit | Perlu keputusan |
| Interval aplikasi otomatis Sprinkler | BELUM DIPUTUSKAN | detik/menit | Perlu keputusan |
| Bonus ukuran buah Sprinkler | BELUM DIPUTUSKAN | % atau multiplier | Perlu keputusan |
| Seed Extractor hasil | BELUM DIPUTUSKAN | benih/penggunaan | Tanaman dikorbankan |
| Harvest Basket konsumsi | 1 | unit/penggunaan | Untuk satu tanaman |
| Plant Sprayer cairan | 1 | aplikasi/tanaman | Jenis dan efek belum diputuskan |
| Pupuk bonus pertumbuhan | BELUM DIPUTUSKAN | % atau waktu | Perlu keputusan |
| Soil Aerator status | Consumable | tipe alat | D-015 |
| Soil Aerator konsumsi | 1 unit/aktivasi berhasil | unit/penggunaan | Dikonsumsi saat zona pengeringan aktif |
| Soil Aerator area | Lingkaran | bentuk | D-015 |
| Skala WaterLevel | 0-5 integer | level | Level 4 = Overwatered; level 5 = Flooded; D-017 |
| Rentang air ideal tanaman | Per jenis tanaman, dalam level 0-3 | level | Level 4 dan 5 selalu berbahaya untuk semua tanaman |
| Soil Aerator radius | BELUM DIPUTUSKAN | studs | Radius zona pengeringan |
| Soil Aerator interval tick | BELUM DIPUTUSKAN | detik | Interval pengurangan kadar air bertahap |
| Soil Aerator pengurangan air | 1 | level/tick/tanaman | Diterapkan pada tanaman dalam radius; D-017 |
| Soil Aerator durasi zona | 180 | detik | 3 menit sejak aktivasi berhasil; D-016 |
| Soil Aerator radius | 12 (ASUMSI usulan) | studs | Diameter zona 24 studs; perlu playtest |
| Soil Aerator interval tick | 15 (ASUMSI usulan) | detik | 12 tick selama durasi 180 detik |
| Soil Aerator pengurangan air | 1 | level/tick/tanaman | Setiap tick menurunkan WaterLevel satu level sampai minimum 0; D-017 |
| Soil Aerator batas zona aktif | 1 (ASUMSI usulan) | zona/plot | Aktivasi kedua ditolak selama zona pertama aktif; item tidak dikonsumsi |

### Rekomendasi balancing sementara Soil Aerator (ASUMSI, belum disetujui)

| Parameter | Nilai usulan | Alasan |
|---|---:|---|
| Skala WaterLevel | 0-5 integer | Memudahkan tuning lintas tanaman; toleransi tetap per jenis |
| Radius | 12 studs | Diameter 24 studs, cukup untuk kelompok tanaman kecil tanpa mencakup seluruh plot |
| Durasi | 180 detik | D-016, keputusan pemilik |
| Interval tick | 15 detik | 12 tick per aktivasi, beban server relatif ringan |
| Pengurangan per tick | 1 level/tanaman | Level turun satu langkah per tick; berhenti pada 0 |
| Zona aktif | Maksimal 1 per plot | Mencegah spam dan penumpukan pengeringan area |
| Zona tanpa tanaman | Aktivasi ditolak, item tidak dikonsumsi | Mencegah item terbuang karena salah penempatan |
| Overlap antar zona | Tidak berlaku jika hanya 1 zona aktif/plot | Aturan sederhana untuk vertical slice |

**Catatan balancing:** radius 12 studs, interval 15 detik, dan batas satu zona aktif per plot masih ASUMSI. Skala WaterLevel 0-5 dan pengurangan satu level per tick adalah keputusan D-017. Jika interval 15 detik dipakai, zona 180 detik memiliki 12 tick; pengurangan efektif berhenti ketika tanaman mencapai WaterLevel 0.

## 4. Kondisi tepi & kegagalan

- Target tanaman sudah dihapus atau tidak lagi valid: batalkan aksi tanpa mengonsumsi item.
- Inventori tidak memiliki consumable yang dibutuhkan: tampilkan pesan item tidak tersedia; jangan jalankan efek.
- Watering Can digunakan tanpa tanaman di dalam radius: tentukan apakah penggunaan tetap mengonsumsi satu unit; BELUM DIPUTUSKAN.
- Tanaman berada tepat di batas radius: dianggap masuk area.
- Tanaman menerima beberapa sumber penyiraman pada waktu yang sama: hitung bonus pertumbuhan gabungan secara server dan clamp pada batas maksimum; akumulasi WaterLevel tetap dihitung terpisah dan dapat melewati toleransi tanaman.
- WaterLevel mencapai 4: tandai tanaman Overwatered dan mulai hitung durasi kondisi tersebut jika sebelumnya berada pada level 0-3.
- WaterLevel mencapai 5: tampilkan status Flooded; timer episode yang sudah dimulai tetap berjalan.
- WaterLevel turun dari 5 ke 4: tanaman tetap Overwatered dan timer tidak di-reset.
- WaterLevel turun ke 3 atau lebih rendah: tanaman pulih dan timer episode dihapus sesuai D-013.
- WaterLevel turun ke 3 atau lebih rendah sebelum timer kematian habis: hapus OverwateredSince dan kembalikan status ke normal sesuai D-013.
- Tanaman kembali melewati toleransi setelah pulih: mulai episode Overwatered baru; jangan menjumlahkan durasi episode lama.
- WaterLevel tetap 4 atau 5 sampai durasi kematian tercapai: ubah status tanaman menjadi Dead.
- Soil Aerator diaktifkan pada lokasi di luar plot atau tanpa izin: tolak aktivasi tanpa mengonsumsi item.
- Soil Aerator menurunkan WaterLevel satu level per tick; hasil tidak boleh kurang dari 0.
- Soil Aerator menurunkan WaterLevel dari 5 ke 4: status berubah dari Flooded menjadi Overwatered, tetapi timer kematian tetap berjalan.
- Soil Aerator menurunkan WaterLevel dari 4 ke 3 atau lebih rendah: tanaman pulih dan timer kematian dibatalkan sesuai D-013.
- Soil Aerator aktif dan tanaman memasuki radius: tanaman mulai menerima pengeringan pada tick berikutnya.
- Tanaman keluar dari radius sebelum zona berakhir: pengeringan dari zona tersebut berhenti untuk tanaman itu.
- Tanaman pulih selama zona aktif: timer Overwatered dibatalkan sesuai D-013; pengeringan dapat berlanjut hingga zona berakhir atau WaterLevel mencapai 0.
- Dua zona Soil Aerator saling tumpang tindih: perilaku penggabungan laju pengeringan BELUM DIPUTUSKAN; implementasi tidak boleh menggandakan efek secara diam-diam.
- Pemain mengaktifkan Soil Aerator tanpa tanaman di dalam radius: rekomendasi DRAFT adalah menolak aktivasi dan tidak mengonsumsi item.
- Zona Soil Aerator mencapai 180 detik: hentikan tick, hapus status zona aktif, dan jangan mengurangi kadar air setelah waktu kedaluwarsa.
- Pemain mencoba mengaktifkan zona kedua pada plot yang sudah memiliki zona aktif: rekomendasi DRAFT adalah menolak aktivasi tanpa mengonsumsi item.
- Plot unload atau server restart ketika tanaman Overwatered: hitung durasi berdasarkan timestamp server tersimpan; jangan mengandalkan timer client atau menghentikan timer hanya karena pemain offline.
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
| WaterLevel | integer | Kadar air aktual tanaman pada skala 0-5; terpisah dari bonus pertumbuhan |
| PreferredWaterRange | struktur/range | Rentang kadar air ideal per jenis tanaman pada level 0-3 |
| OverwateredSince | timestamp/null | Waktu server saat tanaman mulai melewati toleransi |
| PlantHealthState | enum | Kondisi Normal/Overwatered/Flooded/Dead |
| WateringEffectValue | number | Bonus pertumbuhan aktif; bukan kadar air |
| SoilAeratorZoneId | string | Identitas zona pengeringan aktif |
| SoilAeratorCenter | Vector3/struktur posisi | Titik pusat zona pada plot |
| SoilAeratorStartedAt | timestamp | Waktu server aktivasi zona |
| SoilAeratorExpiresAt | timestamp | Waktu server berakhirnya zona |
| SoilAeratorNextTickAt | timestamp | Jadwal tick pengeringan berikutnya, jika diperlukan untuk persistence |

Catatan: radius, interval tick, dan laju pengurangan sebaiknya berasal dari config item, bukan disimpan berulang pada setiap tanaman. Persist hanya data zona aktif yang diperlukan untuk melanjutkan efek setelah plot unload/server restart.
| WateringEffectExpiresAt | timestamp | Waktu berakhir efek jika efek berbatas durasi |
| SprinklerPlacedAt | timestamp | Waktu perangkat mulai aktif |
| SprinklerExpiresAt | timestamp | Waktu perangkat berakhir |
| FruitSizeModifier | number | Modifier ukuran buah, jika sistem ukuran buah diterapkan |

Catatan: skema final mengikuti sistem tanaman/inventori yang dirancang engineer. Jangan menyimpan nilai yang dapat dihitung ulang jika tidak diperlukan. Status waktu harus menggunakan waktu server, bukan timer client.

## 6. UI yang dibutuhkan

- Hotbar/inventori menampilkan ikon, nama, jumlah consumable, dan penanda alat permanen.
- Saat Watering Can dipilih, tampilkan preview lingkaran jangkauan di tanah sebelum pemain mengonfirmasi penggunaan.
- Preview lingkaran membedakan area valid dan tidak valid serta menampilkan tanaman yang akan terkena efek.
- UI status tanaman menampilkan WaterLevel 0-5 dengan label yang mudah dipahami. Level 4 diberi status Overwatered dan level 5 Flooded; rentang ideal level 0-3 dapat diberi indikator sesuai jenis tanaman.
- Saat tanaman Overwatered atau Flooded, tampilkan peringatan visual dan teks yang jelas; jangan hanya mengandalkan warna.
- Saat Soil Aerator dipilih, tampilkan preview zona lingkaran dan tanaman yang akan terkena pengeringan.
- Saat zona aktif, tampilkan indikator durasi tersisa dan efek visual pengeringan yang mudah dikenali.
- Jika tanaman masih Overwatered setelah satu atau beberapa tick, UI menjelaskan bahwa proses pengeringan masih berlangsung.
- UI menampilkan bahwa tanaman masih dapat diselamatkan selama belum mati; jika timer kematian ditampilkan, gunakan bahasa yang mudah dipahami dan tidak menuntut pemain membaca angka teknis.
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
| Soil Aerator | Item/perangkat consumable, animasi aktivasi, preview lingkaran, dan efek visual pengeringan bertahap |

Seluruh asset berstatus placeholder sampai masuk pipeline asset.

## 8. Analisis dampak

- **Dampak core loop:** Tools memperkaya loop tanam–rawat–panen dan memberi pilihan antara interaksi manual, otomatis, dan kenyamanan. Watering Can mendukung sesi singkat; Sprinkler mendukung pemain yang ingin menata kebun sambil membiarkan tanaman dirawat.
- **Source/sink ekonomi:** Consumable Watering Can, Sprinkler, cairan Plant Sprayer, Seed Extractor, Harvest Basket, dan Pupuk berpotensi menjadi sink Life Coin jika dijual di toko. Harga dan sumber pendapatan belum ditentukan; tidak boleh menganggap semuanya berbayar.
- **Risiko:** bonus pertumbuhan berlebihan, stacking tanpa batas, buah besar menciptakan inflasi hasil jual, penggunaan otomatis menambah beban server, exploit remote, serta kematian tanaman yang terasa tidak adil jika toleransi/indikator tidak jelas.
- **Rekomendasi balancing:** pisahkan kadar air dari bonus pertumbuhan. Watering Can dan Sprinkler dapat meningkatkan keduanya, tetapi hanya bonus pertumbuhan yang dibatasi cap D-011; kadar air mengikuti toleransi masing-masing tanaman D-012. D-013 menetapkan kesempatan pulih sebelum kematian.
- **Risiko tambahan:** timer kematian yang berjalan saat pemain offline dapat terasa kejam. Tuning durasi harus memberi ruang sesi singkat dan tidak mendorong pemain login secara kompulsif. Pertimbangkan notifikasi saat kembali, bukan kewajiban memantau tanaman terus-menerus.
- **Dampak tool baru:** Soil Aerator consumable berbentuk zona lingkaran memberi opsi penyelamatan area, bukan satu tanaman. Durasi 3 menit memberi jendela penyelamatan yang jelas. Rekomendasi radius 12 studs dan interval 15 detik masih ASUMSI dan wajib diuji melalui playtest. Setiap tick menurunkan satu level sesuai D-017.
- **Ekonomi Soil Aerator:** Setiap aktivasi menghabiskan satu item, sehingga berpotensi menjadi sink Life Coin bila kelak dijual. Harga dan sumber perolehan belum diputuskan; jangan menganggap item otomatis dijual di toko.
- **Metrik sukses:** persentase pemain yang memakai alat; jumlah penggunaan rata-rata per sesi; waktu dari menanam ke panen; jumlah tanaman yang terkena efek; frekuensi penggunaan Sprinkler; dan perubahan pendapatan panen dibanding pemain yang tidak memakai booster. Target angka ditetapkan setelah baseline playtest.

## 9. Kriteria selesai (acceptance criteria)

- [ ] Shovel dan Trowel tetap tersedia setelah digunakan.
- [ ] Trowel memindahkan tanaman tanpa mereset progres pertumbuhannya.
- [ ] Watering Can menghasilkan area lingkaran dan memengaruhi semua tanaman di dalam radius.
- [ ] Bonus pertumbuhan dari beberapa sumber penyiraman bertambah tetapi tidak melewati batas maksimum D-011.
- [ ] Kadar air tanaman dihitung terpisah dari bonus pertumbuhan.
- [ ] WaterLevel selalu berupa integer 0-5 dan tidak pernah keluar dari rentang tersebut.
- [ ] WaterLevel 4 menampilkan status Overwatered dan WaterLevel 5 menampilkan status Flooded.
- [ ] Turun dari level 5 ke 4 tidak membatalkan timer kematian.
- [ ] Tanaman pulih dan timer dibatalkan hanya ketika WaterLevel turun ke level 3 atau lebih rendah.
- [ ] Setiap jenis tanaman memiliki toleransi air yang divalidasi server.
- [ ] Tanaman yang melewati toleransi masuk status Overwatered.
- [ ] Tanaman tidak langsung mati saat pertama kali melewati toleransi air.
- [ ] Jika kadar air kembali ke/bawah toleransi sebelum durasi kematian habis, tanaman pulih dan timer episode dihapus.
- [ ] Jika kadar air tetap di atas toleransi sampai durasi kematian habis, tanaman berubah menjadi Dead.
- [ ] Episode Overwatered baru setelah pemulihan memiliki timer baru dan tidak menjumlahkan durasi episode sebelumnya.
- [ ] Timer Overwatered tetap akurat setelah plot unload, server restart, atau pemain disconnect.
- [ ] UI memberi peringatan yang jelas saat tanaman Overwatered.
- [ ] Soil Aerator mengonsumsi satu item saat zona lingkaran berhasil diaktifkan.
- [ ] Zona Soil Aerator mengurangi WaterLevel tanaman di dalam radius secara bertahap pada tick server.
- [ ] Tanaman yang masuk/keluar radius mulai/berhenti menerima pengeringan sesuai aturan area.
- [ ] Soil Aerator menurunkan WaterLevel satu level per tick server pada tanaman dalam radius dan tidak mengubah WateringEffectValue.
- [ ] Soil Aerator tidak dapat membuat WaterLevel kurang dari 0.
- [ ] Tanaman yang mencapai batas aman selama proses pengeringan pulih dan timer kematian dibatalkan sesuai D-013.
- [ ] Tanaman yang masih di atas toleransi tetap Overwatered dan timer kematian tetap berjalan.
- [ ] Zona berhenti tepat setelah 180 detik (3 menit) berdasarkan waktu server dan tidak lagi mengurangi WaterLevel.
- [ ] Jika rekomendasi balancing ASUMSI diterima, zona memiliki radius 12 studs dan tick 15 detik; nilai ini harus dapat diubah melalui config.
- [ ] Aktivasi tidak valid atau tanpa izin tidak mengonsumsi item.
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
| v2 | 2026-11-15 | Memisahkan kadar air dari bonus pertumbuhan; menambahkan toleransi air per tanaman, status Overwatered, dan risiko kematian | Menindaklanjuti D-012 dan mencegah penyiraman berlebihan menjadi strategi tanpa konsekuensi |
| v3 | 2026-11-15 | Menetapkan pemulihan jika kadar air kembali ke batas aman sebelum durasi kematian; timer episode baru setelah pulih | Menindaklanjuti D-013, memberi konsekuensi tanpa kematian instan |
| v4 | 2026-11-15 | Menambahkan kebutuhan tool pengurang kadar air dengan Soil Aerator sebagai nama dan rancangan sementara | Menindaklanjuti D-014 agar pemain memiliki tindakan aktif untuk menyelamatkan tanaman |
| v5 | 2026-11-15 | Mengubah Soil Aerator menjadi consumable area lingkaran dengan pengeringan bertahap | Menindaklanjuti D-015 sesuai pilihan pemilik |
| v6 | 2026-11-15 | Menetapkan durasi Soil Aerator 3 menit dan menambahkan rekomendasi balancing awal berlabel ASUMSI | Menindaklanjuti D-016 dan menyediakan titik awal playtest tanpa mengunci angka usulan |
| v7 | 2026-11-15 | Mengganti skala WaterLevel menjadi integer 0-5; level 4 Overwatered, level 5 Flooded; Soil Aerator mengurangi satu level per tick | Menindaklanjuti D-017 sesuai pilihan pemilik |
