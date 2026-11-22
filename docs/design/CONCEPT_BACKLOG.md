# CONCEPT BACKLOG · Garden Life

**Status dokumen:** Catatan desain konsep, bukan instruksi implementasi.
**Terakhir diperbarui:** 2026-11-22

Dokumen ini mengumpulkan gagasan Garden Life yang pernah dibahas agar tidak hilang saat GDD disusun ulang. Hanya hal yang dikonfirmasi pemilik yang diperlakukan sebagai keputusan. Hal yang belum lengkap tetap berstatus eksplorasi.

## 1. Identitas yang dikonfirmasi

- Garden Life adalah pengalaman Roblox santai yang berfokus pada membangun dan mendekorasi kebun.
- Manajemen dan ekonomi hanya menjadi lapisan pendukung, bukan tantangan utama.
- Life Coin adalah mata uang utama, divisualisasikan sebagai koin emas berikon daun.
- Saldo awal pribadi: 1.000 Life Coin.
- Pemain baru menerima Starter Kit gratis sebagai item inventori (D-009); komposisinya ditetapkan melalui D-010.

## 2. Plot dan multiplayer

| Elemen | Detail yang pernah diputuskan | Status |
|---|---|---|
| Plot per server | 4 plot persisten | Dikonfirmasi |
| Kepemilikan | Original Owner permanen; Active Owner mengatur plot selama sesi | Dikonfirmasi |
| Kapasitas awal | 2 pemain | Dikonfirmasi |
| Kapasitas maksimum | 3 pemain setelah upgrade | Dikonfirmasi |
| Undangan | Pemain yang menerima undangan berpindah dari plot asal ke plot pengundang; plot asal tersedia kembali | Dikonfirmasi |
| Disconnect | Active Owner berpindah ke anggota lain; kembali ke Original Owner saat ia bergabung lagi | Dikonfirmasi; urutan pemilihan pengganti belum ditentukan |
| Hak Build | Original Owner dan Active Owner memiliki hak pengelolaan penuh; anggota hanya dapat memasang item sendiri dan mengubah objek miliknya sendiri | Dikonfirmasi (D-006) |

## 3. Tile, dekorasi, dan ekspansi

| Elemen | Detail | Status |
|---|---|---|
| Farm Tile | Ukuran 5×5 sel grid (20×20 studs); dibeli dan masuk inventori sebelum ditempatkan | Dikonfirmasi (D-007 untuk skala world) |
| Build Tile | Ukuran 5×5 sel grid (20×20 studs); dibeli dan masuk inventori sebelum ditempatkan | Dikonfirmasi (D-007 untuk skala world) |
| Dekorasi | Tidak membutuhkan tile sebagai alas/slot | Dikonfirmasi |
| Stage 1 | 80×80 | Dikonfirmasi |
| Stage 2 | 160×160 | Dikonfirmasi |
| Stage 3 | 240×240 | Dikonfirmasi |
| Stage 4 | 320×320 | Dikonfirmasi |
| Arah ekspansi per upgrade | +40 kiri, +40 kanan, +80 belakang, +0 depan | Dikonfirmasi |
| Posisi objek | Objek yang sudah ditempatkan tetap pada posisi tetap saat plot berkembang | Dikonfirmasi |
| Harga dan syarat upgrade | Belum ditentukan | Terbuka |

**Skala grid dunia (D-007):** Satu sel grid = 4×4 studs. Satu Farm Tile atau Build Tile mencakup 5×5 sel = 20×20 studs. Ukuran ini membuat Stage 1 (80×80 studs) setara dengan 4×4 footprint tile.

**Aturan penempatan yang telah dikonfirmasi (D-004):** Farm Tile dan Build Tile memakai grid placement 5×5. Dekorasi, bangunan, dan tanaman memakai free placement. Snap to Grid tersedia sebagai opsi yang dapat diaktifkan/dinonaktifkan. Rotasi objek menggunakan interval 90° sebagai aturan awal.

**Hak Build multiplayer yang dikonfirmasi (D-006):** Original Owner dan Active Owner dapat Place, Move, dan Store seluruh objek di plot. Anggota hanya dapat Place dari inventori sendiri serta Move/Store objek dengan OwnerUserId miliknya sendiri. Anggota tidak dapat mengelola hak anggota plot.

