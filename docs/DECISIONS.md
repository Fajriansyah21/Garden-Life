### D-022 · Sistem Variant, Mutation, dan perhitungan harga buah
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Buah membutuhkan dua lapisan atribut khusus yang sama-sama mengubah tampilan dan nilai jual, tetapi memiliki aturan perolehan, penumpukan, serta prioritas visual yang berbeda.
- Keputusan:
  - Variant dan Mutation adalah dua sistem terpisah. Keduanya dapat dimiliki oleh buah yang sama dan sama-sama meningkatkan harga jual.
  - Satu buah hanya dapat memiliki satu Variant. Variant yang sudah diperoleh bersifat permanen pada buah tersebut: tidak dapat diganti, ditimpa, atau ditumpuk dengan Variant lain.
  - Variant mengubah tampilan buah dan memiliki prioritas visual tertinggi. Tampilan Variant tidak dapat ditimpa oleh tampilan Mutation.
  - Variant yang telah diperoleh tetap menjadi atribut buah dan tidak hilang ketika buah memperoleh Mutation.
  - Variant Seasonal meningkatkan Rarity buah. Variant Seasonal sangat langka dan memerlukan kondisi khusus. Nama Variant Winter diubah menjadi **Cristal**.
  - Multiplier Variant:
    | Variant | Multiplier harga |
    |---|---:|
    | Seasonal: Cristal (Winter) | 5x |
    | Silver | 1,5x |
    | Gold | 3x |
    | Rainbow | 4x |
  - Mutation juga mengubah tampilan buah dan meningkatkan harga jual. Sebuah buah dapat memiliki beberapa jenis Mutation sekaligus.
  - Mutation yang baru diperoleh dapat menggantikan tampilan Mutation sebelumnya, tetapi tidak menghapus Mutation sebelumnya sebagai atribut atau menghilangkan multiplier ekonominya.
  - Satu jenis Mutation hanya dapat tercatat satu kali pada buah yang sama. Mendapatkan jenis Mutation yang sudah dimiliki tidak menambahkan stack duplikat.
  - Mutation dapat diperoleh melalui cuaca, musim, metode khusus, atau Plant Sprayer. Peluang, kondisi, dan multiplier masing-masing Mutation ditentukan secara individual; nilai multiplier Mutation belum ditetapkan secara global.
  - Perhitungan harga jual menggunakan urutan: **Harga Dasar × Multiplier Variant × Jumlah Multiplier Mutation**.
  - Multiplier Mutation dijumlahkan terlebih dahulu. Contoh: harga dasar 100 C, Variant Seasonal 5x, dan dua Mutation dengan multiplier 2x serta 5x menghasilkan 100 C × 5 × (2 + 5) = **3.500 C**.
  - Jika buah tidak memiliki Variant, faktor Variant menggunakan nilai netral 1x. Jika buah tidak memiliki Mutation, faktor Mutation menggunakan nilai netral 1x.
  - Angka 2x dan 5x pada contoh perhitungan hanya ilustrasi, bukan nilai multiplier Mutation yang telah disetujui.
- Alternatif yang ditolak: Menjadikan Variant dan Mutation satu sistem; mengizinkan Variant ditimpa; menghapus efek ekonomi Mutation yang tampilannya ditimpa; serta mengalikan semua multiplier Mutation satu per satu tanpa penjumlahan terlebih dahulu.
- Dampak:
  - Data buah perlu menyimpan VariantId tunggal dan kumpulan MutationId unik secara persisten.
  - Tampilan buah harus menerapkan prioritas Variant di atas Mutation, sementara semua atribut Mutation tetap dihitung untuk ekonomi.
  - Sistem harga harus menghitung multiplier Variant dan Mutation secara terpisah sesuai urutan rumus.
  - D-021 tetap berlaku khusus untuk batas satu keberhasilan mutasi banjir per buah; D-022 tidak menghapus batas tersebut.
  - Detail tiap Mutation, peluang perolehan, efek tambahan, dan multiplier individual masih harus ditetapkan sebelum spec implementasi dinyatakan lengkap.

