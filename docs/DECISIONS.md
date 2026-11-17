### D-041 · Identitas visual musim Summer: Golden Summer
- Tanggal: 2026-11-17
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Setelah eksplorasi identitas Spring, musim berikutnya yang dibahas adalah Summer. Setiap musim perlu memiliki identitas suasana yang mudah dikenali.
- Keputusan:
  - Identitas visual dan suasana Summer menggunakan konsep **Golden Summer**.
  - Summer harus terasa **cerah dan hangat**.
  - Keputusan ini menetapkan arah suasana musim, bukan detail final lingkungan, palet warna, aset visual, kalender, distribusi cuaca, atau mekanik gameplay.
  - Seasons & Weather tetap berstatus eksplorasi dan tidak otomatis menjadi scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menetapkan identitas Summer yang redup atau dingin sebagai arah utama musim.
- Dampak:
  - Eksplorasi visual Summer berikutnya harus konsisten dengan suasana cerah dan hangat.
  - Mekanik gameplay dan ekonomi Summer masih perlu dirancang terpisah; belum ada angka balancing yang ditetapkan.
  - Tidak ada spec yang dinaikkan menjadi READY.
- Hal yang masih BELUM DIPUTUSKAN:
  - Palet warna, tampilan langit, pencahayaan, vegetasi, bunga, dan lingkungan khas Summer.
  - Roster cuaca, distribusi, durasi, dan transisi cuaca Summer.
  - Efek cuaca pada WaterLevel, pertumbuhan, buah, Mutation, serta kondisi tanaman.
  - Tanaman musiman, kalender, dan hubungan Summer dengan sistem musim lainnya.
  - Apakah dan kapan Seasons & Weather masuk scope rilis.

### D-040 · Efek penggunaan Vitamin untuk memulihkan tanaman Scorched
- Tanggal: 2026-11-17
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: D-039 menetapkan Vitamin sebagai satu-satunya cara memulihkan tanaman Scorched. Efek dan jumlah konsumsi item perlu ditentukan agar perilaku pemulihan jelas.
- Keputusan:
  - Menggunakan **1 item Vitamin** pada **1 tanaman Scorched** menghilangkan status Scorched dari tanaman tersebut.
  - Satu item Vitamin hanya dapat memulihkan satu tanaman.
  - Pemulihan hanya menghapus status Scorched. Vitamin tidak mengubah atau mereset umur tanaman, ukuran tanaman, maupun progres pertumbuhan yang sudah dimiliki.
  - Setelah status Scorched dihapus, tanaman kembali menghasilkan jumlah buah normal sesuai aturan tanaman tersebut.
  - Vitamin tidak dapat digunakan pada tanaman yang tidak berstatus Scorched; aturan konsumsi pada percobaan penggunaan yang tidak valid perlu mengikuti validasi server dan tidak boleh menghabiskan item.
  - Cara memperoleh Vitamin, harga, batas stack inventori, tampilan UI, animasi, dan feedback penggunaan masih BELUM DIPUTUSKAN.
  - Aturan ini merupakan rancangan konsep Thunderstorm dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menggunakan lebih dari satu Vitamin untuk satu tanaman; mereset umur, ukuran, atau progres pertumbuhan saat pemulihan; atau membuat Vitamin mengubah parameter tanaman selain status Scorched.
- Dampak:
  - Sistem item perlu mengonsumsi satu Vitamin untuk satu pemulihan tanaman Scorched.
  - Sistem kondisi tanaman menghapus Scorched setelah penggunaan valid dan mempertahankan state tanaman lainnya.
  - Sistem panen kembali menggunakan hasil normal setelah Scorched dihapus.
  - Vitamin menjadi item pemulihan dan penguras inventori; harga serta sumber perolehannya belum ditetapkan sehingga dampak Life Coin belum dapat dihitung.
  - Tidak ada spec yang dinaikkan menjadi READY.
- Hal yang masih BELUM DIPUTUSKAN:
  - Cara memperoleh Vitamin dan harga toko atau sumber lainnya.
  - Batas stack dan kapasitas inventori Vitamin.
  - UI, animasi, feedback, serta cara memilih tanaman target.
  - Detail kondisi tanaman mati, konversi menjadi pupuk, dan revive Robux sesuai D-038.

### D-039 · Status Scorched dan penalti hasil buah
- Tanggal: 2026-11-17
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Tanaman yang terkena hasil kerusakan gosong dari Thunderstorm perlu memiliki identitas visual, penalti hasil panen, dan jalur pemulihan yang jelas.
- Keputusan:
  - Tanaman dengan kondisi **Scorched** ditampilkan berwarna hitam seperti tanaman yang hangus terbakar.
  - Tanaman Scorched hanya menghasilkan **50% dari jumlah buah normal** pada setiap hasil panen selama status tersebut aktif.
  - Jumlah buah hasil panen Scorched dihitung dengan rumus: `floor(jumlah_buah_normal × 0,5)`. Hasil selalu dibulatkan ke bawah ke bilangan bulat.
  - Jika jumlah buah normal adalah 1, tanaman Scorched menghasilkan **0 buah**.
  - Status Scorched tidak memiliki batas waktu dan tidak pulih secara otomatis.
  - Satu-satunya cara menghilangkan status Scorched adalah menggunakan item **Vitamin**.
  - Jumlah Vitamin yang dibutuhkan, aturan konsumsi item, target penggunaan, animasi/UI, dan detail efek pemulihan masih BELUM DIPUTUSKAN.
  - Aturan ini merupakan rancangan konsep Thunderstorm dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Membatasi penalti berdasarkan timer atau memulihkan Scorched secara otomatis; membulatkan hasil buah ke atas; atau menjamin minimal satu buah untuk tanaman yang normalnya menghasilkan satu buah.
- Dampak:
  - Sistem panen perlu menerapkan hasil 50% dengan pembulatan ke bawah pada tanaman berstatus Scorched.
  - Sistem kondisi tanaman perlu mempertahankan Scorched sampai item Vitamin berhasil digunakan.
  - Visual tanaman perlu membedakan kondisi Scorched melalui tampilan hitam seperti hangus.
  - Tanaman dengan hasil normal satu buah tidak menghasilkan buah selama Scorched, sehingga pemulihan menggunakan Vitamin menjadi penting.
  - Harga, ketersediaan, dan konsumsi Vitamin belum ditentukan; dampak ekonomi belum dapat dihitung.
  - Tidak ada spec yang dinaikkan menjadi READY.
