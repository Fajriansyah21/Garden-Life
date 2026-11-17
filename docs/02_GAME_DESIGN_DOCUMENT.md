# 02 · Game Design Document (GDD)

**Pemilik:** ChatGPT (Perancang) · **Penyetuju:** Pemilik proyek
**Versi:** 3.3 · **Terakhir diubah:** 2026-11-17

> Dokumen ini mencatat arah desain yang telah dikonfirmasi. Detail yang belum diputuskan ditandai **BELUM DIPUTUSKAN** atau **ASUMSI** dan tidak boleh dianggap sebagai aturan implementasi.

## 1. Visi

- **Nama game / map:** Garden Life.
- **Identitas visi jangka panjang (D-023):** Cozy Garden Life Simulator.
- **Pitch:** Garden Life adalah game Roblox santai tentang membangun, merawat, dan mendekorasi kebun pribadi yang terus berkembang bersama teman. Pemain mengekspresikan gaya kebunnya, mengoleksi tanaman unik, merawat kebun, dan mengunjungi kebun pemain lain. Farming serta manajemen dan ekonomi ringan menjadi aktivitas pendukung, bukan satu-satunya tujuan.
- **Genre / pengalaman:** Cozy garden building, decorating, light farming, dan social co-op.
- **Pengalaman utama:** Kreativitas, relaksasi, rasa memiliki terhadap kebun sebagai ruang personal, koleksi, interaksi sosial, dan kepuasan melihat kebun berkembang sesuai gaya pemain.
- **Prioritas desain:** Dekorasi dan ekspresi personal > pengalaman sosial/co-op > koleksi dan perawatan kebun > farming santai > manajemen dan ekonomi ringan.
- **Arah scope:** Visi mencakup pengembangan jangka panjang, tetapi fitur dibagi ke First Release, Post-Release, dan Long-Term Vision. Persetujuan visi tidak otomatis menyetujui seluruh fitur sebagai scope rilis.
- **Game referensi (3):** **BELUM DIPUTUSKAN**. Jangan menetapkan referensi tanpa persetujuan pemilik.
- **Player Journey (D-024):** empat tahap pengalaman, yaitu First Visit, Early Garden, Growing Garden, dan Established Garden. Tahap ini bukan level atau gerbang waktu. Rincian pengalaman DRAFT berada di [PLAYER_JOURNEY.md](design/PLAYER_JOURNEY.md).

## 2. Target pemain

- **Target pengalaman:** Pemain yang ingin bermain santai, menata kebun, mengoleksi dekorasi, dan sesekali mengurus tanaman atau ekonomi.
- **Perangkat:** Roblox; UI wajib nyaman untuk PC dan perangkat sentuh.
- **Mode:** Solo maupun multiplayer/co-op dalam plot yang sama.
- **Panjang sesi:** **BELUM DIPUTUSKAN**. Core experience harus tetap menyenangkan dalam sesi singkat dan tidak menghukum pemain yang pergi.

## 3. Core loop

Loop konseptual utama:

1. Masuk ke kebun pribadi atau kebun bersama.
2. Mengenali plot kosong dan mulai membentuk kebun dengan objek yang tersedia.
3. Menata area dan menempatkan Farm/Build Tiles serta dekorasi.
4. Menanam dan merawat tanaman sebagai aktivitas santai.
5. Memanen atau memperoleh hasil aktivitas kebun.
6. Menjual hasil bila sistem jual telah ditetapkan untuk memperoleh Life Coin.
7. Menggunakan Life Coin untuk membuka ruang, membeli tile, tanaman, atau dekorasi.
8. Kembali menata kebun sesuai kreativitas pemain.

**Kondisi awal plot (D-008):** Saat pertama kali dimasuki, plot tidak memiliki dekorasi, bangunan, atau tanaman yang sudah ditempatkan.

**Starter Kit (D-009 dan D-010):** Pemain baru menerima Starter Kit gratis sebagai item inventori dan item tidak otomatis ditempatkan di plot. Komposisi kit telah ditetapkan: 1 Shovel permanen, 10 Watering Can, 1 Pupuk, 2 Farm Tile, 1 Trowel permanen, 10 Benih Wortel, 1 Kursi Kayu, dan 1 Lampu Taman. Shovel menghapus tanaman; Trowel memindahkan tanaman. Detail kapasitas/refill Watering Can, efek/penggunaan Pupuk, waktu pemberian, serta aturan pemberian ulang masih BELUM DIPUTUSKAN.

