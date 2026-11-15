# FEAT-002 · Tools & Perawatan Tanaman

| Field | Isi |
|---|---|
| Status | DRAFT |
| Versi | v5 |
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
8. Sistem wajib membedakan `WaterLevel` (akumulasi kadar air tanaman) dari `WateringEffectValue` (bonus pertumbuhan). Keduanya tidak boleh disimpan atau dihitung sebagai satu nilai yang sama.
9. Setiap jenis tanaman memiliki `MaxWaterTolerance`. Nilai ini menentukan kadar air maksimum yang dapat ditoleransi tanpa risiko overwatering.
10. Sumber penyiraman menambah `WaterLevel` sesuai nilai aplikasi masing-masing. Bonus pertumbuhan dari penyiraman dihitung terpisah dan tetap mengikuti cap D-011.
11. Jika `WaterLevel` melebihi `MaxWaterTolerance`, tanaman masuk status `Overwatered`. Status ini dapat berujung pada kematian jika kondisi berlangsung melewati durasi toleransi.
12. Tanaman yang melewati `MaxWaterTolerance` masuk status `Overwatered`; tanaman tidak langsung mati saat status ini dimulai (D-013).
13. Saat memasuki status Overwatered, server mencatat `OverwateredSince` menggunakan waktu server.
14. Selama `WaterLevel` tetap di atas `MaxWaterTolerance`, durasi Overwatered terus berjalan.
15. Jika `WaterLevel` turun ke atau di bawah `MaxWaterTolerance` sebelum durasi kematian tercapai, tanaman pulih: status kembali normal dan `OverwateredSince` dihapus/null.
16. Jika `WaterLevel` tetap di atas `MaxWaterTolerance` sampai durasi kematian tercapai, tanaman berubah menjadi `Dead`.
17. Setelah tanaman pulih, jika kadar air kembali melewati toleransi, episode Overwatered baru dimulai dan timer baru dicatat. Waktu dari episode sebelumnya tidak dijumlahkan.
18. Bonus pertumbuhan penyiraman tetap dibatasi cap D-011 dan tidak meningkat karena tanaman Overwatered.
19. Rekomendasi balancing: selama Overwatered, hentikan bonus pertumbuhan dari penyiraman tambahan. Apakah tanaman tetap tumbuh pada laju dasar selama fase ini masih BELUM DIPUTUSKAN.
20. Kadar air berkurang secara alami dari waktu ke waktu. Laju pengurangan dan apakah tiap jenis tanaman memiliki laju berbeda BELUM DIPUTUSKAN.

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
3. Semua tanaman yang berada di dalam radius zona menerima pengurangan `WaterLevel` secara bertahap selama zona aktif.
4. Pengurangan kadar air dilakukan melalui tick berkala server, bukan pengurangan instan saat item digunakan.
5. Tanaman yang masuk ke area saat zona masih aktif mulai menerima pengurangan pada tick berikutnya. Tanaman yang keluar dari area tidak lagi menerima pengurangan dari zona tersebut.
6. `WaterLevel` setiap tanaman tidak boleh turun di bawah 0.
7. Jika `WaterLevel` turun ke atau di bawah `MaxWaterTolerance` sebelum durasi kematian tercapai, tanaman pulih sesuai D-013 dan `OverwateredSince` dihapus/null.
8. Jika `WaterLevel` masih di atas `MaxWaterTolerance`, tanaman tetap Overwatered dan timer kematian tetap berjalan.
9. Soil Aerator tidak menambah `WateringEffectValue` dan tidak memberikan bonus pertumbuhan. Fungsinya hanya mengurangi kadar air.
10. Item dikonsumsi ketika zona berhasil diaktifkan, bukan pada setiap tick pengeringan. Aktivasi gagal karena lokasi/izin tidak valid tidak mengonsumsi item.
11. Rekomendasi UX: zona memiliki visual penanda lingkaran dan indikator durasi agar pemain memahami area yang sedang dikeringkan.
12. Radius, interval tick, pengurangan WaterLevel per tick, durasi zona, aturan zona yang saling tumpang tindih, batas jumlah zona aktif, serta apakah zona diwujudkan sebagai perangkat fisik yang terlihat BELUM DIPUTUSKAN.
13. Seluruh perhitungan area, pengurangan kadar air, konsumsi item, dan pemulihan dilakukan server-authoritative. Client hanya menampilkan preview, animasi, dan hasil.

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
| Penambahan kadar air Watering Can | BELUM DIPUTUSKAN | water units/aplikasi | Menambah WaterLevel tiap tanaman yang terkena |
| Penambahan kadar air Sprinkler | BELUM DIPUTUSKAN | water units/tick | Menambah WaterLevel pada setiap tick penyiraman |
| Pengurangan alami kadar air | BELUM DIPUTUSKAN | water units/menit | Mengurangi WaterLevel dari waktu ke waktu |
| Toleransi air tanaman | Per jenis tanaman | water units | Field MaxWaterTolerance pada data tanaman, D-012 |
| Durasi Overwatered sebelum mati | BELUM DIPUTUSKAN | menit | Timer berjalan selama WaterLevel > MaxWaterTolerance; D-013 |
| Pemulihan Overwatered | WaterLevel <= MaxWaterTolerance | kondisi | Menghapus OverwateredSince dan mengembalikan status normal; D-013 |
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
| Soil Aerator radius | BELUM DIPUTUSKAN | studs | Radius zona pengeringan |
| Soil Aerator interval tick | BELUM DIPUTUSKAN | detik | Interval pengurangan kadar air bertahap |
| Soil Aerator pengurangan air | BELUM DIPUTUSKAN | water units/tick/tanaman | Diterapkan pada tanaman dalam radius |
| Soil Aerator durasi zona | BELUM DIPUTUSKAN | menit | Zona berhenti setelah durasi habis |
| Soil Aerator batas zona aktif | BELUM DIPUTUSKAN | zona/plot | Perlu aturan limit dan overlap |