- Hal yang masih BELUM DIPUTUSKAN:
  - Jumlah Vitamin yang digunakan per tanaman dan apakah satu item menyembuhkan satu tanaman.
  - Cara memperoleh Vitamin, harga toko, dan apakah Vitamin dapat ditumpuk dalam inventori.
  - UI, animasi, dan feedback saat Vitamin digunakan.
  - Penalti pertumbuhan atau efek lain selain pengurangan jumlah buah; saat ini hanya penalti hasil buah yang dikonfirmasi.
  - Detail kondisi tanaman mati, konversi menjadi pupuk, dan revive Robux tetap terbuka sesuai D-038.

### D-038 · Aturan gameplay Thunderstorm, sambaran petir, dan item perlindungan
- Tanggal: 2026-11-16
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Thunderstorm menjadi cuaca Spring yang jarang menimbulkan sambaran di plot pemain, memberi peluang Mutation eksklusif, tetapi membawa risiko kerusakan tanaman yang dapat dikurangi melalui item perlindungan.
- Keputusan:
  - Thunderstorm mengikuti durasi cuaca non-Sunny pada D-031, yaitu **20 tick / 10 menit**, dengan satu tick setiap **30 detik**.
  - Pada setiap tick Thunderstorm, setiap plot melakukan roll sambaran secara independen dengan peluang **1% per plot per tick**.
  - Maksimal terjadi **5 sambaran per plot dalam satu episode Thunderstorm**. Batas ini menghitung seluruh kejadian sambaran, termasuk sambaran yang berhasil dialihkan oleh Lightning Rod.
  - Dengan 20 roll independen pada peluang 1%, peluang satu plot mengalami setidaknya satu sambaran dalam satu episode adalah sekitar **18,21%** sebelum memperhitungkan batas maksimum; jumlah sambaran rata-rata teoritis adalah **0,2 per episode**.
  - Titik sambaran ditentukan secara acak di dalam plot. Area dampak setiap sambaran berbentuk lingkaran dengan radius **8 studs**. Hanya tanaman yang berada di dalam area dampak yang terkena efek sambaran.
  - Setiap buah pada tanaman yang terkena sambaran memperoleh Mutation **Shocked** dengan peluang **100%** dan melakukan roll Mutation **Charged** secara independen dengan peluang **15%**. Shocked dan Charged dapat dimiliki bersamaan pada buah yang sama sesuai D-022. Multiplier harga dan tampilan kedua Mutation masih BELUM DIPUTUSKAN.
  - Hasil kondisi tanaman akibat satu sambaran bersifat saling eksklusif: **60% tidak mengalami kerusakan**, **25% menjadi gosong**, dan **15% mati**.
  - Tanaman gosong masih dapat dirawat, tetapi penalti dan durasi efeknya masih BELUM DIPUTUSKAN.
  - Tanaman mati tidak dapat dipulihkan melalui perawatan biasa. Pemain dapat membuangnya, mengolahnya menjadi pupuk, atau memilih opsi revive menggunakan Robux. Harga Robux, hasil pupuk, dan aturan revive masih BELUM DIPUTUSKAN.
  - WaterLevel selama Thunderstorm bertambah **0,075 per tick**, mengikuti Rainy pada D-034 dan presisi D-033.
  - Seluruh tanaman menerima tambahan waktu pertumbuhan **20%** selama Thunderstorm, mengikuti Rainy pada D-034. Thunderstorm tidak memberikan bonus atau percepatan pertumbuhan.
  - **Lightning Rod** memiliki area berbentuk lingkaran dengan radius **24 studs**. Setiap kejadian sambaran yang titiknya berada dalam area tersebut memiliki peluang **50%** untuk dialihkan ke Lightning Rod. Satu Lightning Rod dapat menahan maksimal **3 sambaran yang berhasil dialihkan**, lalu habis/tidak lagi memberi perlindungan. Sambaran yang dialihkan tetap dihitung terhadap batas 5 sambaran per plot per episode.
  - **Thunderstorm Relief** memiliki area berbentuk lingkaran dengan radius **20 studs**. Tanaman di dalam area menerima pengurangan peluang gosong sebesar **5 poin persentase** dan pengurangan peluang mati sebesar **5 poin persentase** per stack aktif.
  - Thunderstorm Relief dapat ditumpuk maksimal **3 item** pada area yang sama. Tiga stack aktif menurunkan peluang gosong dari 25% menjadi 10% dan peluang mati dari 15% menjadi 0%; peluang tidak rusak menjadi 90%.
  - Setiap Thunderstorm Relief memiliki durabilitas **3 sambaran yang dilindungi** secara individual. Setiap sambaran mengurangi durabilitas **masing-masing item Relief yang area lingkarannya mencakup titik sambaran sebesar 1**, secara bersamaan dan independen. Jika satu sambaran berada di area dua Relief, kedua item masing-masing kehilangan 1 durabilitas; jika berada di area tiga Relief, ketiganya masing-masing kehilangan 1 durabilitas. Item yang tidak mencakup titik sambaran tidak kehilangan durabilitas. Setelah suatu item kehabisan 3 durabilitas, item tersebut tidak lagi memberi pengurangan risiko. Pengurangan risiko pada tanaman dihitung dari jumlah item Relief aktif yang area lingkarannya mencakup tanaman tersebut: 5 poin persentase untuk gosong dan 5 poin persentase untuk mati per item aktif.
  - Efek perlindungan berlaku pada tanaman yang berada di dalam area lingkaran masing-masing item. Tanaman di luar area tidak menerima efeknya.
  - Aturan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Membuat Thunderstorm sebagai cuaca yang sering menyambar; memberi efek kerusakan seluruh plot; atau menjadikan risiko gosong dan mati dapat terjadi bersamaan pada satu hasil sambaran.