**Arrival & First Impression (D-026, D-027):** Pemain muncul langsung di plot dengan kontrol karakter dan kamera normal yang langsung aktif. Tidak ada cinematic, camera lock, atau NPC pemandu. Pesan sambutan “Selamat datang di kebunmu! Tempat kecil untuk menciptakan kebun impianmu.” tampil selama 3 detik tanpa memblokir kontrol, lalu menghilang otomatis. Setelah itu, penanda visual dan prompt Inventory tetap tersedia secara halus sampai pemain membuka Inventory. Penanda tidak mengikuti karakter dan tidak mengulang pulse terus-menerus. Jika Inventory dibuka sebelum pesan sambutan selesai, prompt tidak perlu muncul.

**Onboarding First Visit (D-025, D-032):** Pemain membuka Inventory sendiri melalui penanda visual dan prompt. Ketika terbuka, kelompok Tools, Farming, dan Decorations langsung terlihat; pengenalan dilakukan bertahap dengan highlight/tooltip tanpa mengunci navigasi. Pemain dapat melewati penjelasan dan menutup Inventory sendiri. Setelah itu panel pilihan aktivitas menawarkan Mulai Bertani, Mulai Mendekorasi, atau Skip Tutorial. Panel tidak muncul kembali secara otomatis setelah pilihan dibuat. Jika pemain memilih Skip Tutorial, onboarding langsung dianggap selesai/dilewati tanpa panduan jalur aktivitas, tetapi seluruh fitur gameplay tetap dapat digunakan normal. Jika memilih salah satu jalur, onboarding berakhir setelah satu tindakan kreatif berhasil. Pemain dapat memulai ulang tutorial secara manual melalui Pengaturan; tutorial dimulai dari pengenalan Inventory dan tidak mengulang pesan sambutan D-026 atau mereset progres gameplay. Detail alur dan pertanyaan terbuka dicatat di [PLAYER_JOURNEY.md](design/PLAYER_JOURNEY.md).

Loop di atas adalah rancangan konseptual; detail transaksi dan pertumbuhan tetap memerlukan spec.