**Aturan tabrakan yang dikonfirmasi (D-005):** GroundTile tidak boleh bertumpuk dengan GroundTile lain dan tidak memblokir objek di atasnya. Solid (bangunan/objek besar) tidak boleh overlap dengan Solid atau Detail. Detail (tanaman/dekorasi kecil) boleh overlap dengan Detail lain, tetapi tidak boleh menembus Solid. Setiap asset wajib memiliki PlacementProfile dan bounding volume.

Surface placement seperti pot di atas meja belum termasuk. Batas area, jumlah objek, pemindahan, penyimpanan layout, dan perilaku objek saat ekspansi masih perlu dirinci.

## 4. Shared Savings / Bank

| Elemen | Detail | Status |
|---|---|---|
| Kepemilikan saldo | Shared Savings dimiliki plot dan terpisah dari saldo pribadi | Dikonfirmasi |
| Akses anggota saat dibuat | Anggota yang sudah berada di plot mendapat akses otomatis | Dikonfirmasi |
| Akses anggota baru | Membayar biaya administrasi 5.000 Life Coin dan memerlukan persetujuan Original Owner | Dikonfirmasi |
| Spending Limit | Batas mingguan berlaku untuk semua pembelian yang memakai saldo bersama | Dikonfirmasi |
| Pengaturan limit | Original Owner dapat mengubah atau menghapus limit (Unlimited) | Dikonfirmasi |
| Biaya pembuatan rekening | Belum dapat dipastikan dari keputusan yang tersedia | Terbuka |
| Isi saldo, penarikan, audit transaksi | Belum ditentukan | Terbuka |
| Pilihan sumber pembayaran | Personal atau Shared Savings per transaksi pernah dibahas, tetapi aturan final perlu dikonfirmasi | Terbuka |

## 5. Sistem farming yang pernah dibahas

Ini adalah gagasan terdahulu yang belum memiliki spesifikasi final. Jangan anggap angka atau fitur berikut sudah masuk scope Vertical Slice.

| Sistem | Detail awal yang pernah muncul | Yang masih harus diputuskan |
|---|---|---|
| Petak tanam | Area farming 5×5 | Apakah sama persis dengan ukuran Farm Tile dan bagaimana penempatan tanaman |
| Watering Can | Kapasitas awal 100 ml | Konsumsi per siram, sumber refill, jangkauan, cooldown |
| Greenhouse | Kapasitas maksimal 18 tanaman | Unlock, biaya, aturan tumbuh, interaksi dengan cuaca |
| Pupuk | 5 tier | Efek tiap tier, harga, durasi, stacking |
| Musim | 4 musim | Durasi, kalender, tanaman musiman |
| Cuaca | Efek cuaca pada farming | Jenis cuaca, peluang, dampak numerik |
| Tanaman | Sistem tanam dan panen | Daftar crop, bibit, waktu tumbuh, yield, harga jual |
| Gudang | Konsep gudang bersama | Kapasitas, hak akses, pemisahan item pribadi/plot |


### Roster tanaman reguler (D-064)
Roster 20 tanaman reguler telah disetujui pemilik untuk konsep. Roster ini bukan spec implementasi dan tidak otomatis menetapkan scope Vertical Slice.

| Tier | Tanaman | Jumlah |
|---|---|---:|
| Common | Carrot, Daisy, Strawberry, Lettuce | 4 |
| Uncommon | Tulip, Blueberry, Bell Pepper, Mint | 4 |
| Rare | Sunflower, Watermelon, Lavender, Peony | 4 |
| Epic | Orchid, Dragonfruit, Firefly Mushroom | 3 |
| Legendary | Wisteria, Sakura | 2 |
| Mystic | Starflower, Aurora Rose, Stardust Willow | 3 |
| **Total** | **20 tanaman** | **20** |

Golden Apple dan Moonflower tetap tanaman event dan tidak termasuk roster reguler. Harga, pertumbuhan, yield, season affinity, kebutuhan air/panas/dingin, cara memperoleh, dan detail visual final masih terbuka. Baseline harga tier D-052 tidak diubah.

### Eksplorasi Spring: identitas dan cuaca (D-028)