- Dampak:
  - Sistem cuaca perlu menjalankan roll sambaran independen per plot setiap tick Thunderstorm dan membatasi total kejadian per plot per episode menjadi 5.
  - Sistem sambaran perlu menentukan titik dampak acak, menghitung tanaman dalam radius 8 studs, lalu memproses pengalihan Lightning Rod dan perlindungan Thunderstorm Relief.
  - Sistem Mutation perlu memberikan Shocked kepada seluruh buah pada tanaman yang terkena dan melakukan roll Charged 15% per buah.
  - Sistem kondisi tanaman perlu memilih tepat satu hasil dari tidak rusak/gosong/mati sesuai peluang yang ditetapkan dan menghitung pengurangan risiko dari Relief aktif.
  - Thunderstorm Relief menambahkan mekanisme perlindungan area dan durabilitas item; Lightning Rod menambahkan mekanisme pengalihan sambaran.
  - Mutation dan opsi revive Robux berpotensi memengaruhi ekonomi/monetisasi. Multiplier Mutation, penalti gosong, hasil pupuk, dan harga revive belum ditetapkan sehingga dampak ekonomi final belum dapat dihitung.
  - Tidak ada spec yang dinaikkan menjadi READY.
- Hal yang masih BELUM DIPUTUSKAN:
  - Perilaku beberapa Lightning Rod dengan area tumpang tindih: urutan roll pengalihan atau pemilihan satu rod.
  - Penalti dan durasi status gosong.
  - Detail pemulihan tanaman gosong, hasil konversi tanaman mati menjadi pupuk, dan harga/aturan revive Robux.
  - Multiplier harga dan tampilan visual Mutation Shocked/Charged.
  - Aturan penanaman tanaman baru saat Thunderstorm sedang berlangsung.
  - Peluang kemunculan Thunderstorm dalam distribusi cuaca Spring dan aturan transisinya.

### D-037 · Aturan gameplay cuaca Misty dan evolusi Foggy
- Tanggal: 2026-11-16
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Misty perlu memiliki identitas gameplay berbasis Mutation yang berbeda dari cuaca hujan, dengan Foggy sebagai evolusi langka dari Misty.
- Keputusan:
  - Selama Misty, WaterLevel setiap tanaman yang terkena efek cuaca bertambah **0,25 satu kali saat episode Misty dimulai**, mengikuti aturan Cloudy. Tidak ada penambahan WaterLevel berkala selama episode.
  - Seluruh tanaman menerima tambahan waktu pertumbuhan **15%** selama Misty, mengikuti modifier pertumbuhan Drizzle. Misty tidak memberikan bonus atau percepatan pertumbuhan.
  - Setiap tick, setiap buah eligible yang **belum memiliki Mutation Misty** melakukan roll secara independen untuk memperoleh Mutation **Misty** dengan peluang **6,697% per buah per tick**.
  - Peluang 6,697% menghasilkan peluang kumulatif sekitar **75%** setelah 20 roll independen pada satu buah yang eligible sepanjang episode penuh.
  - Setiap tick, setiap buah yang **sudah memiliki Mutation Misty dan belum memiliki Foggy** melakukan roll evolusi secara independen dengan peluang **0,809% per buah per tick** untuk berevolusi menjadi Mutation **Foggy**.
  - Peluang 0,809% menghasilkan peluang kumulatif sekitar **15% setelah 20 roll evolusi eligible**. Karena buah baru eligible setelah memperoleh Misty, jumlah roll evolusi aktual dalam satu episode dapat kurang dari 20; peluang Foggy aktual per episode karena itu bergantung pada tick saat Misty diperoleh.
  - Jika evolusi berhasil, Mutation Misty **digantikan** oleh Mutation Foggy. Misty tidak lagi tercatat pada buah tersebut dan multiplier Misty tidak lagi berlaku; multiplier Foggy masih BELUM DIPUTUSKAN.
  - Roll Mutation Misty dan evolusi Misty→Foggy dilakukan independen per buah. Buah yang telah memiliki Misty tidak lagi melakukan roll Misty; buah yang telah berevolusi menjadi Foggy tidak lagi melakukan roll evolusi.
  - Tick Misty mengikuti interval 30 detik dan durasi cuaca non-Sunny mengikuti D-031, yaitu 20 tick / 10 menit.
  - Aturan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menumpuk Misty dan Foggy pada buah yang sama setelah evolusi; Foggy dipilih sebagai evolusi yang menggantikan Mutation asal agar status evolusi tetap tunggal dan jelas.
- Dampak:
  - Sistem cuaca perlu menjalankan roll Misty per buah yang belum memiliki Misty dan roll evolusi Foggy hanya pada buah yang telah memiliki Misty.
  - Sistem Mutation perlu mengganti status Misty menjadi Foggy ketika evolusi berhasil, bukan menyimpan keduanya.
  - Sistem WaterLevel perlu menerapkan kenaikan satu kali +0,25 pada awal episode Misty.
  - Sistem pertumbuhan perlu menerapkan tambahan waktu 15% untuk seluruh tanaman selama Misty.
  - Multiplier harga dan tampilan visual Mutation Misty/Foggy masih belum ditentukan; dampak ekonomi belum dapat dihitung.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-036 · Aturan gameplay cuaca Windy
- Tanggal: 2026-11-16
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Windy perlu menjadi cuaca ringan yang mendukung perawatan dan pertumbuhan tanaman tanpa menambahkan tekanan atau Mutation.
- Keputusan:
  - Windy digambarkan sebagai **angin sepoi-sepoi**, bukan angin kencang.
  - Selama Windy, WaterLevel setiap tanaman yang terkena efek cuaca berkurang **0,005 setiap 2 tick**. Satu tick berdurasi 30 detik berdasarkan D-018, sehingga pengurangan terjadi setiap 60 detik.
  - WaterLevel tidak boleh turun di bawah **0,000**. Perhitungan mengikuti presisi internal 0,001 dari D-033.
  - Selama Windy, kecepatan seluruh proses pertumbuhan tanaman dan pertumbuhan buah menjadi **1,5x** dari kecepatan normal (1,0x). Ini adalah multiplier laju pertumbuhan, bukan perubahan permanen pada durasi dasar tanaman.
  - Bonus kecepatan 1,5x berlaku untuk **semua tanaman**, tanpa pengecualian berdasarkan kebutuhan sinar matahari.
  - Windy **tidak menghasilkan Mutation**.
  - Durasi Windy mengikuti aturan cuaca non-Sunny pada D-031, yaitu 20 tick / 10 menit.
  - Aturan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menggambarkan Windy sebagai angin kencang; memberi efek pertumbuhan hanya pada klasifikasi tanaman tertentu; atau menghasilkan Mutation dari Windy.