### Musim & cuaca: eksplorasi Spring (D-028, D-030, D-031, D-034, D-035)
- Identitas visual Spring adalah **Fresh Nature** dengan pola cuaca **Balanced**. Roster konsepnya: Sunny, Cloudy, Drizzle, Rainy, Windy, Misty, dan Thunderstorm.
- **Sunny** menjadi cuaca awal Spring dan cuaca dasar yang sering muncul. Efek gameplay dan Mutation: tidak ada. Durasi Sunny belum ditetapkan.
- **Cloudy** dapat menjadi transisi menuju Drizzle, Rainy, atau Thunderstorm. Saat episode dimulai, WaterLevel tanaman yang terkena efek bertambah 0,25 satu kali.
- Selama Cloudy, tanaman dengan kebutuhan sinar matahari tinggi membutuhkan waktu tumbuh 15% lebih lama. Jika tanaman tersebut sedang tumbuh saat Cloudy dimulai, sisa waktu tumbuhnya juga bertambah 15%; progres yang sudah diperoleh tidak dihapus. Cloudy tidak menghasilkan Mutation.
- **Drizzle** adalah gerimis lembut dan menenangkan. Selama episode berlangsung, WaterLevel tanaman yang terkena efek bertambah 0,05 setiap tick. Setiap tick, setiap buah eligible melakukan roll Mutation Wet (Basah) secara independen dengan peluang 2,5%. Seluruh tanaman menerima tambahan waktu pertumbuhan 15%; Drizzle tidak memberikan bonus atau percepatan pertumbuhan. WaterLevel tetap dibatasi maksimum 5,00 sesuai D-018.
- **Rainy** memiliki hujan sedang hingga deras, tetapi tetap tenang, sejuk, dan sedikit sendu. WaterLevel tanaman yang terkena efek bertambah 0,075 setiap tick. Setiap buah eligible memiliki peluang 5% per tick untuk memperoleh Mutation Wet; buah yang sudah memiliki Wet memiliki peluang 2,5% per tick untuk berevolusi menjadi Flooded. Evolusi berhasil menggantikan Wet, sehingga Wet tidak lagi tercatat dan multiplier Wet tidak lagi berlaku. Seluruh tanaman menerima tambahan waktu pertumbuhan 20%; Rainy tidak memberikan bonus atau percepatan pertumbuhan (D-034).
- Mutation Flooded dari evolusi Wet selama Rainy adalah Mutation yang sama dengan Flooded dari WaterLevel tinggi. Pada WaterLevel 4,00-4,99, peluang Flooded adalah 2,5% per interval paparan 2 menit; pada WaterLevel 5,00, peluangnya 2,5% per interval 1 menit. Satu buah hanya dapat memperoleh Flooded satu kali dari salah satu jalur tersebut (D-035). D-019 dan D-020 tetap menjadi riwayat, bukan nilai peluang aktif.
- **Windy** adalah angin sepoi-sepoi. Selama episode berlangsung, WaterLevel tanaman yang terkena efek berkurang 0,005 setiap 2 tick (60 detik), dengan batas minimum 0,000. Kecepatan seluruh proses pertumbuhan tanaman dan pertumbuhan buah menjadi 1,5x dari kecepatan normal 1,0x. Bonus berlaku untuk semua tanaman tanpa pengecualian klasifikasi sinar matahari. Windy tidak menghasilkan Mutation (D-036).
- **Misty** menerapkan kenaikan WaterLevel +0,25 satu kali pada awal episode, mengikuti Cloudy. Seluruh tanaman menerima tambahan waktu pertumbuhan 15%, mengikuti Drizzle, tanpa bonus atau percepatan pertumbuhan. Setiap buah yang belum memiliki Misty melakukan roll Mutation Misty 6,697% per tick; peluang kumulatifnya sekitar 75% setelah 20 roll independen. Buah yang sudah memiliki Misty melakukan roll evolusi menuju Foggy sebesar 0,809% per tick. Peluang tersebut setara sekitar 15% setelah 20 roll evolusi eligible. Karena roll Foggy baru dimulai setelah Misty diperoleh, jumlah roll aktual dapat kurang dari 20. Jika evolusi berhasil, Foggy menggantikan Misty dan Misty tidak lagi tercatat pada buah (D-037).
- **Thunderstorm** adalah cuaca berisiko tinggi dengan sambaran petir yang jarang terjadi. Setiap plot melakukan roll sambaran **1% per tick** selama 20 tick / 10 menit; maksimal 5 kejadian per plot per episode. Titik sambaran acak di dalam plot memiliki area dampak lingkaran radius **8 studs**. Tanaman dalam area dampak terkena Mutation Shocked pada seluruh buahnya (100%) dan setiap buah melakukan roll Charged 15%. Hasil kondisi tanaman setelah tersambar bersifat saling eksklusif: 60% tidak rusak, 25% gosong, atau 15% mati. Tanaman gosong masih dapat dirawat tetapi menerima penalti yang belum dirinci; tanaman mati dapat dibuang, diolah menjadi pupuk, atau di-revive dengan Robux (detail belum ditetapkan).
- Selama Thunderstorm, WaterLevel bertambah **0,075 per tick** dan seluruh tanaman menerima tambahan waktu pertumbuhan **20%**, sama seperti Rainy. Thunderstorm tidak mempercepat pertumbuhan.
- **Scorched (D-039, D-040):** Tanaman gosong ditampilkan berwarna hitam seperti hangus terbakar. Selama status Scorched aktif, jumlah buah setiap panen menjadi 50% dari hasil normal dan dibulatkan ke bawah (`floor(jumlah_buah_normal × 0,5)`). Tanaman yang normalnya menghasilkan 1 buah menghasilkan 0 buah saat Scorched. Status ini tidak memiliki batas waktu dan tidak pulih otomatis. Satu item Vitamin memulihkan satu tanaman Scorched; Vitamin hanya menghapus status Scorched tanpa mengubah atau mereset umur, ukuran, maupun progres pertumbuhan tanaman. Setelah pulih, tanaman kembali menghasilkan buah dalam jumlah normal. Cara memperoleh Vitamin, harga, batas stack inventori, dan detail UI masih BELUM DIPUTUSKAN.
- **Lightning Rod** memiliki area lingkaran radius **24 studs** dan peluang 50% untuk mengalihkan sambaran yang jatuh di dalam area. Satu rod menahan maksimal 3 sambaran yang berhasil dialihkan. **Thunderstorm Relief** memiliki area lingkaran radius **20 studs** dan mengurangi peluang gosong serta mati masing-masing 5 poin persentase per stack aktif. Maksimal 3 stack; durabilitas setiap item 3 sambaran yang dilindungi secara independen. Setiap sambaran mengurangi durabilitas semua Relief yang area lingkarannya mencakup titik sambaran sebesar 1; jika sambaran berada dalam dua area, kedua item kehilangan 1 durabilitas. Item yang tidak mencakup titik sambaran tidak berkurang. Pengurangan risiko dihitung dari jumlah Relief aktif yang melindungi tanaman (D-038).
- WaterLevel disimpan dengan presisi internal 0,001 (integer 0-5000), sedangkan UI menampilkan 2 angka desimal. Penambahan Rainy +0,075 tidak dibulatkan per tick; 20 tick menghasilkan total +1,500 sebelum clamp maksimum 5,000 (D-033).
- Setiap cuaca selain Sunny berlangsung selama 20 tick (600 detik/10 menit). Satu tick berdurasi 30 detik. Sunny dikecualikan dan durasinya masih BELUM DIPUTUSKAN (D-031).
- Multiplier harga dan tampilan Mutation Wet/Flooded/Misty/Foggy, urutan roll Wet dan evolusi Wet→Flooded dalam tick yang sama, serta penerapan modifier cuaca pada tanaman yang baru ditanam ketika episode sedang berjalan masih BELUM DIPUTUSKAN.
- Peluang kemunculan dan distribusi cuaca, aturan transisi lengkap, serta detail Thunderstorm masih BELUM DIPUTUSKAN.
- Seasons & Weather tetap berstatus eksplorasi dan tidak otomatis menjadi scope First Release atau Vertical Slice.