### D-023 · Identitas visi jangka panjang Garden Life
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Roadmap perlu memiliki arah produk jangka panjang yang konsisten agar pengembangan sistem dan konten tidak kehilangan identitas utama Garden Life.
- Keputusan:
  - Identitas pengalaman jangka panjang Garden Life adalah **Cozy Garden Life Simulator**.
  - Garden Life berpusat pada kebun pribadi pemain sebagai ruang personal yang terus berkembang.
  - Pengalaman utama yang ingin didukung adalah mendekorasi dan mengekspresikan gaya kebun, mengoleksi tanaman unik, merawat kebun, serta mengunjungi kebun teman.
  - Farming merupakan aktivitas pendukung perkembangan kebun, bukan satu-satunya tujuan permainan.
  - Visi ini berlaku sebagai arah jangka panjang dan tidak otomatis menjadikan seluruh sistem atau ide sebagai scope First Release.
  - Pembagian pekerjaan ke First Release, Post-Release, dan Long-Term Vision digunakan untuk memisahkan prioritas rilis dari pengembangan masa depan. Detail scope tiap lapisan tetap memerlukan analisis dan persetujuan pemilik.
- Alternatif yang ditolak: Memposisikan Garden Life terutama sebagai farming simulator atau game manajemen pertanian berat, karena tidak sesuai dengan prioritas dekorasi, ekspresi personal, dan pengalaman cozy.
- Dampak:
  - GDD dan Roadmap harus menggunakan identitas ini sebagai acuan saat menyusun player journey, prioritas sistem, dan scope.
  - Fitur baru perlu dinilai berdasarkan kontribusinya terhadap kebun sebagai ruang personal, koleksi, perawatan santai, atau interaksi sosial.
  - D-023 tidak menetapkan fitur baru, angka balancing, maupun scope implementasi First Release.

# DECISIONS · Log Keputusan

Aturan: **hanya ditambah, tidak dihapus.** Untuk mengubah keputusan, tulis entri baru yang menyebut "Menggantikan D-0xx".
Entri terbaru di paling atas.

### D-021 · Setiap buah hanya dapat memperoleh mutasi banjir satu kali
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Menggantikan: D-019 dan D-020 hanya pada bagian apakah buah yang sudah berhasil bermutasi dapat menerima mutasi banjir lanjutan.
- Konteks: Peluang mutasi banjir 5% per menit tetap dapat menghasilkan mutasi berulang pada buah yang sama jika tanaman dibiarkan kebanjiran cukup lama. Mutasi bertumpuk dapat menjadikan membiarkan tanaman dalam kondisi berbahaya sebagai strategi farming yang terlalu menguntungkan.
- Keputusan:
  - Setiap buah hanya dapat berhasil memperoleh mutasi banjir satu kali sepanjang siklus hidup buah tersebut.
  - Setelah mutasi banjir berhasil diterapkan pada sebuah buah, buah itu tidak lagi mengikuti roll mutasi banjir berikutnya.
  - Jika roll gagal, buah tetap eligible untuk roll berikutnya sesuai interval paparan dan peluang yang berlaku pada WaterLevel.
  - Aturan ini tidak mengubah peluang atau interval: WaterLevel 4,00-4,99 tetap 5% per 2 menit paparan; WaterLevel 5,00 tetap 5% per 1 menit paparan, mengikuti D-019 dan D-020.
  - Status keberhasilan mutasi banjir harus disimpan per buah dan divalidasi server-authoritative.
- Alternatif yang ditolak: Mengizinkan mutasi banjir berulang/bertumpuk pada buah yang sama, karena durasi banjir yang lebih lama akan memberi keuntungan mutasi berulang dan mendorong pemain sengaja membiarkan tanaman dalam kondisi berbahaya.
- Dampak: FEAT-002 diperbarui ke v11. Data buah perlu menyimpan penanda apakah mutasi banjir sudah berhasil diterapkan. Buah yang sudah bermutasi tetap dapat dipanen seperti biasa; aturan ini hanya membatasi roll mutasi banjir lanjutan.
 