## 4. Kondisi tepi & kegagalan

- Target tanaman sudah dihapus atau tidak lagi valid: batalkan aksi tanpa mengonsumsi item.
- Inventori tidak memiliki consumable yang dibutuhkan: tampilkan pesan item tidak tersedia; jangan jalankan efek.
- Watering Can digunakan tanpa tanaman di dalam radius: tentukan apakah penggunaan tetap mengonsumsi satu unit; BELUM DIPUTUSKAN.
- Tanaman berada tepat di batas radius: dianggap masuk area.
- Tanaman menerima beberapa sumber penyiraman pada waktu yang sama: hitung bonus pertumbuhan gabungan secara server dan clamp pada batas maksimum; akumulasi WaterLevel tetap dihitung terpisah dan dapat melewati toleransi tanaman.
- WaterLevel melebihi MaxWaterTolerance: tandai tanaman Overwatered dan mulai hitung durasi kondisi tersebut.
- WaterLevel kembali ke atau di bawah MaxWaterTolerance sebelum timer kematian habis: hapus OverwateredSince dan kembalikan status ke normal sesuai D-013.
- Tanaman kembali melewati toleransi setelah pulih: mulai episode Overwatered baru; jangan menjumlahkan durasi episode lama.
- WaterLevel tetap di atas MaxWaterTolerance sampai durasi kematian tercapai: ubah status tanaman menjadi Dead.
- Soil Aerator diaktifkan pada lokasi di luar plot atau tanpa izin: tolak aktivasi tanpa mengonsumsi item.
- Soil Aerator mengurangi kadar air hingga melewati nol: clamp hasil pada 0.
- Soil Aerator aktif dan tanaman memasuki radius: tanaman mulai menerima pengeringan pada tick berikutnya.
- Tanaman keluar dari radius sebelum zona berakhir: pengeringan dari zona tersebut berhenti untuk tanaman itu.
- Tanaman pulih selama zona aktif: timer Overwatered dibatalkan sesuai D-013; pengeringan dapat berlanjut hingga zona berakhir atau WaterLevel mencapai 0.
- Dua zona Soil Aerator saling tumpang tindih: perilaku penggabungan laju pengeringan BELUM DIPUTUSKAN; implementasi tidak boleh menggandakan efek secara diam-diam.
- Pemain mengaktifkan Soil Aerator tanpa tanaman di dalam radius: kebijakan konsumsi BELUM DIPUTUSKAN.
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
| WaterLevel | number | Kadar air aktual tanaman; terpisah dari bonus pertumbuhan |
| MaxWaterTolerance | number | Batas toleransi air dari data jenis tanaman |
| OverwateredSince | timestamp/null | Waktu server saat tanaman mulai melewati toleransi |
| PlantHealthState | enum | Kondisi Normal/Overwatered/Dead |
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
- UI status tanaman menampilkan indikator kadar air yang mudah dipahami (misalnya Normal, Basah, Overwatered), tanpa mewajibkan pemain membaca angka internal.
- Saat tanaman Overwatered, tampilkan peringatan visual yang jelas dan konsisten; hindari hanya mengandalkan warna agar tetap terbaca oleh pemain dengan gangguan persepsi warna.
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
- **Dampak tool baru:** Soil Aerator consumable berbentuk zona lingkaran memberi opsi penyelamatan area, bukan satu tanaman. Karena pengeringan berlangsung bertahap, pemain perlu memilih lokasi dan waktu aktivasi. Jika laju terlalu tinggi, risiko overwatering menjadi tidak berarti; jika terlalu rendah atau durasi terlalu pendek, item terasa sia-sia. Nilai harus diuji terhadap laju pengeringan alami dan durasi kematian.
- **Ekonomi Soil Aerator:** Setiap aktivasi menghabiskan satu item, sehingga berpotensi menjadi sink Life Coin bila kelak dijual. Harga dan sumber perolehan belum diputuskan; jangan menganggap item otomatis dijual di toko.
- **Metrik sukses:** persentase pemain yang memakai alat; jumlah penggunaan rata-rata per sesi; waktu dari menanam ke panen; jumlah tanaman yang terkena efek; frekuensi penggunaan Sprinkler; dan perubahan pendapatan panen dibanding pemain yang tidak memakai booster. Target angka ditetapkan setelah baseline playtest.

## 9. Kriteria selesai (acceptance criteria)

- [ ] Shovel dan Trowel tetap tersedia setelah digunakan.
- [ ] Trowel memindahkan tanaman tanpa mereset progres pertumbuhannya.
- [ ] Watering Can menghasilkan area lingkaran dan memengaruhi semua tanaman di dalam radius.
- [ ] Bonus pertumbuhan dari beberapa sumber penyiraman bertambah tetapi tidak melewati batas maksimum D-011.
- [ ] Kadar air tanaman dihitung terpisah dari bonus pertumbuhan.
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
- [ ] Soil Aerator tidak mengubah WateringEffectValue dan tidak dapat membuat WaterLevel negatif.
- [ ] Tanaman yang mencapai batas aman selama proses pengeringan pulih dan timer kematian dibatalkan sesuai D-013.
- [ ] Tanaman yang masih di atas toleransi tetap Overwatered dan timer kematian tetap berjalan.
- [ ] Zona berhenti setelah durasi yang ditetapkan dan tidak lagi mengurangi WaterLevel.
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