### Eksplorasi Summer: Golden Summer, Countryside Summer, dan Fresh Summer (D-041, D-042, D-043, D-044)
- Identitas visual dan suasana Summer menggunakan konsep **Golden Summer**: cerah dan hangat.
- Arah lingkungan Summer adalah **Countryside Summer**: lanskap pedesaan musim panas dengan hamparan rumput, padang bunga, kebun buah, pagar kayu, dan suasana lanskap yang disinari matahari hangat.
- Palet warna utama menggunakan **Fresh Summer**: hijau segar, biru langit, kuning cerah, dan putih, dengan aksen emas dari Golden Summer.
- Palet Fresh Summer menjaga lanskap Countryside Summer tetap terasa hijau, subur, cerah, dan hidup, bukan kering atau didominasi warna cokelat.
- Pembagian warna per elemen (D-044):
  - Rumput dan padang: variasi hijau segar, hijau muda, dan hijau tua.
  - Langit: biru cerah; awan: putih.
  - Bunga dan padang bunga: kuning cerah, putih, dan krem dengan variasi alami.
  - Kebun buah: dedaunan hijau dan warna buah cerah sesuai jenis buah.
  - Pagar dan properti kayu: cokelat muda, beige, dan krem; bukan kayu gelap/lapuk sebagai karakter dominan.
  - Jalan setapak: beige dan warna tanah hangat sebagai warna netral pendamping.
  - Aksen emas digunakan terbatas pada pantulan cahaya dan detail atmosfer; bukan warna dominan lingkungan.
- Golden Summer menetapkan karakter cahaya dan suasana; Countryside Summer menetapkan arah lanskap; Fresh Summer menetapkan arah palet; D-044 menetapkan pembagian warna konseptual per elemen.
- Kode warna, proporsi warna, pencahayaan spesifik, jenis bunga/pohon/vegetasi, aset lingkungan, dan tata letak masih BELUM DIPUTUSKAN.
- **Tornado Summer (D-045):** Penghitung Tornado berlaku untuk satu server, dengan batas minimal 1 dan maksimal 5 Tornado per musim Summer. Tornado baru eligible mulai progres musim 50%. Sistem memeriksa peluang pada progres 50%, 60%, 70%, 80%, dan 85%; empat kesempatan pertama masing-masing memiliki peluang 10% untuk memulai rantai. Pada kesempatan kelima, peluang tetap 10% jika server sudah mengalami setidaknya satu Tornado. Jika belum ada Tornado sama sekali, rantai dijamin dimulai. Rantai harus berurutan Heatwave → Summer Shower → Muggy → Tornado. Jika cuaca lain menyela sebelum Muggy selesai pada kesempatan biasa, rantai dibatalkan dan kesempatan tidak dikembalikan. Jika kesempatan kelima menjadi jaminan minimum, rangkaian pemicu dilindungi dari interupsi cuaca lain. Satu rantai hanya menghasilkan satu Tornado; setelah Tornado kelima dimulai, pemicu dinonaktifkan sampai Summer berikutnya. Penghitung direset pada awal Summer baru.
- Roster lengkap, distribusi cuaca selain peluang pemicu Tornado, durasi Summer dan cuaca, serta efek gameplay Summer masih BELUM DIPUTUSKAN.
- Dampak Summer terhadap WaterLevel, pertumbuhan, buah, Mutation, kondisi tanaman, dan ekonomi masih BELUM DIPUTUSKAN.
- Seasons & Weather tetap berstatus eksplorasi dan tidak otomatis menjadi scope First Release atau Vertical Slice.