### D-011 · Area dan penumpukan efek penyiraman
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Menentukan bentuk area penyiraman dan batas penumpukan efek agar Watering Can serta Sprinkler memiliki aturan dasar yang konsisten.
- Keputusan:
  - Area efek penyiraman berbentuk lingkaran.
  - Efek penyiraman dapat bertambah melalui penggunaan berulang atau sumber penyiraman lain, tetapi hanya sampai batas maksimum.
  - Efek gabungan tidak boleh melewati batas maksimum yang ditetapkan dalam balancing.
  - Radius area dan nilai batas maksimum belum ditentukan dan harus ditetapkan dalam spec sebelum implementasi.
- Alternatif yang ditolak: Efek penyiraman tanpa batas, karena dapat mempercepat pertumbuhan secara tidak terkendali dan merusak ekonomi tanaman.
- Dampak: Watering Can dan Sprinkler menggunakan area lingkaran. Sistem pertumbuhan perlu menghitung efek gabungan secara server dan membatasi hasilnya pada cap. Angka radius serta cap tetap menjadi parameter tuning.


### D-012 · Toleransi air dan risiko overwatering tanaman
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Penyiraman yang dapat ditumpuk membutuhkan batas biologis agar pemain tidak memperoleh keuntungan tanpa risiko dari penyiraman berulang.
- Keputusan:
  - Setiap tanaman memiliki batas toleransi terhadap air.
  - Penyiraman berlebihan yang melewati toleransi tanaman dapat menyebabkan tanaman mati.
  - Batas toleransi dapat berbeda antarjenis tanaman dan harus menjadi parameter data tanaman.
  - Nilai toleransi, akumulasi air per aplikasi, pemulihan kadar air, serta durasi/kondisi kematian belum ditentukan dan harus dirinci dalam spec.
- Alternatif yang ditolak: Semua tanaman menerima penyiraman tanpa risiko, karena menghilangkan konsekuensi dari penggunaan alat secara berlebihan.
- Dampak: Sistem tanaman perlu melacak kadar air secara terpisah dari bonus pertumbuhan. Watering Can dan Sprinkler dapat menambah kadar air; sistem harus memeriksa toleransi tanaman secara server-authoritative.

### D-013 · Pemulihan tanaman dari overwatering
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Kematian tanaman akibat kelebihan air perlu memberi konsekuensi tanpa menghukum pemain secara instan.
- Keputusan:
  - Tanaman yang kadar airnya melewati toleransi masuk status Overwatered, bukan langsung mati.
  - Tanaman memiliki kesempatan pulih jika kadar air turun kembali ke atau di bawah batas toleransi sebelum durasi kematian tercapai.
  - Jika tanaman terus berada di atas batas toleransi hingga durasi kematian tercapai, tanaman mati.
  - Pemulihan membatalkan hitungan waktu menuju kematian dan mengembalikan status tanaman ke kondisi tidak Overwatered.
  - Durasi kematian, laju penurunan kadar air, serta aturan apakah tanaman yang pulih mengalami penalti sementara masih harus ditentukan dalam balancing/spec.
- Alternatif yang ditolak: Kematian instan saat toleransi terlampaui; dianggap terlalu menghukum untuk game santai.
- Dampak: Sistem tanaman perlu mencatat awal status Overwatered, mengevaluasi kadar air secara server-authoritative, membatalkan timer kematian ketika kadar air pulih, dan menyimpan status secara aman saat plot unload atau pemain disconnect.