Bagian ini mencatat konsep Spring yang telah dikonfirmasi pemilik. Seasons & Weather masih berstatus eksplorasi dan belum otomatis menjadi scope rilis.

| Elemen | Rancangan yang dikonfirmasi | Status |
|---|---|---|
| Identitas visual | Fresh Nature: hijau segar, kuning, dan warna bunga alami; cerah, hidup, dan penuh energi | Dikonfirmasi |
| Pola cuaca | Balanced: cuaca cerah dan hujan relatif seimbang | Dikonfirmasi; distribusi angka terbuka |
| Roster Spring | Sunny, Cloudy, Drizzle, Rainy, Windy, Misty, Thunderstorm | Dikonfirmasi sebagai roster konsep |
| Sunny | Cuaca awal Spring, cuaca dasar dan sering muncul; netral tanpa efek tanaman atau Mutation | Dikonfirmasi |
| Cloudy | Transisi yang dapat mendahului Drizzle, Rainy, atau Thunderstorm | Dikonfirmasi |
| Cloudy: WaterLevel | +0,25 satu kali saat episode Cloudy dimulai; tidak berkala | Dikonfirmasi |
| Cloudy: waktu tumbuh | +15% waktu tumbuh untuk tanaman dengan kebutuhan sinar matahari tinggi | Dikonfirmasi |
| Cloudy saat tanaman sedang tumbuh | Sisa waktu tumbuh bertambah 15%; progres yang sudah diperoleh tidak dihapus | Dikonfirmasi |
| Cloudy: Mutation | Tidak menghasilkan Mutation | Dikonfirmasi |
| Drizzle | Gerimis lembut dan menenangkan; WaterLevel +0,05 setiap tick; Mutation Wet 2,5% per buah secara independen setiap tick; seluruh tanaman mendapat +15% waktu tumbuh tanpa bonus pertumbuhan | Dikonfirmasi (D-030) |
| Rainy | Hujan sedang hingga deras tetapi tetap tenang; WaterLevel +0,075 per tick; Wet 5% per buah per tick; Wet dapat berevolusi menjadi Flooded dengan peluang 2,5% per buah per tick; seluruh tanaman mendapat +20% waktu tumbuh tanpa bonus pertumbuhan | Dikonfirmasi (D-034) |
| Windy | Angin sepoi-sepoi; WaterLevel -0,005 setiap 2 tick (60 detik); kecepatan pertumbuhan seluruh tanaman dan buah 1,5x; tidak menghasilkan Mutation | Dikonfirmasi (D-036) |
| Misty | WaterLevel +0,25 satu kali saat episode dimulai; seluruh tanaman mendapat +15% waktu tumbuh; Mutation Misty 6,697% per buah eligible per tick (75% kumulatif setelah 20 roll); Misty dapat berevolusi menjadi Foggy dengan peluang 0,809% per tick eligible (15% setelah 20 roll evolusi eligible); Foggy menggantikan Misty | Dikonfirmasi (D-037) |
| Thunderstorm | 1% chance sambaran per plot per tick; maksimal 5 sambaran per episode; dampak radius 8 studs; Shocked 100% dan Charged 15% per buah pada tanaman tersambar; risiko 25% gosong / 15% mati (saling eksklusif); WaterLevel +0,075 per tick dan +20% waktu tumbuh; Lightning Rod radius 24 studs, 50% pengalihan, 3 sambaran; Thunderstorm Relief radius 20 studs, pengurangan risiko 5 poin persentase per stack, maksimal 3 item; setiap item memiliki durabilitas 3 sambaran secara independen dan setiap sambaran mengurangi durabilitas semua item yang area perlindungannya mencakup titik sambaran | Dikonfirmasi sebagai konsep (D-038) |
| Mutation Flooded | Peluang dari WaterLevel 4,00-4,99: 2,5% per 2 menit; WaterLevel 5,00: 2,5% per 1 menit. Satu Flooded per buah lintas semua jalur | Dikonfirmasi (D-035) |
| Presisi WaterLevel | Internal 0,001 (integer 0-5000); UI tetap 2 angka desimal; Rainy +0,075 × 20 tick = +1,500 | Dikonfirmasi (D-033) |
| Durasi cuaca non-Sunny | 20 tick × 30 detik = 600 detik/10 menit per episode | Dikonfirmasi (D-031) |
| Siklus cuaca Spring | Bobot ASUMSI 34/16/14/12/10/8/6 untuk Sunny/Cloudy/Drizzle/Windy/Rainy/Misty/Thunderstorm; aturan transisi D-048 | Dikonfirmasi sebagai konsep (D-048) |
| Durasi Sunny | 40 tick / 20 menit | Dikonfirmasi (D-048) |
| Menu informasi tanaman | Menu khusus agar pemain dapat memeriksa kondisi tanaman; rincian isi dan interaksi belum ditetapkan (D-029) | Kebutuhan konseptual dikonfirmasi |

