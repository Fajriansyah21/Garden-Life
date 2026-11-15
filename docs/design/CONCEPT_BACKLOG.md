# CONCEPT BACKLOG · Garden Life

**Status dokumen:** Catatan desain konsep, bukan instruksi implementasi.
**Terakhir diperbarui:** 2026-11-15

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
| Durasi cuaca non-Sunny | 20 tick × 30 detik = 600 detik/10 menit per episode | Dikonfirmasi (D-031) |
| Durasi Sunny | Dikecualikan dari durasi standar cuaca lain | Terbuka |
| Menu informasi tanaman | Menu khusus agar pemain dapat memeriksa kondisi tanaman; rincian isi dan interaksi belum ditetapkan (D-029) | Kebutuhan konseptual dikonfirmasi |

- Klasifikasi kebutuhan sinar matahari tanaman diperlukan untuk menerapkan efek Cloudy secara selektif; nama field dan skema data belum ditetapkan.
- Durasi setiap cuaca non-Sunny ditetapkan 10 menit; durasi Sunny masih terbuka. Peluang dan distribusi kemunculan serta aturan lengkap Rainy, Windy, Misty, dan Thunderstorm masih terbuka.
- Efek Cloudy pada sisa waktu pertumbuhan harus diproses satu kali ketika episode Cloudy dimulai untuk tanaman yang sedang tumbuh dan memenuhi syarat. Detail penanganan beberapa episode sebelum tanaman selesai tumbuh perlu dirinci sebelum implementasi.
- Drizzle melakukan roll Mutation Wet per buah secara independen pada setiap tick 30 detik. Jenis Mutation yang sama tidak boleh tercatat dua kali pada buah yang sama sesuai D-022.
- WaterLevel Drizzle tidak boleh melewati batas 5,00. Aturan penerapan modifier pertumbuhan pada tanaman yang baru ditanam selama Drizzle masih terbuka.
- Tidak ada angka ekonomi atau perubahan source/sink yang ditetapkan oleh konsep ini.

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