### D-014 · Kebutuhan alat untuk mengurangi kadar air tanah
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Tanaman yang Overwatered membutuhkan cara aktif untuk mengurangi kadar air agar pemain memiliki kesempatan menyelamatkannya sebelum durasi kematian tercapai.
- Keputusan:
  - Garden Life membutuhkan satu tool yang dapat membantu mengurangi kadar air berlebih pada tanah/tanaman.
  - Tool ini menjadi opsi pemulihan aktif selain menunggu kadar air berkurang secara alami.
  - Nama tool, status permanen/consumable, target penggunaan, besaran pengurangan air, dan cooldown BELUM DIPUTUSKAN.
- Alternatif yang ditolak: Hanya mengandalkan pengeringan alami, karena pemain tidak memiliki tindakan langsung untuk menyelamatkan tanaman yang mendekati batas kematian.
- Dampak: FEAT-002 harus mencakup tool pengurang kadar air. Semua angka dan detail operasional wajib ditentukan sebelum spec READY.

### D-015 · Mekanik Soil Aerator
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Pemain membutuhkan cara aktif untuk mengurangi kadar air berlebih pada beberapa tanaman sekaligus tanpa membuat pemulihan terjadi secara instan.
- Keputusan:
  - Nama tool: Soil Aerator.
  - Soil Aerator merupakan consumable.
  - Area efek Soil Aerator berbentuk lingkaran.
  - Soil Aerator mempercepat pengeringan secara bertahap, bukan mengurangi kadar air secara instan.
  - Radius, laju pengeringan, durasi efek, konsumsi per penggunaan, dan aturan penumpukan area masih harus ditetapkan dalam balancing/spec.
- Alternatif yang ditolak: Alat permanen dengan target satu tanaman dan pengurangan instan; pemilik memilih item consumable dengan efek area dan pengeringan bertahap.
- Dampak: FEAT-002 harus memproses pengurangan WaterLevel secara berkala pada tanaman yang berada di area lingkaran selama efek aktif. Pemulihan dari Overwatered tetap mengikuti D-013.

### D-016 · Durasi zona Soil Aerator
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Digantikan oleh D-018
- Konteks: Menentukan lama efek pengeringan area dari satu penggunaan Soil Aerator.
- Keputusan:
  - Satu zona Soil Aerator aktif selama 3 menit (180 detik) sejak aktivasi berhasil.
  - Setelah durasi habis, zona berhenti memberikan efek pengeringan.
  - Radius, interval tick, dan laju pengurangan kadar air masih harus ditentukan melalui balancing.
- Alternatif yang ditolak: Durasi 5 atau 10 menit; pemilik memilih 3 menit.
- Dampak: FEAT-002 harus menghentikan efek zona tepat setelah 180 detik berdasarkan waktu server.

### D-020 · Peluang mutasi banjir diturunkan menjadi 5%
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Menggantikan: D-019 khusus nilai peluang mutasi pada WaterLevel 5,00. Aturan independen per buah dan interval 1 menit tetap berlaku.
- Konteks: Peluang mutasi banjir 15% per buah per menit menghasilkan peluang kumulatif sekitar 91,3% selama 15 roll, terlalu tinggi untuk pengalaman cozy dan durasi kematian tanaman 15 menit.
- Keputusan:
  - Setiap buah memiliki roll mutasi independen; hasil satu buah tidak memengaruhi buah lain.
  - Pada WaterLevel 4,00-4,99, peluang mutasi tetap 5% per buah untuk setiap interval paparan lengkap selama 2 menit.
  - Pada WaterLevel 5,00, peluang mutasi banjir diturunkan dari 15% menjadi 5% per buah untuk setiap interval paparan lengkap selama 1 menit.
  - Roll mutasi diproses server-authoritative.
  - Jika satu buah menerima 15 roll independen pada level 5, peluang kumulatif minimal satu mutasi adalah 1 - (0,95^15) = sekitar 53,7%.
  - Urutan pemrosesan roll interval terakhir dan timer kematian pada batas 15 menit perlu ditetapkan di spec; jika tanaman mati sebelum roll ke-15, hanya 14 roll yang terjadi dan peluang kumulatifnya sekitar 51,2%.
  - Aturan sisa waktu paparan saat WaterLevel berpindah antara 4,00-4,99 dan 5,00, serta apakah buah yang sudah bermutasi dapat mengalami mutasi lanjutan, masih BELUM DIPUTUSKAN.