- Dampak:
  - Sistem WaterLevel perlu mengurangi nilai sebesar 0,005 pada interval dua tick selama Windy, dengan batas minimum 0,000.
  - Sistem pertumbuhan perlu menerapkan multiplier laju 1,5x pada seluruh tanaman dan proses pertumbuhan buah selama episode Windy.
  - Windy tidak menambah jalur perolehan Mutation dan tidak menambah multiplier harga buah.
  - Pengurangan WaterLevel dapat membantu mengurangi risiko overwatering, sementara percepatan pertumbuhan dapat meningkatkan frekuensi panen. Dampak ekonomi perlu dievaluasi setelah data tanaman, harga jual, dan durasi pertumbuhan ditetapkan.
  - Tidak ada spec yang dinaikkan menjadi READY.


### D-032 · Skip Tutorial dan mulai ulang tutorial dari Pengaturan
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Pemain perlu memiliki pilihan yang jelas untuk melewati panduan awal tanpa kehilangan akses gameplay, sekaligus tetap dapat mempelajari tutorial kembali jika berubah pikiran.
- Keputusan:
  - Setelah pemain menutup Inventory pada alur First Visit, tampilkan panel pilihan aktivitas yang berisi **Mulai Bertani**, **Mulai Mendekorasi**, dan **Skip Tutorial**.
  - Panel pilihan aktivitas hanya ditampilkan satu kali dalam satu rangkaian tutorial. Panel tidak muncul kembali secara otomatis setelah pemain memilih salah satu jalur atau Skip Tutorial.
  - Jika pemain memilih **Skip Tutorial**, tutup panel dan tandai onboarding sebagai selesai/dilewati. Pemain tidak menerima panduan jalur bertani maupun jalur dekorasi pada rangkaian tersebut.
  - Skip Tutorial tidak mengunci atau menyembunyikan fitur gameplay. Pemain tetap dapat menggunakan Inventory, bertani, mendekorasi, dan mengakses seluruh fitur yang tersedia secara normal.
  - Jika pemain memilih Mulai Bertani atau Mulai Mendekorasi, jalankan panduan jalur yang dipilih sesuai D-025. Onboarding selesai setelah satu tindakan kreatif berhasil.
  - Sediakan opsi **Mulai Ulang Tutorial** pada menu Pengaturan. Saat dipilih, tutorial dimulai kembali dari tahap pengenalan Inventory, kemudian berlanjut ke panel pilihan aktivitas dan panduan jalur.
  - Mulai Ulang Tutorial tidak mengulang pesan sambutan D-026. Pesan sambutan tetap hanya menjadi bagian dari kedatangan pertama pemain.
  - Memulai ulang tutorial hanya mengulang state/panduan onboarding. Tidak boleh mereset atau mengubah Life Coin, inventori, Starter Kit, objek yang telah ditempatkan, tanaman, atau progres gameplay pemain.
  - Setelah tutorial selesai atau dilewati, pemain dapat memulainya kembali secara manual melalui Pengaturan.
  - Perilaku penyimpanan dan pemulihan state tutorial ketika pemain disconnect atau keluar di tengah tutorial masih perlu dirinci dalam spec; D-032 tidak menetapkan aturan sesi tersebut.
- Alternatif yang ditolak: Menggunakan tombol "Nanti saja" yang menyiratkan panel akan muncul lagi otomatis; menjadikan panel pilihan aktivitas sebagai fitur permanen; atau mengulang pesan sambutan saat tutorial dimulai ulang.
- Dampak:
  - D-032 melengkapi D-025 dan alur First Visit; tidak menggantikan D-025, D-026, atau D-027.
  - PLAYER_JOURNEY.md dan GDD diperbarui untuk membedakan penyelesaian tutorial, skip, dan restart manual.
  - Menu Pengaturan membutuhkan entri **Mulai Ulang Tutorial**.
  - Tidak ada perubahan pada Starter Kit, inventori, ekonomi, atau akses gameplay.
  - Tidak ada spec yang dinaikkan menjadi READY.


### D-033 · Presisi internal WaterLevel hingga seperseribu
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Menggantikan: Ketentuan presisi 0,01 dan representasi integer seperseratus pada D-018; rentang WaterLevel, batas, label, dan aturan lain D-018 tetap berlaku.
- Konteks: Efek cuaca Rainy membutuhkan penambahan WaterLevel +0,075 per tick. Presisi 0,01 akan memaksa pembulatan dan membuat total perubahan selama satu episode tidak akurat.
- Keputusan:
  - WaterLevel tetap memiliki rentang 0,00 sampai 5,00.
  - Nilai WaterLevel disimpan secara internal dengan presisi 0,001, direpresentasikan sebagai integer 0-5000 dalam satuan seperseribu (misalnya field konseptual `WaterLevelMilli`).
  - UI tetap menampilkan WaterLevel dengan 2 angka desimal. Tampilan dibulatkan untuk presentasi saja; nilai internal tidak boleh dibulatkan pada setiap tick.
  - Semua perubahan WaterLevel dihitung dari nilai internal presisi 0,001, lalu dibatasi pada rentang 0,000-5,000.
  - Contoh: Rainy menambah 0,075 per tick. Setelah 20 tick, total kenaikan adalah tepat 1,500 sebelum penerapan batas maksimum 5,000.
  - D-033 mengubah presisi penyimpanan dan perhitungan, bukan nilai balancing Watering Can, Sprinkler, Soil Aerator, Cloudy, atau Drizzle.
- Alternatif yang ditolak: Membulatkan +0,075 menjadi +0,08 setiap tick, karena menghasilkan total +1,60 setelah 20 tick dan mengubah balancing yang dipilih.
- Dampak:
  - Representasi WaterLevel pada GDD dan FEAT-002 harus menggunakan integer seperseribu.
  - UI tetap menggunakan format dua angka desimal agar mudah dibaca.
  - Semua operasi perubahan WaterLevel wajib server-authoritative.
  - D-033 tidak mengubah rentang bahaya, timer kematian, atau batas maksimum D-018.