- Klasifikasi kebutuhan sinar matahari tanaman diperlukan untuk menerapkan efek Cloudy secara selektif; nama field dan skema data belum ditetapkan.
- Durasi non-Sunny 10 menit dan Sunny 20 menit. Bobot Spring masih ASUMSI balancing; aturan transisi aktif ada di D-048.
- WaterLevel memakai presisi internal 0,001, tetapi UI tetap menampilkan dua angka desimal. Jangan membulatkan nilai per tick.
- Rainy menjalankan roll Wet dan evolusi Wet→Flooded per buah. Urutan kedua roll ketika keduanya berpotensi terjadi pada tick yang sama masih perlu ditentukan sebelum implementasi.
- Multiplier dan tampilan Wet/Flooded/Misty/Foggy, serta modifier cuaca untuk tanaman yang baru ditanam di tengah episode, masih terbuka.
- Efek Cloudy pada sisa waktu pertumbuhan harus diproses satu kali ketika episode Cloudy dimulai untuk tanaman yang sedang tumbuh dan memenuhi syarat. Detail penanganan beberapa episode sebelum tanaman selesai tumbuh perlu dirinci sebelum implementasi.
- Drizzle melakukan roll Mutation Wet per buah secara independen pada setiap tick 30 detik. Jenis Mutation yang sama tidak boleh tercatat dua kali pada buah yang sama sesuai D-022.
- WaterLevel Drizzle tidak boleh melewati batas 5,00. Aturan penerapan modifier pertumbuhan pada tanaman yang baru ditanam selama Drizzle masih terbuka.
- Windy mengurangi WaterLevel sebesar 0,005 setiap dua tick dan menerapkan multiplier laju pertumbuhan 1,5x pada seluruh tanaman serta pertumbuhan buah. Windy tidak menghasilkan Mutation (D-036).
- Misty menambahkan WaterLevel +0,25 satu kali pada awal episode dan +15% waktu tumbuh untuk seluruh tanaman. Roll Misty dan evolusi Foggy dilakukan independen per buah; Foggy menggantikan Misty setelah evolusi berhasil (D-037). Peluang Foggy 15% berlaku setelah 20 roll evolusi eligible, bukan otomatis per episode karena eligibility baru dimulai setelah buah memperoleh Misty.
- Thunderstorm memiliki risiko gosong/mati serta opsi revive Robux; penalti gosong, hasil pupuk, harga revive, dan multiplier Shocked/Charged belum ditentukan (D-038).
- **Scorched (D-039, D-040):** Tanaman terlihat hitam seperti hangus, menghasilkan 50% jumlah buah normal dengan pembulatan ke bawah (termasuk 0 buah jika hasil normal 1), dan tidak pulih otomatis. Satu Vitamin menyembuhkan satu tanaman; efeknya hanya menghapus status Scorched tanpa mengubah umur, ukuran, atau progres pertumbuhan. Setelah pulih, hasil buah kembali normal. Sumber, harga, batas stack, dan UI Vitamin masih terbuka.
- Detail distribusi peluang cuaca, transisi, dan penanganan beberapa Lightning Rod dengan area tumpang tindih masih terbuka.
- Tidak ada angka ekonomi atau perubahan source/sink yang ditetapkan oleh konsep ini.

### Eksplorasi Summer: Golden Summer dan Countryside Summer (D-041, D-042)