### Tools & perawatan tanaman

Tools yang telah dirancang dicatat dalam [FEAT-002 Tools & Perawatan Tanaman](design/FEAT-002_tools_perawatan_tanaman.md), status DRAFT. Aturan yang telah dikonfirmasi:
- Shovel dan Trowel adalah alat permanen. Shovel menghapus tanaman; Trowel memindahkan tanaman tanpa mereset progres pertumbuhannya.
- Watering Can adalah consumable. Satu penggunaan menyiram semua tanaman di dalam area berbentuk lingkaran.
- Efek penyiraman dapat bertambah melalui penggunaan berulang, tetapi dibatasi oleh nilai maksimum (D-011).
- Setiap tanaman memiliki toleransi air. Kadar air yang melampaui toleransi menyebabkan status Overwatered, tetapi tanaman masih dapat pulih jika kadar air kembali ke batas aman sebelum durasi kematian tercapai (D-012, D-013). Kadar air dan bonus pertumbuhan adalah dua nilai terpisah.
- Soil Aerator adalah consumable dengan area lingkaran yang mempercepat pengeringan kadar air secara bertahap. Satu aktivasi membentuk zona selama 2,5 menit (150 detik); setiap tick 30 detik mengurangi WaterLevel sebesar 0,50 pada tanaman di dalam radius. WaterLevel memakai rentang 0,00-5,00 dengan presisi internal 0,001 (integer 0-5000), sementara UI menampilkan 2 angka desimal; level 4 = Tanah terlalu basah dan level 5 = Tanah kebanjiran (D-018, D-033). Watering Can menambah 0,50 per penggunaan; Sprinkler menambah 0,15 per tick selama 10 menit. Tanaman yang berada pada WaterLevel >=4,00 selama 15 menit terus-menerus mati; Billboard Alert muncul di atas tanaman.
- Sprinkler adalah perangkat consumable yang ditempatkan pada plot. Area jangkauannya berbentuk lingkaran; selama durasi aktif, perangkat menyiram otomatis, mempercepat pertumbuhan, dan meningkatkan ukuran buah. Setelah durasi berakhir, perangkat dikonsumsi dan menghilang.
- Seed Extractor mengorbankan satu tanaman untuk menghasilkan benih.
- Harvest Basket menghabiskan satu penggunaan untuk mengambil seluruh buah siap panen pada satu tanaman. Panen manual satu per satu tetap tersedia.
- Plant Sprayer adalah alat permanen; cairan aplikasinya consumable dan digunakan pada satu tanaman untuk efek khusus seperti mutasi, ukuran, atau variasi.
- **Variant dan Mutation buah (D-022):** keduanya merupakan sistem terpisah, sama-sama mengubah tampilan dan meningkatkan harga jual, serta dapat dimiliki bersamaan pada satu buah. Satu buah hanya dapat memiliki satu Variant; Variant permanen, tidak dapat diganti/ditimpa, dan tampilan Variant selalu berada di atas tampilan Mutation. Variant Seasonal meningkatkan Rarity dan sangat langka serta memerlukan kondisi khusus. Nama Variant Winter diubah menjadi Cristal. Multiplier Variant: Seasonal/Cristal 5x, Silver 1,5x, Gold 3x, Rainbow 4x.
- Mutation dapat dimiliki dalam beberapa jenis pada satu buah. Jenis Mutation yang sama hanya dapat tercatat satu kali per buah. Mutation baru dapat menimpa tampilan Mutation sebelumnya, tetapi Mutation sebelumnya tetap tersimpan sebagai atribut dan multiplier ekonominya tetap aktif. Mutation dapat diperoleh dari cuaca, musim, metode khusus, atau Plant Sprayer. Multiplier masing-masing Mutation belum ditentukan dan akan dibahas satu per satu.
- **Rumus harga buah (D-022):** Harga Dasar × Multiplier Variant × Jumlah Multiplier Mutation. Multiplier Mutation dijumlahkan terlebih dahulu. Contoh ilustratif: 100 C × 5 × (2 + 5) = 3.500 C. Jika tidak memiliki Variant atau Mutation, faktor terkait menggunakan nilai netral 1x. Angka 2x dan 5x hanya contoh, bukan nilai Mutation yang disetujui.
- Mutation Flooded dari paparan WaterLevel dihitung independen per buah: peluang 2,5% per 2 menit pada WaterLevel 4,00-4,99 dan 2,5% per 1 menit pada WaterLevel 5,00. Satu buah hanya dapat memperoleh Flooded satu kali sepanjang siklus hidupnya, termasuk jika diperoleh melalui evolusi Wet selama Rainy (D-021, D-034, D-035).
- Pupuk dari Starter Kit direncanakan mempercepat pertumbuhan, tetapi aturan penggunaan dan efek numeriknya belum diputuskan.