### D-034 · Aturan gameplay cuaca Rainy
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Rainy perlu terasa lebih intens daripada Drizzle, tetapi tetap nyaman dan menenangkan, bukan badai atau cuaca ekstrem.
- Keputusan:
  - Rainy memiliki intensitas hujan sedang hingga deras dengan suasana tetap tenang, sejuk, dan sedikit sendu. Rainy bukan Thunderstorm.
  - Selama Rainy, WaterLevel setiap tanaman yang terkena efek cuaca bertambah **0,075 per tick**.
  - Setiap tick, setiap buah eligible melakukan roll Mutation **Wet (Basah)** secara independen dengan peluang **5% per buah per tick**.
  - Setiap tick, buah yang telah memiliki Mutation Wet dan masih eligible melakukan roll evolusi Wet menjadi Mutation **Flooded** dengan peluang **2,5% per buah per tick**.
  - Ketika evolusi berhasil, Mutation Wet digantikan oleh Mutation Flooded pada buah tersebut. Wet tidak lagi tercatat pada buah itu dan multiplier Wet tidak lagi berlaku; multiplier Flooded yang berlaku masih BELUM DIPUTUSKAN.
  - Flooded dari evolusi Rainy adalah Mutation yang sama dengan Flooded yang dapat diperoleh melalui paparan WaterLevel tinggi. Batas satu kali Flooded per buah mengikuti D-035.
  - Seluruh tanaman menerima tambahan waktu pertumbuhan **20%** selama Rainy, tanpa membedakan klasifikasi kebutuhan sinar matahari.
  - Rainy tidak memberikan bonus atau percepatan pertumbuhan.
  - WaterLevel tidak boleh melampaui 5,00. Perhitungan mengikuti presisi internal 0,001 dari D-033.
  - Tick Rainy mengikuti interval 30 detik pada D-018 dan durasi episode mengikuti D-031, yaitu 20 tick / 10 menit.
  - Efek visual dan audio Rainy harus membedakannya dari Drizzle melalui hujan yang lebih tebal/deras, langit lebih kelabu, dedaunan basah, dan genangan kecil/refleksi; detail asset final belum ditetapkan.
  - Peluang kemunculan Rainy, aturan transisi, multiplier dan tampilan Mutation Wet/Flooded, serta penerapan modifier pada tanaman yang baru ditanam ketika Rainy sedang berlangsung masih BELUM DIPUTUSKAN.
  - Aturan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menyamakan Rainy dengan Drizzle; memberi bonus pertumbuhan; atau menjadikan Rainy sebagai badai/Thunderstorm.
- Dampak:
  - Sistem cuaca perlu menjalankan roll Wet dan evolusi Wet→Flooded secara independen per buah eligible.
  - Sistem pertumbuhan perlu menerapkan tambahan waktu 20% untuk semua tanaman.
  - Sistem WaterLevel harus mempertahankan pecahan 0,075 tanpa pembulatan per tick sesuai D-033.
  - Flooded tetap dibatasi satu kali per buah dan berbagi identitas Mutation dengan jalur WaterLevel tinggi sesuai D-035.
  - Tidak ada perubahan source/sink ekonomi yang ditetapkan; multiplier Mutation masih terbuka.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-035 · Peluang Mutation Flooded dan batas satu kali per buah
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Menggantikan: Nilai peluang mutasi banjir pada D-019 dan D-020. Ketentuan satu kali berhasil per buah pada D-021 tetap berlaku dan diperjelas lintas semua jalur perolehan.
- Konteks: Mutation Flooded memiliki dua jalur perolehan, yaitu evolusi Wet selama Rainy dan paparan WaterLevel tinggi. Peluang jalur WaterLevel perlu diturunkan agar seimbang dengan jalur cuaca.
- Keputusan:
  - Pada WaterLevel **4,00-4,99**, setiap buah eligible melakukan roll Mutation Flooded dengan peluang **2,5% per interval paparan 2 menit**.
  - Pada WaterLevel **5,00**, setiap buah eligible melakukan roll Mutation Flooded dengan peluang **2,5% per interval paparan 1 menit**.
  - Interval paparan tetap mengikuti ketentuan D-019 dan D-020; hanya peluangnya yang diubah dari 5% menjadi 2,5%.
  - Mutation Flooded yang diperoleh dari Rainy dan Mutation Flooded yang diperoleh dari WaterLevel tinggi adalah jenis Mutation yang sama.
  - Satu buah hanya dapat memperoleh Mutation Flooded **satu kali sepanjang siklus hidup buah**, tanpa memandang jalur perolehannya.
  - Jika buah memperoleh Flooded melalui evolusi Wet saat Rainy, buah tidak lagi eligible untuk roll Flooded dari WaterLevel tinggi. Jika buah memperoleh Flooded dari WaterLevel tinggi lebih dahulu, buah tidak lagi eligible untuk evolusi Wet menjadi Flooded.
  - Evolusi Wet menjadi Flooded menggantikan Wet sesuai D-034; aturan umum Mutation lain tetap mengikuti D-022.
  - Aturan akumulasi sisa waktu paparan ketika WaterLevel berpindah antara rentang 4,00-4,99 dan 5,00 masih BELUM DIPUTUSKAN.
  - Keputusan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Mempertahankan peluang 5% pada kedua rentang WaterLevel; peluang yang lebih tinggi berisiko membuat Flooded terlalu sering diperoleh selama paparan berbahaya.
- Dampak:
  - D-019 dan D-020 tetap tersimpan sebagai riwayat, tetapi angka peluang aktif digantikan oleh D-035.
  - FEAT-002 dan GDD harus menampilkan peluang 2,5% pada kedua rentang WaterLevel.
  - Status Flooded harus disimpan per buah dan mencegah roll dari semua jalur setelah berhasil.
  - Tidak ada multiplier harga yang ditetapkan; dampak ekonomi masih perlu dianalisis setelah multiplier Mutation diputuskan.
  - Tidak ada spec yang dinaikkan menjadi READY.


### D-031 · Durasi standar episode cuaca non-Sunny
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Sistem cuaca membutuhkan durasi episode yang konsisten agar efek lingkungan, pergantian cuaca, dan perhitungan tick dapat dirancang serta diuji secara terukur.
- Keputusan:
  - Setiap episode cuaca selain **Sunny** berlangsung selama **20 tick**, setara dengan **600 detik atau 10 menit**.
  - Satu tick cuaca berdurasi **30 detik**, mengikuti interval tick lingkungan yang telah digunakan pada D-018.
  - Aturan durasi ini berlaku untuk seluruh cuaca non-Sunny, bukan hanya roster Spring.
  - **Sunny dikecualikan** dari durasi standar ini. Durasi Sunny masih BELUM DIPUTUSKAN.
  - Durasi episode tidak menetapkan peluang kemunculan, urutan transisi, atau jeda antarcuaca.
  - Keputusan ini merupakan aturan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Menggunakan durasi acak untuk setiap episode cuaca non-Sunny sebelum ada kebutuhan desain khusus.