| Elemen | Rancangan yang dikonfirmasi | Status |
|---|---|---|
| Identitas visual dan suasana | Golden Summer: cerah dan hangat | Dikonfirmasi (D-041) |
| Arah lingkungan | Countryside Summer: hamparan rumput, padang bunga, kebun buah, pagar kayu, dan lanskap pedesaan musim panas | Dikonfirmasi (D-042) |
| Arah palet warna | Fresh Summer: hijau segar, biru langit, kuning cerah, dan putih, dengan aksen emas dari Golden Summer | Dikonfirmasi (D-043) |
| Pembagian warna elemen | Rumput hijau; langit biru dan awan putih; bunga kuning/putih/krem; kebun buah hijau dengan buah cerah; kayu cokelat muda/beige/krem; jalan beige/tanah hangat; emas hanya aksen | Dikonfirmasi (D-044) |
| Detail warna dan pencahayaan | Kode warna, proporsi, intensitas/sudut cahaya, dan saturasi | Terbuka |
| Vegetasi dan aset | Spesies bunga, pohon buah, rumput, pagar, jalan, dan properti pedesaan spesifik | Terbuka |
| Cuaca | Roster Sunny/Cloudy/Windy/Heatwave/Summer Shower/Muggy/Tornado (D-051) | Dikonfirmasi sebagai konsep |
| Efek gameplay | WaterLevel, pertumbuhan, buah, Mutation, dan kondisi tanaman | Terbuka |
| Tanaman musiman dan kalender | Jenis tanaman dan hubungan Summer dengan sistem kalender | Terbuka |
| Pemicu Tornado | Heatwave → Summer Shower → Muggy → Tornado; rantai harus berurutan | Dikonfirmasi sebagai konsep (D-045) |
| Distribusi Tornado | Satu penghitung per server; minimal 1 dan maksimal 5 per Summer; lima pemeriksaan pada progres 50/60/70/80/85%; empat peluang awal 10%; jaminan pada 85% jika belum ada Tornado | Dikonfirmasi sebagai konsep (D-045) |
| Scope rilis | Spring dan tiga musim lain ditargetkan lengkap untuk First Release; scope Vertical Slice belum ditentukan | First Release dikonfirmasi; Vertical Slice terbuka |
**Aturan Tornado Summer (D-045):** Penghitung berlaku untuk satu server dan direset pada awal Summer baru. Tornado minimal terjadi 1 kali dan maksimal 5 kali per Summer. Kesempatan pemeriksaan tersedia pada progres 50%, 60%, 70%, 80%, dan 85%. Empat kesempatan pertama masing-masing memiliki peluang 10% untuk memulai rantai. Pada kesempatan kelima, peluangnya 10% jika setidaknya satu Tornado sudah terjadi; jika belum ada Tornado, rantai dijamin dimulai. Rantai Heatwave → Summer Shower → Muggy → Tornado harus berurutan. Interupsi cuaca pada kesempatan biasa membatalkan rantai dan kesempatan tidak dikembalikan. Rantai pada kesempatan jaminan dilindungi dari interupsi cuaca. Satu rantai hanya menghasilkan satu Tornado. Durasi Summer dan cuaca masih perlu ditentukan agar jaminan pada progres 85% dapat selesai sebelum musim berakhir.

#### Heatwave dan kondisi tanaman Summer (D-046)

| Elemen | Rancangan yang dikonfirmasi | Status |
|---|---|---|
| Penguapan | WaterLevel seluruh tanaman berkurang bertahap selama Heatwave; minimum 0,000; berhenti saat cuaca berakhir | Dikonfirmasi; nilai per tick terbuka |
| Heat-loving | Laju tumbuh 1,25× | Dikonfirmasi (D-051) |
| Heat-neutral | Tidak mendapat bonus atau penalti | Dikonfirmasi |
| Heat-sensitive | Laju tumbuh 0,75×; Overheat setelah 3 menit; risiko mati 20% | Dikonfirmasi (D-051) |
| Extremely Heat-sensitive | Laju tumbuh 0,50×; Overheat setelah 3 menit; risiko mati 40% | Dikonfirmasi (D-051) |
| Overheat | Heat-sensitive dan Extremely Heat-sensitive mendapat status setelah 3 menit paparan panas berturut-turut | Dikonfirmasi |
| Risiko kematian | Diperiksa saat Overheat dimulai; Heat-sensitive di bawah 50%; Extremely Heat-sensitive dapat mati | Dikonfirmasi secara konsep; peluang tepat terbuka |
| Pemulihan Overheat | Membutuhkan 30 menit dalam kondisi pemulihan (lingkungan/cuaca tidak panas atau hujan); tidak hilang seketika saat Heatwave berakhir | Dikonfirmasi; perilaku timer saat panas kembali terbuka |
| Cooling Balm | Rebranding Ice Cooler; menghapus status Overheat seketika | Dikonfirmasi (D-051) |
| Sunburnt | Mutation buah, target kumulatif 45% setelah 20 tick; 2,945% per tick | Dikonfirmasi dengan asumsi 20 tick |
| Blazing | Mutation buah, target kumulatif 10% setelah 20 tick; 0,5254% per tick | Dikonfirmasi dengan asumsi 20 tick |
| Stacking mutasi | Sunburnt dan Blazing dapat dimiliki bersamaan pada buah yang sama | Dikonfirmasi |
| Durasi dan angka final | Durasi Heatwave, penguapan, modifier, peluang kematian, multiplier Mutation | Terbuka |