- Alternatif yang ditolak: Mempertahankan 15% per menit, karena peluang kumulatifnya terlalu tinggi untuk risiko yang seharusnya tetap terasa sebagai kejadian khusus.
- Dampak: FEAT-002 diperbarui ke v10. Risiko mutasi banjir tetap lebih tinggi per satuan waktu daripada mutasi level 4, tetapi tidak lagi hampir pasti selama seluruh jendela Overwatered.

### D-019 · Mutasi buah dihitung secara independen per buah
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif, dengan peluang level 5 digantikan oleh D-020
- Konteks: Mutasi akibat kelebihan air perlu menghasilkan variasi per buah, bukan satu hasil mutasi yang diterapkan ke seluruh tanaman.
- Keputusan:
  - Setiap buah yang terpapar kondisi air berlebih memiliki peluang mutasi sendiri. Hasil roll satu buah tidak memengaruhi buah lain pada tanaman yang sama.
  - Pada WaterLevel 4,00-4,99, peluang mutasi adalah 5% untuk setiap buah pada setiap interval paparan 2 menit.
  - Pada WaterLevel 5,00, peluang mutasi banjir awalnya 15% untuk setiap buah pada setiap interval paparan 1 menit; nilai ini kemudian diturunkan menjadi 5% oleh D-020.
  - Roll mutasi diproses server-authoritative.
  - Aturan akumulasi sisa waktu paparan ketika WaterLevel berpindah antara rentang 4 dan level 5, serta apakah buah yang sudah bermutasi masih dapat mengalami mutasi lanjutan, belum diputuskan dan tidak boleh ditebak saat implementasi.
- Analisis balancing:
  - Analisis awal 15% per roll menghasilkan peluang kumulatif 91,3%; nilai peluang tersebut digantikan oleh D-020.
  - Pada WaterLevel 4 dengan 7 roll independen selama 14 menit, peluang kumulatif minimal satu mutasi adalah 1 - (0,95^7) = sekitar 30,2%.
  - Angka 15% dipilih pemilik sebagai risiko mutasi banjir yang tinggi. Angka ini bukan peluang sekali per tanaman, melainkan per buah per interval.
- Dampak: Setiap buah membutuhkan pencatatan paparan/roll yang cukup agar peluang diterapkan independen dan tidak bergantung pada frekuensi update client.

### D-018 · Skala WaterLevel pecahan dan tuning penyiraman/pengeringan
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Menggantikan: D-017 untuk representasi skala dan nilai perubahan WaterLevel, serta D-016 untuk durasi Soil Aerator. Ketentuan level 4/5 sebagai kondisi berbahaya tetap dipertahankan dengan penyesuaian numerik.
- Konteks: Nilai penyiraman dan pengeringan membutuhkan perubahan pecahan, sehingga WaterLevel integer 0-5 tidak lagi memadai.
- Keputusan:
  - WaterLevel memiliki rentang 0,00 sampai 5,00 dan presisi 0,01. Rekomendasi implementasi: simpan sebagai integer 0-500 dalam satuan seperseratus untuk menghindari galat floating point.
  - Label: 0 = Kering; 1 = Tanah sedikit basah; 2 = Tanah lumayan basah; 3 = Tanah Basah (rekomendasi umum); 4 = Tanah terlalu basah/Overwatered; 5 = Tanah kebanjiran/Flooded. Nilai pecahan di antara label tetap valid.
  - WaterLevel >=4,00 memicu kondisi berbahaya dan timer kematian. Tanaman mati setelah 15 menit terus-menerus berada pada WaterLevel >=4,00. Jika WaterLevel turun di bawah 4,00 sebelum timer habis, tanaman pulih dan timer dibatalkan.
  - Satu tick sistem berdurasi 30 detik.
  - Watering Can menambah WaterLevel 0,50 per penggunaan pada setiap tanaman yang terkena.
  - Sprinkler menambah WaterLevel 0,15 per tick selama 10 menit (600 detik / 20 tick).
  - Soil Aerator mengurangi WaterLevel 0,50 per tick dan zona aktif selama 2,5 menit (150 detik / 5 tick).
  - Pengeringan alami dipicu cuaca panas atau musim Summer. Laju dan interval pengurangan belum ditentukan.
  - Saat WaterLevel mencapai 4,00 atau lebih, Billboard Alert muncul di atas tanaman.
  - Pemicu mutasi buah (nilai awal): pada rentang WaterLevel 4,00-4,99, peluang mutasi 5% per 2 menit paparan; pada WaterLevel 5,00, peluang mutasi banjir 25% per 1 menit paparan. Nilai 25% level 5 kemudian digantikan oleh D-019 menjadi 15% per buah per 1 menit.