- Dampak:
  - Semua efek cuaca berkala dapat menggunakan 20 tick sebagai durasi episode standar non-Sunny.
  - Efek per tick harus dihentikan setelah episode berakhir dan tidak boleh berjalan melewati batas episode.
  - Sistem cuaca perlu membedakan Sunny dari cuaca lain saat menentukan durasi.
  - Tidak menetapkan perubahan source/sink ekonomi.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-030 · Aturan gameplay cuaca Drizzle
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Drizzle perlu memiliki identitas gerimis lembut dan menenangkan, dengan efek tanaman yang terasa berbeda dari Cloudy tanpa menjadikan hujan ringan sebagai hukuman berat.
- Keputusan:
  - Drizzle memiliki suasana gerimis lembut, tenang, dan menenangkan.
  - Selama Drizzle, WaterLevel setiap tanaman yang terkena efek cuaca bertambah **0,05 per tick**.
  - Penambahan WaterLevel tidak boleh melampaui batas maksimum **5,00** yang ditetapkan D-018.
  - Setiap tick, setiap buah yang eligible melakukan roll Mutation **Wet (Basah)** secara independen dengan peluang **2,5% per buah per tick**.
  - Roll Wet satu buah tidak memengaruhi hasil roll buah lain. Aturan D-022 tetap berlaku: jenis Mutation yang sama hanya dapat tercatat satu kali pada buah yang sama.
  - Selama Drizzle, seluruh tanaman menerima tambahan waktu pertumbuhan **15%**, tanpa membedakan klasifikasi kebutuhan sinar matahari.
  - Drizzle tidak memberikan bonus atau percepatan pertumbuhan.
  - Drizzle tidak menimbulkan efek gameplay lain di luar aturan yang disebutkan, kecuali jika ditetapkan melalui keputusan baru.
  - Tick Drizzle mengikuti interval **30 detik** pada D-018. Durasi episode mengikuti aturan cuaca non-Sunny pada D-031.
  - Multiplier harga Mutation Wet, detail visual Wet, dan aturan penerapan modifier pada tanaman yang baru ditanam ketika Drizzle sedang berlangsung masih BELUM DIPUTUSKAN.
  - Aturan ini merupakan rancangan konsep dan tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Roll Mutation satu kali untuk seluruh tanaman; memberi bonus pertumbuhan pada Drizzle; atau membatasi modifier waktu tumbuh hanya pada tanaman dengan kebutuhan sinar matahari tinggi.
- Dampak:
  - Sistem cuaca perlu menjalankan roll Mutation secara independen untuk setiap buah eligible pada setiap tick Drizzle.
  - Sistem tanaman perlu membedakan WaterLevel dari modifier waktu pertumbuhan; penambahan air tidak otomatis mempercepat pertumbuhan.
  - Karena 2,5% berlaku pada setiap tick, peluang kumulatif dapat menjadi signifikan untuk buah yang eligible sepanjang episode penuh. Nilai ini perlu dievaluasi melalui balancing/playtest tanpa mengubah keputusan secara diam-diam.
  - Tidak ada perubahan source/sink ekonomi yang ditetapkan; Wet berpotensi memengaruhi harga jual setelah multipliernya diputuskan.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-028 · Konsep cuaca Spring: Sunny dan Cloudy
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk rancangan konsep; belum menjadi persetujuan scope implementasi
- Konteks: Musim Spring membutuhkan identitas atmosfer dan aturan awal cuaca yang konsisten dengan visi Cozy Garden Life Simulator. Cuaca juga menjadi salah satu sumber kondisi lingkungan untuk tanaman dan Mutation, tetapi tidak setiap cuaca harus menghasilkan Mutation.
- Keputusan:
  - Identitas visual Spring adalah **Fresh Nature**: dominasi hijau segar, kuning, dan warna bunga alami; suasana hidup, cerah, dan penuh energi.
  - Pola cuaca normal Spring adalah **Balanced**, dengan cuaca cerah dan hujan relatif seimbang. Distribusi peluang numerik belum ditetapkan.
  - Roster konsep Spring terdiri dari tujuh cuaca: **Sunny, Cloudy, Drizzle, Rainy, Windy, Misty, dan Thunderstorm**.
  - **Sunny** adalah cuaca awal ketika musim Spring dimulai, berperan sebagai cuaca dasar dan sering muncul kembali selama Spring. Sunny bersifat netral: tidak mengubah WaterLevel, waktu pertumbuhan, ukuran buah, atau status tanaman; Sunny tidak menghasilkan Mutation.
  - **Cloudy** berperan sebagai cuaca transisi yang dapat mendahului Drizzle, Rainy, atau Thunderstorm.
  - Saat satu episode Cloudy dimulai, WaterLevel setiap tanaman yang terkena efek cuaca bertambah **0,25 satu kali**. Tidak ada penambahan WaterLevel berkala selama episode Cloudy.
  - Tanaman dengan kebutuhan sinar matahari tinggi menerima tambahan waktu tumbuh **15%** selama Cloudy. Tanaman dengan kebutuhan sinar matahari rendah atau sedang tidak terkena modifier ini.
  - Jika Cloudy dimulai ketika tanaman yang memenuhi syarat sedang dalam proses tumbuh, **sisa waktu pertumbuhannya bertambah 15%**. Progres yang telah diperoleh tidak dihapus.
  - Cloudy tidak menghasilkan Mutation.
  - Durasi, peluang kemunculan, distribusi cuaca, nilai penurunan/penambahan selain yang disebut di atas, dan aturan transisi lengkap masih BELUM DIPUTUSKAN.
  - Roster dan aturan Spring ini merupakan hasil eksplorasi konsep; tidak otomatis memasukkan Seasons & Weather ke scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Mengharuskan semua cuaca menghasilkan Mutation; memberi efek pertumbuhan negatif kepada semua tanaman saat Cloudy; dan menambah WaterLevel secara berkala selama Cloudy.