## 6. Prinsip penyaringan fitur

Sebelum sebuah gagasan dipindahkan menjadi FEAT spec:
1. Pastikan fitur memperkuat pengalaman santai dan kreativitas dekorasi.
2. Hindari kebutuhan login harian atau grind yang menghukum pemain yang tidak aktif.
3. Ekonomi harus sederhana dan tidak mengambil alih fokus dekorasi.
4. Tetapkan source dan sink Life Coin agar ekonomi tidak menciptakan inflasi tanpa tujuan.
5. Pisahkan keputusan yang telah dikonfirmasi dari asumsi dan usulan baru.
6. Setiap angka implementasi harus masuk tabel tuning pada spec fitur.

## 7. Starter Kit

| Item | Jumlah | Fungsi / status |
|---|---:|---|
| Shovel | 1 | Menghapus tanaman; alat permanen |
| Watering Can | 10 | Menyiram tanaman; kapasitas/refill belum ditentukan |
| Pupuk | 1 | Mempercepat tanaman; efek/penggunaan belum ditentukan |
| Farm Tile | 2 | Area pertanian |
| Trowel | 1 | Memindahkan tanaman; alat permanen |
| Benih Wortel | 10 | Bibit awal |
| Kursi Kayu | 1 | Dekorasi |
| Lampu Taman | 1 | Dekorasi |

- Pemberian: gratis untuk pemain baru, D-009.
- Bentuk: item masuk inventori dan tidak otomatis ditempatkan di plot, D-009.
- Komposisi dan kuantitas: dikonfirmasi melalui D-010.
- Waktu pemberian dan aturan perolehan ulang: masih terbuka.\n\n## 8. Pertanyaan desain berikutnya

- Bagaimana detail Build Mode (preview, konfirmasi, undo/move) dan batas area penempatan?
- Apakah perlu aturan tabrakan berbeda untuk tile, dekorasi, bangunan, dan tanaman?
- Apa loop farming minimum yang cukup untuk mendukung pembelian dekorasi?
- Bagaimana pemain memperoleh, menyimpan, dan membelanjakan Life Coin?
- Bagaimana hak anggota plot di luar Build Mode dibedakan (farm, bank, invite, remove)?
- Apa aturan penyelesaian sesi dan penyimpanan layout saat beberapa pemain mengedit bersamaan?

### Pupuk dan timer plot kosong (D-049)

- Timer pupuk freeze saat plot kosong dan berjalan ketika minimal satu pemain menempati plot.
- First Release memakai Basic Fertilizer (+0,2×, 120 tick) dan Premium Fertilizer (+0,5×, 240 tick).
- Satu pupuk aktif per tanaman; tidak dapat ditumpuk atau menggantikan efek aktif.
- Dapat digunakan bersama Season Pill, cuaca, dan Greenhouse; tidak dapat digunakan pada Dormant, Layu, atau Mati.
- Harga, sumber, stack inventori, dan detail formula pertumbuhan masih terbuka.
- Batas 15 berlaku pada jumlah Mutation unik per buah, bukan multiplier pertumbuhan.
| Transcendent | Tanaman khusus musiman, cara perolehan unik (contoh: Whispering Lily) | Backlog |