- Alternatif yang ditolak: Mempertahankan WaterLevel integer saja, karena tidak dapat mewakili penambahan 0,15 dari Sprinkler.
- Dampak: FEAT-002 dan GDD harus menggunakan skala pecahan yang sama. Seluruh perubahan WaterLevel, timer kematian, dan peluang mutasi dihitung server-authoritative.

### D-017 · Skala kadar air tanaman 0-5
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Digantikan oleh D-018
- Konteks: Sistem kadar air perlu memakai skala sederhana dan mudah dibaca pemain, sekaligus membedakan kelebihan air dari kondisi banjir.
- Keputusan:
  - WaterLevel menggunakan bilangan bulat dari 0 sampai 5.
  - Level 4 berarti Overwatered (kelebihan air).
  - Level 5 berarti Flooded (tanah/tanaman berada dalam kondisi banjir).
  - Level tidak boleh kurang dari 0 atau lebih dari 5.
  - Turun dari level 5 ke level 4 belum memulihkan tanaman; pemulihan baru terjadi ketika WaterLevel turun ke level 3 atau lebih rendah, mengikuti D-013.
  - Episode Overwatered dimulai ketika WaterLevel naik dari level 0-3 ke level 4 atau 5. Timer kematian terus berjalan selama WaterLevel berada pada level 4 atau 5; perpindahan antara level 4 dan 5 tidak memulai ulang timer.
  - Rentang kadar air ideal dapat berbeda menurut jenis tanaman pada level 0-3. Level 4 dan 5 selalu dianggap kondisi kelebihan air.
  - Soil Aerator mengurangi WaterLevel sebanyak 1 level per tick pada setiap tanaman di area lingkaran selama zona aktif. Interval tick masih harus ditentukan melalui balancing.
- Alternatif yang ditolak: Skala kontinu 0-100 untuk WaterLevel, karena pemilik memilih level diskret yang lebih mudah dibaca dan diseimbangkan.
- Dampak: FEAT-002 menggunakan integer WaterLevel 0-5. Logika status tanaman, UI, Watering Can, Sprinkler, pengeringan alami, dan Soil Aerator harus memakai skala yang sama. Rekomendasi interval tick, radius, dan jumlah zona aktif tetap parameter tuning terpisah.

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