- Dampak:
  - Concept Backlog dan GDD mencatat identitas Spring serta aturan awal Sunny dan Cloudy sebagai konsep terkonfirmasi.
  - Sistem data tanaman nantinya perlu memiliki klasifikasi kebutuhan sinar matahari agar modifier Cloudy dapat diterapkan secara selektif.
  - Sistem pertumbuhan perlu memperhitungkan modifier waktu pada tanaman yang sedang tumbuh ketika Cloudy dimulai.
  - Semua perubahan WaterLevel dan waktu pertumbuhan tetap harus dihitung server-authoritative jika kelak masuk implementasi.
  - Tidak ada perubahan source/sink ekonomi yang ditetapkan.
  - D-028 tidak menetapkan durasi musim, durasi cuaca, peluang kemunculan, Mutation Cloudy, atau scope rilis.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-029 · Menu informasi kondisi tanaman
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif untuk kebutuhan konseptual UI; detail belum ditetapkan
- Konteks: Pemain perlu dapat memeriksa kondisi tanaman dan memahami faktor yang sedang memengaruhi pertumbuhannya, termasuk efek musim dan cuaca.
- Keputusan:
  - Garden Life akan menyediakan **menu khusus informasi tanaman** yang dapat digunakan pemain untuk memeriksa kondisi tanaman.
  - Menu tersebut harus membantu pemain memahami kondisi tanaman yang dipilih. Informasi rinci yang ditampilkan, susunan panel, cara membuka, interaksi, dan perilaku pada PC/perangkat sentuh masih BELUM DIPUTUSKAN.
  - Informasi efek cuaca yang relevan, termasuk modifier waktu tumbuh Cloudy, perlu dapat dijelaskan kepada pemain melalui UI informasi tanaman ketika efek tersebut berlaku.
  - Contoh field seperti tahap pertumbuhan, progres, sisa waktu, WaterLevel, dan status kondisi masih merupakan kandidat rancangan, bukan daftar final yang disetujui.
  - Keputusan ini menetapkan kebutuhan konseptual UI dan tidak otomatis menetapkan scope First Release atau Vertical Slice.
- Alternatif yang ditolak: Mengharuskan pemain menebak kondisi tanaman hanya dari tampilan visual tanpa akses ke informasi kondisi.
- Dampak:
  - GDD dan Concept Backlog mencatat kebutuhan menu informasi tanaman.
  - Detail UI, field, interaksi, aksesibilitas, dan prioritas implementasi perlu dirancang dalam pembahasan/spec terpisah.
  - Tidak ada perubahan pada ekonomi, pertumbuhan, atau aturan tanaman selain kebutuhan penyampaian informasi yang sudah ditetapkan.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-027 · Prompt Inventory tetap tersedia sampai dibuka
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Pemain perlu mendapat arahan untuk menemukan Starter Kit tanpa harus menghentikan eksplorasi kebun atau terus-menerus dikejar oleh UI.
- Keputusan:
  - Setelah pesan sambutan D-026 selesai dan menghilang, tampilkan penanda visual pada tombol Inventory beserta prompt: **"Perlengkapan kebunmu sudah tersedia. Buka Inventory untuk melihatnya!"**
  - Penanda visual dan prompt tetap tersedia secara halus sampai pemain membuka Inventory.
  - Jika pemain memilih menjelajahi plot dan belum membuka Inventory, prompt tetap tersedia; sistem tidak memaksa pemain kembali ke tombol atau menghentikan eksplorasi.
  - Penanda visual berada pada tombol Inventory, bukan mengikuti posisi karakter atau kamera.
  - Gunakan satu penekanan visual awal yang halus. Jangan mengulang pulse terus-menerus atau menggunakan kedipan cepat.
  - Saat pemain membuka Inventory, prompt dan penanda visual onboarding ini langsung dihilangkan.
  - Jika pemain membuka Inventory sebelum pesan sambutan 3 detik selesai, prompt Inventory tidak perlu ditampilkan setelah pesan sambutan menghilang.
  - Inventory tetap dibuka atas tindakan pemain sendiri; tidak pernah terbuka otomatis.
- Alternatif yang ditolak: Menghilangkan prompt setelah jeda singkat meskipun belum dibuka; membuat prompt mengikuti karakter; mengulang animasi pulse tanpa henti; atau memaksa pemain membuka Inventory.
- Dampak:
  - D-027 melengkapi urutan Arrival & First Impression D-026 dan onboarding Inventory D-025; tidak menggantikan keduanya.
  - PLAYER_JOURNEY.md dan GDD diperbarui untuk menjelaskan perilaku prompt yang persisten tetapi tidak memaksa.
  - Tidak mengubah isi Starter Kit, inventori, source/sink ekonomi, atau aturan gameplay.
  - Tidak menetapkan pemulihan onboarding lintas disconnect/sesi; hal tersebut tetap perlu dirinci dalam spec onboarding.
  - Tidak ada spec yang dinaikkan menjadi READY.

### D-026 · Arrival & First Impression pemain baru
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Kedatangan pertama pemain perlu terasa langsung dan ramah, tanpa mengambil alih kontrol atau menambah karakter pemandu yang memperpanjang onboarding.
- Keputusan:
  - Pemain muncul langsung di plot pribadinya dan dapat menggerakkan karakter sejak awal.
  - Kamera menggunakan kondisi normal; tidak ada cinematic, camera lock, atau urutan kamera khusus.
  - Tidak ada NPC pemandu pada momen kedatangan pertama.
  - Saat tiba, tampilkan pesan sambutan singkat: **"Selamat datang di kebunmu! Tempat kecil untuk menciptakan kebun impianmu."**
  - Pesan sambutan tampil selama **3 detik**, lalu menghilang otomatis.
  - Pesan tidak memblokir pergerakan, kamera, atau interaksi pemain. Tidak ada tombol konfirmasi dan pemain tidak perlu menunggu pesan selesai untuk bergerak.
  - Setelah pesan sambutan menghilang, lanjutkan arahan penanda visual dan prompt Inventory sesuai D-025.
  - Pesan sambutan hanya ditampilkan pada kunjungan pertama pemain ke plot pribadinya.
- Alternatif yang ditolak: Cinematic/camera lock saat spawn, NPC pemandu yang menyapa pemain, dan dialog sambutan yang mewajibkan konfirmasi.
- Dampak:
  - PLAYER_JOURNEY.md bagian First Visit diperbarui untuk memasukkan momen kedatangan dan durasi pesan.
  - GDD merangkum pendekatan Arrival & First Impression dan merujuk D-026.
  - Tidak ada perubahan pada Starter Kit, inventori, source/sink ekonomi, atau aturan gameplay.
  - D-026 melengkapi urutan onboarding D-025 dan tidak menggantikannya.
  - D-026 tidak menyetujui scope implementasi di luar pengalaman kedatangan yang dijelaskan dan tidak menaikkan spec apa pun menjadi READY.