Radius area, batas maksimum bonus pertumbuhan, rentang air ideal tiap tanaman, laju pengeringan alami saat cuaca panas/Summer, radius Soil Aerator dan Sprinkler, bonus ukuran buah, aturan akumulasi sisa paparan mutasi saat level air berubah, hasil Seed Extractor, dan efek cairan Plant Sprayer masih BELUM DIPUTUSKAN. Detail tersebut tidak boleh ditebak saat implementasi.
**Catatan:** Langkah jual, detail pertumbuhan tanaman, dan daftar sumber/penguras uang masih perlu dirancang. Jangan mengimplementasikan detail yang belum memiliki spec.

Pengalaman 5 menit pertama harus mengutamakan pemain bisa memahami plot, menempatkan atau memperoleh objek kebun, dan mulai mengekspresikan gaya kebunnya. Target waktu numerik **BELUM DIPUTUSKAN**.

## 4. Sistem utama

| Sistem | Ringkasan | Prioritas (M/S/C/W) | Spec |
|---|---|---|---|
| Plot & kepemilikan | 4 plot persisten per server; kepemilikan Original Owner dan Active Owner dibedakan | M | Belum dibuat |
| Kolaborasi plot | Pemilik mengundang pemain; kapasitas awal 2 dan dapat ditingkatkan menjadi 3 pemain | M | Belum dibuat |
| Dekorasi & pembangunan | Farm/Build Tiles memakai grid 5×5; dekorasi, bangunan, dan tanaman memakai free placement dengan opsi Snap to Grid | M | Belum dibuat |
| Ekspansi plot | Plot berkembang melalui 4 stage ukuran yang telah ditetapkan | M | Belum dibuat |
| Tanaman & farming | Aktivitas menanam, merawat, dan memanen secara santai | S | Belum dibuat |
| Tools & perawatan tanaman | Watering Can, Sprinkler, Soil Aerator, Shovel, Trowel, Seed Extractor, Harvest Basket, Plant Sprayer, dan Pupuk | S | FEAT-002 (DRAFT) |
| Panen & penjualan | Hasil kebun berpotensi menjadi sumber Life Coin | S | Belum dibuat |
| Inventori & gudang | Inventori pribadi dan konsep gudang bersama pernah dibahas; aturan final belum ditetapkan | S | Belum dibuat |
| Shared Savings / Bank | Tabungan milik plot untuk pembelian bersama, dengan kontrol pengeluaran | S | Belum dibuat |
| Toko | Pembelian tile, tanaman, dan dekorasi | S | Belum dibuat |
| Greenhouse | Konsep greenhouse dengan kapasitas 18 tanaman pernah dibahas | C | Belum dibuat |
| Pupuk | Starter Kit memberi 1 Pupuk; efek numerik dan aturan penggunaan belum ditetapkan. Konsep 5 tier belum disetujui | S | Belum dibuat |
| Musim & cuaca | 4 musim dan efek cuaca pernah dibahas; dampak gameplay belum ditetapkan | C | Belum dibuat |
| Progres & upgrade | Upgrade kapasitas, stage plot, dan akses fitur | S | Belum dibuat |
| Sosial | Kunjungan dan kerja sama di kebun | S | Belum dibuat |

Prioritas di atas adalah rekomendasi awal untuk konsep, bukan persetujuan scope implementasi. Vertical Slice perlu ditetapkan setelah detail core loop disepakati.

## 5. Ekonomi