### D-010 · Komposisi Starter Kit pemain baru
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Menentukan perlengkapan awal agar pemain dapat memulai pertanian di plot kosong dan memiliki sedikit dekorasi untuk personalisasi.
- Keputusan:
  - Starter Kit gratis berisi 8 jenis item dengan jumlah awal:
    | Item | Jumlah |
    |---|---:|
    | Shovel | 1 |
    | Watering Can | 10 |
    | Pupuk | 1 |
    | Farm Tile | 2 |
    | Trowel | 1 |
    | Benih Wortel | 10 |
    | Kursi Kayu | 1 |
    | Lampu Taman | 1 |
  - Shovel digunakan untuk menghapus tanaman dan merupakan alat permanen, tidak habis karena digunakan.
  - Trowel digunakan untuk memindahkan tanaman dan merupakan alat permanen, tidak habis karena digunakan.
  - Kursi Kayu dan Lampu Taman adalah dua dekorasi dalam Starter Kit.
  - Watering Can berjumlah 10 unit item. Kapasitas, konsumsi air, refill, dan apakah tiap unit merupakan alat terpisah atau persediaan belum ditentukan.
  - Efek numerik, target penggunaan, dan aturan konsumsi Pupuk belum ditentukan.
  - Waktu pemberian Starter Kit dan kebijakan pemberian ulang setelah reset akun tetap BELUM DIPUTUSKAN.
- Alternatif yang ditolak: Starter Kit dekorasi-dominan atau kit tanpa perlengkapan farming; pemilik memilih kit yang memprioritaskan pertanian.
- Dampak: Inventori/onboarding harus memberikan kuantitas di atas tanpa menempatkan objek otomatis di plot. Kit menjadi sumber item awal, bukan sumber Life Coin. Detail alat dan farming harus ditetapkan dalam spec sebelum implementasi.

---

### D-009 · Starter Kit gratis untuk pemain baru
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Plot dimulai kosong sesuai D-008. Pemain tetap membutuhkan cara untuk mulai membangun tanpa harus menghabiskan saldo awal sebelum memahami permainan.
- Keputusan:
  - Pemain baru menerima Starter Kit secara gratis.
  - Starter Kit diberikan sebagai item inventori, bukan objek yang otomatis ditempatkan di plot.
  - Jenis item, jumlah tiap item, waktu pemberian yang tepat, dan apakah kit dapat diperoleh kembali setelah reset akun masih BELUM DIPUTUSKAN.
- Alternatif yang ditolak: Memulai dengan inventori kosong dan mewajibkan pembelian item pertama menggunakan Life Coin; pendekatan ini berisiko menghambat pengalaman awal.
- Dampak: Onboarding dan inventori harus mendukung pemberian item gratis. Starter Kit menjadi sumber item awal (bukan sumber Life Coin); harga toko dan ekonomi tetap perlu diseimbangkan terpisah.

### D-008 · Kondisi awal plot pemain
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Garden Life berfokus pada kreativitas dan ekspresi personal melalui pembangunan serta dekorasi kebun. Kondisi awal plot menentukan seberapa besar ruang kreasi yang dimiliki pemain sejak pertama masuk.
- Keputusan:
  - Saat pertama kali pemain memasuki plot miliknya, area plot dimulai dalam kondisi kosong.
  - Tidak ada dekorasi, bangunan, atau tanaman yang sudah ditempatkan di plot pada kondisi awal.
  - Keputusan ini mengatur objek yang sudah berada di dunia/plot, bukan isi inventori. Starter inventory, hadiah tutorial, dan item awal masih belum diputuskan.
- Alternatif yang ditolak: Kebun starter yang sudah memiliki dekorasi dan tanaman; ditolak agar pemain membentuk identitas kebunnya sendiri sejak awal.
- Dampak: Onboarding perlu membantu pemain memperoleh atau menempatkan objek pertama tanpa mengandalkan dekorasi bawaan. Isi starter inventory dan hadiah tutorial harus dirancang terpisah dan tidak boleh diasumsikan dari keputusan ini.