### D-025 · Onboarding First Visit dan pengenalan Starter Kit
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Pemain baru perlu memahami bahwa plot awal memang kosong, sementara Starter Kit tersedia di Inventory. Pengenalan harus memberi arah tanpa mengambil kendali pemain atau menjadikan farming sebagai kewajiban.
- Keputusan:
  - Onboarding First Visit menggunakan pendekatan kontekstual dan bertahap, bukan tutorial panjang yang mengunci urutan tindakan pemain.
  - Setelah pemain mengenali plot, UI memberi penanda visual pada tombol Inventory beserta prompt singkat yang menjelaskan bahwa perlengkapan kebun tersedia di sana.
  - Inventory tidak dibuka otomatis. Pemain harus menekan tombol Inventory sendiri.
  - Saat Inventory pertama kali dibuka, ketiga kelompok Starter Kit langsung terlihat: **Tools**, **Farming**, dan **Decorations**.
  - Kelompok diperkenalkan secara bertahap dengan urutan Tools -> Farming -> Decorations melalui highlight dan tooltip/prompt kontekstual.
  - Isi kelompok:
    | Kelompok | Item Starter Kit |
    |---|---|
    | Tools | Shovel, Trowel, Watering Can, Pupuk |
    | Farming | Farm Tile, Benih Wortel |
    | Decorations | Kursi Kayu, Lampu Taman |
  - Pengenalan kelompok tidak mengunci navigasi Inventory. Pemain bebas memilih kelompok lain, melihat item, atau menjelajahi Inventory selama pengenalan berlangsung.
  - Pemain dapat melewati penjelasan kelompok. Detail kontrol dan tampilan final tetap harus dijabarkan dalam dokumen desain/spec UI.
  - Inventory tidak ditutup otomatis. Pemain menutup panel sendiri.
  - Setelah Inventory ditutup, onboarding memperkenalkan pilihan aktivitas awal: **Mulai Bertani** atau **Mulai Mendekorasi**.
  - Kedua pilihan merupakan jalur yang valid. Farming boleh ditonjolkan sebagai jalur rekomendasi, tetapi tidak wajib dan tidak boleh menghalangi pemain memilih dekorasi.
  - Jalur bertani mengarahkan pemain untuk menempatkan Farm Tile, memilih Benih Wortel, lalu menanam. Jalur dekorasi mengarahkan pemain untuk menempatkan Kursi Kayu atau Lampu Taman.
  - Onboarding awal berakhir setelah pemain berhasil melakukan satu tindakan kreatif pada jalur yang dipilih. Setelah itu pemain bebas mengeksplorasi game.
  - Keputusan ini tidak menetapkan waktu tumbuh, hasil panen, harga jual, reward, maupun aturan ekonomi tanaman yang belum memiliki keputusan/spec.
- Alternatif yang ditolak: Membuka Inventory secara otomatis; menyembunyikan kelompok item sampai tutorial selesai; mengunci pemain pada urutan tutorial; atau mewajibkan farming sebelum pemain boleh mendekorasi.
- Dampak:
  - PLAYER_JOURNEY.md bagian First Visit menjadi acuan alur onboarding dan tetap berstatus DRAFT sampai keseluruhan rancangan ditinjau.
  - GDD merangkum prinsip onboarding dan merujuk D-025.
  - UI Inventory perlu mendukung kategori yang langsung terlihat, highlight kontekstual, tooltip/prompt, serta navigasi bebas.
  - Onboarding tidak menambah atau mengurangi item Starter Kit dan tidak menciptakan source/sink ekonomi baru.
  - Metrik evaluasi kandidat: pemain berhasil membuka Inventory sendiri, memahami keberadaan Starter Kit, dan melakukan tindakan kreatif pertama; target numerik menunggu playtest.
  - D-025 tidak menyetujui scope implementasi First Release di luar onboarding yang dirancang dan tidak menaikkan spec apa pun menjadi READY.

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

### D-024 · Struktur empat tahap Player Journey
- Tanggal: 2026-11-15
- Diputuskan oleh: Pemilik proyek
- Status: Aktif
- Konteks: Garden Life membutuhkan kerangka perjalanan pemain dari pertama kali masuk hingga kebun berkembang agar desain onboarding, core loop, progres, dan fitur jangka panjang memiliki urutan pengalaman yang jelas.
- Keputusan:
  - Player Journey Garden Life dibagi menjadi empat tahap pengalaman:
    1. **First Visit:** pemain mengenal dunia, plot, inventori awal, dan cara memulai.
    2. **Early Garden:** pemain mulai membentuk kebun melalui dekorasi, penanaman, dan perawatan dasar.
    3. **Growing Garden:** pemain memperluas kebun melalui koleksi, variasi, progres, dan interaksi sosial.
    4. **Established Garden:** pemain memiliki kebun dengan identitas personal dan aktivitas berkelanjutan, termasuk aktivitas sosial yang lebih luas.
  - Keempat tahap adalah kerangka pengalaman, bukan level, ranking, atau gerbang waktu. Pemain dapat bergerak dengan kecepatan berbeda dan memilih aktivitasnya.
  - Tahap Established Garden bukan kondisi tamat; tahap tersebut merupakan keadaan berkelanjutan untuk menata, menikmati, berbagi, menemukan inspirasi, dan mengembangkan kebun kembali.
  - Struktur empat tahap menjadi dasar penyusunan Player Journey dan pembahasan scope berikutnya.
  - Persetujuan struktur tidak otomatis menyetujui seluruh fitur yang disebut dalam tahap sebagai scope First Release atau fitur implementasi.
- Alternatif yang ditolak: Menjadikan tahap sebagai level atau milestone waktu yang kaku, karena dapat menciptakan tekanan progres yang tidak sesuai dengan visi cozy.
- Dampak:
  - Dokumen PLAYER_JOURNEY.md menjadi acuan pengalaman dari onboarding hingga jangka panjang.
  - GDD dan Roadmap perlu menautkan Player Journey sebagai artefak Fase 1.
  - Target waktu, level, metrik, dan scope tiap tahap tetap perlu dianalisis dan disetujui terpisah.

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