- **Mata uang utama:** Life Coin.
- **Identitas visual:** Koin emas dengan ikon daun.
- **Saldo awal pribadi:** 1.000 Life Coin.
- **Nama tampilan mata uang:** Life Coin, divisualisasikan sebagai koin emas dengan ikon daun.
- **Shared Savings:** saldo terpisah yang dimiliki plot, bukan saldo pribadi anggota.
- **Biaya akses anggota baru ke Shared Savings:** 5.000 Life Coin sebagai biaya administrasi; Original Owner harus menyetujui akses anggota baru.
- **Source potensial:** penjualan hasil kebun. Nilai dan mekanisme penjualan **BELUM DIPUTUSKAN**.
- **Sink potensial:** pembelian Farm/Build Tiles, dekorasi, tanaman, ekspansi, dan upgrade. Harga **BELUM DIPUTUSKAN**.
- **Biaya pembuatan rekening/bank:** **BELUM DIPUTUSKAN**. Jangan menyamakan biaya ini dengan biaya akses anggota baru.
- **Spending Limit:** batas pengeluaran mingguan dari Shared Savings berlaku untuk seluruh pembelian yang memakai saldo bersama. Original Owner dapat mengubah batas atau menghapusnya (Unlimited).
- Semua harga, pendapatan, dan batas waktu ekonomi wajib ditentukan dalam tabel spec sebelum implementasi.

## 6. Dunia / Map

### Plot server
- Satu server menyediakan 4 plot persisten.
- Sesuai D-008, plot pemain dimulai kosong: tidak ada dekorasi, bangunan, atau tanaman yang sudah ditempatkan ketika pemain pertama kali masuk.
- Sesuai D-009 dan D-010, pemain baru menerima Starter Kit gratis sebagai item inventori: 1 Shovel permanen, 10 Watering Can, 1 Pupuk, 2 Farm Tile, 1 Trowel permanen, 10 Benih Wortel, 1 Kursi Kayu, dan 1 Lampu Taman. Item tidak otomatis ditempatkan; kondisi plot kosong tidak berarti inventori kosong.
- Plot tetap terikat pada Original Owner, termasuk ketika pemilik sedang offline.
- Pemain yang diundang dapat berpindah dari plot miliknya sendiri ke plot pengundang; plot asalnya menjadi tersedia bagi pemain lain.
- Original Owner adalah pemilik permanen plot.
- Active Owner adalah pemegang kendali aktif saat sesi berlangsung. Jika Active Owner terputus, kendali berpindah ke anggota yang memenuhi aturan transfer; ketika Original Owner kembali, kendali kembali kepadanya. Urutan pemilihan pengganti **BELUM DIPUTUSKAN**.
- Hak Build multiplayer mengikuti D-006: Original Owner dan Active Owner memiliki hak pengelolaan penuh; anggota hanya dapat memasang objek dari inventori sendiri serta memindahkan/menyimpan objek miliknya sendiri. Anggota tidak dapat mengubah objek milik pemain lain atau mengelola hak anggota.

### Stage dan ekspansi
| Stage | Ukuran plot |
|---|---:|
| 1 | 80 × 80 |
| 2 | 160 × 160 |
| 3 | 240 × 240 |
| 4 | 320 × 320 |

- Setiap upgrade stage menambah area: +40 ke kiri, +40 ke kanan, +80 ke belakang, dan +0 ke depan.
- Objek yang sudah ditempatkan tetap pada posisi tetap saat plot diperluas.
- Harga, syarat unlock, dan batas waktu upgrade **BELUM DIPUTUSKAN**.

### Tile, dekorasi, bangunan, dan tanaman
- Farm Tile dan Build Tile masing-masing menempati footprint 5×5 sel grid. Berdasarkan D-007, 1 sel = 4×4 studs sehingga footprint satu tile = 20×20 studs dan menggunakan **grid placement**.
- Farm/Build Tile harus dibeli dan masuk inventori terlebih dahulu sebelum ditempatkan.
- Dekorasi, bangunan, dan tanaman menggunakan **free placement**; penempatannya tidak diwajibkan mengikuti grid tile dan tidak membutuhkan tile sebagai alas/slot.
- Pemain dapat mengaktifkan atau menonaktifkan **Snap to Grid** sebagai bantuan opsional untuk penempatan objek free placement.
- Rotasi objek menggunakan interval **90°** sebagai aturan awal.
- Aturan tabrakan menggunakan **Hybrid Collision**: tile tidak boleh overlap dengan tile lain tetapi tidak memblokir objek di atasnya; bangunan/objek Solid tidak boleh overlap dengan Solid atau Detail; tanaman/dekorasi Detail boleh overlap dengan Detail lain tetapi tidak dengan Solid.
- Setiap asset yang dapat ditempatkan wajib memiliki profil tabrakan dan bounding volume.
- Batas area penempatan, batas jumlah objek, pemindahan, penyimpanan, serta perilaku objek saat ekspansi plot masih memerlukan detail lanjutan.

## 7. UI / UX