### D-007 · Skala world grid dan footprint tile
- Tanggal: 2026-11-15
- Diputuskan oleh: ChatGPT (rekomendasi desain; disetujui melalui delegasi pemilik)
- Status: Aktif
- Konteks: Istilah grid 5×5 perlu diterjemahkan menjadi ukuran dunia Roblox yang konsisten dengan ukuran plot dan mudah digunakan untuk menyusun tile.
- Keputusan:
  - Satu sel grid berukuran 4 × 4 studs.
  - Satu Farm Tile atau Build Tile memiliki footprint 5 × 5 sel grid, yaitu 20 × 20 studs.
  - Ukuran plot Stage 1 sebesar 80 × 80 studs setara dengan area 4 × 4 footprint tile; Stage 2 = 8 × 8, Stage 3 = 12 × 12, dan Stage 4 = 16 × 16 footprint tile.
  - Ukuran 4 studs per sel menjadi unit grid dasar untuk placement tile. Objek free placement tetap mengikuti aturan free placement; Snap to Grid menggunakan kelipatan unit grid ini kecuali aturan asset tertentu ditetapkan kemudian.
- Alternatif yang ditolak: 1 stud per sel karena menghasilkan footprint tile 5 × 5 studs dan grid sangat rapat; 5 studs per sel karena footprint tile menjadi 25 × 25 studs dan tidak membagi ukuran plot 80 studs secara utuh.
- Dampak: FEAT-001 dan asset pipeline harus menggunakan skala grid 4 studs. Tile perlu memiliki footprint 20 × 20 studs. Batas pivot, origin grid plot, toleransi snapping, dan ukuran bounding volume asset tetap harus ditentukan secara teknis tanpa mengubah unit dasar ini.

### D-006 · Hak Build multiplayer berdasarkan kepemilikan objek
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Menetapkan batas kolaborasi Build Mode agar anggota dapat berkontribusi pada kebun bersama tanpa kehilangan kendali atas objek yang mereka miliki.
- Keputusan:
  - Original Owner memiliki hak pengelolaan penuh atas Build Mode dan seluruh objek pada plot.
  - Active Owner memiliki hak pengelolaan penuh selama memegang kendali aktif plot.
  - Anggota dapat memasang objek dari inventori miliknya sendiri.
  - Anggota dapat memindahkan dan menyimpan hanya objek yang OwnerUserId-nya sama dengan UserId anggota tersebut.
  - Anggota tidak dapat memindahkan atau menyimpan objek milik pemain lain.
  - Anggota tidak dapat mengelola hak anggota plot.
  - Server wajib memvalidasi peran pemain dan kepemilikan objek untuk setiap operasi Place, Move, dan Store; UI client bukan sumber otoritas izin.
- Alternatif yang ditolak: Semua anggota dapat mengubah semua objek, karena berisiko menghilangkan hasil dekorasi pemain lain; hanya Original Owner yang boleh Build, karena terlalu membatasi co-op.
- Dampak: FEAT-001 harus menerapkan pemeriksaan izin berbasis peran dan OwnerUserId. Original Owner dan Active Owner dapat membantu mengatur seluruh kebun, sedangkan anggota memiliki ruang kontribusi yang terbatas pada objek sendiri. Hak Shared Savings, farming, undangan, dan pengelolaan anggota di luar Build Mode tidak ditentukan oleh keputusan ini.

### D-005 · Hybrid Collision untuk Build Mode
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Menjaga struktur bangunan tetap rapi tanpa menghilangkan kebebasan menyusun tanaman dan dekorasi kecil.
- Keputusan: Build Mode menggunakan Hybrid Collision. GroundTile tidak boleh bertumpuk dengan GroundTile lain dan tidak memblokir objek di atasnya. Solid (bangunan/objek besar) tidak boleh bertabrakan dengan Solid atau Detail. Detail (tanaman/dekorasi kecil) boleh bertumpuk dengan Detail lain, tetapi tidak boleh menembus Solid. Setiap asset wajib memiliki PlacementProfile dan bounding volume.
- Alternatif yang ditolak: Strict Placement untuk semua objek karena terlalu membatasi dekorasi; Full Free Placement karena memungkinkan bangunan saling menembus.
- Dampak: Metadata setiap asset harus mendefinisikan profil tabrakan dan bounding volume. Surface placement seperti pot di atas meja belum termasuk dan memerlukan aturan terpisah.

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