Prinsip:
- Santai, bersih, mudah dipahami, dan tidak membebani pemain dengan angka.
- Kontrol penempatan objek harus nyaman untuk mouse dan layar sentuh.
- Informasi ekonomi ditampilkan seperlunya; dekorasi dan kebun menjadi fokus visual.

UI yang dibutuhkan secara konseptual:
- HUD Life Coin.
- Menu build/dekorasi dan inventori tile.
- Mode penempatan, rotasi, konfirmasi, dan pemindahan objek.
- Panel anggota plot dan undangan.
- Panel Shared Savings dan Spending Limit.
- Panel stage/ekspansi plot.
- UI farming: tanaman, status pertumbuhan, alat penyiraman, dan panen (detail **BELUM DIPUTUSKAN**).
- Menu informasi tanaman (D-029) untuk memeriksa kondisi tanaman. Daftar informasi, susunan panel, cara membuka, dan interaksi final masih **BELUM DIPUTUSKAN**.

## 8. Monetisasi

- Strategi monetisasi: **BELUM DIPUTUSKAN**.
- Batas desain: pemain gratis tetap dapat menikmati dekorasi dan progres utama. Monetisasi tidak boleh membuat aktivitas inti terasa wajib membayar.

## 9. Cakupan per fase

- **Discovery (Fase 0):** visi santai-dekoratif telah dikonfirmasi; lengkapi referensi, target pemain, dan batas pengalaman.
- **Konsep & GDD (Fase 1):** tetapkan core loop, aturan penempatan/dekorasi, farming minimum, dan ekonomi dasar.
- **Vertical Slice (Fase 2):** usulkan satu loop kecil yang mendukung identitas dekorasi-first. Rincian fitur dan FEAT akan ditetapkan setelah Fase 1.
- **Produksi (Fase 3+):** greenhouse, pupuk, musim, cuaca, bank lanjutan, dan sistem sosial yang lebih luas hanya masuk setelah prioritas dan scope disetujui.

## 10. Glosarium

| Istilah | Arti | Nama di kode |
|---|---|---|
| Plot | Area kebun milik satu Original Owner | `Plot` |
| Original Owner | Pemilik permanen plot | `OriginalOwner` |
| Active Owner | Anggota yang memegang kendali aktif plot saat sesi | `ActiveOwner` |
| Farm Tile | Tile untuk area pertanian, ukuran 5×5 | `FarmTile` |
| Build Tile | Tile untuk area pembangunan, ukuran 5×5 | `BuildTile` |
| Decoration | Objek dekorasi yang tidak membutuhkan tile | `Decoration` |
| Life Coin | Mata uang utama pemain | `LifeCoin` |
| Shared Savings | Saldo bersama yang dimiliki plot | `SharedSavings` |
| Spending Limit | Batas pengeluaran mingguan dari Shared Savings | `SpendingLimit` |
| Watering Can | Alat penyiraman tanaman | `WateringCan` |
| Crop | Jenis tanaman | `Crop` |
| Harvest | Hasil panen | `Harvest` |

## 11. Risiko & pertanyaan terbuka

1. Bagaimana batas area penempatan, validasi tabrakan, batas jumlah objek, dan aturan pemindahan/penyimpanan objek?
2. Apa yang terjadi pada dekorasi/tile jika stage plot berubah atau objek berada di luar area aktif?
3. Siapa yang menjadi Active Owner jika Original Owner offline dan beberapa anggota memiliki hak yang sama?
4. Bagaimana undangan, keluar plot, kick, dan pergantian anggota memengaruhi inventori serta Shared Savings?
5. Apakah saldo Shared Savings dapat diisi semua anggota atau hanya peran tertentu?
6. Apakah pembelian dapat memilih saldo pribadi atau Shared Savings setiap transaksi?
7. Apa aktivitas farming minimum yang tetap menyenangkan tanpa menggeser fokus utama dekorasi?
8. Apa jenis tanaman, waktu tumbuh, hasil panen, harga bibit, dan harga jual?
9. Apakah greenhouse, pupuk, musim, dan cuaca diperlukan untuk rilis awal atau ditunda?
10. Apa referensi game, target perangkat, strategi monetisasi, dan target panjang sesi?
11. Berapa kapasitas/konsumsi/refill Watering Can dan bagaimana 10 unit kit dihitung?
12. Berapa besar percepatan Pupuk, berapa kali dapat digunakan, dan apakah efeknya menumpuk?
13. Kapan Starter Kit diberikan dan apakah ada kebijakan pemberian ulang setelah reset akun?
