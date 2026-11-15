# 02 · Game Design Document (GDD)

**Pemilik:** ChatGPT (Perancang) · **Penyetuju:** Pemilik proyek
**Versi:** 1.0 · **Terakhir diubah:** 2026-11-15

> Dokumen ini mencatat arah desain yang telah dikonfirmasi. Detail yang belum diputuskan ditandai **BELUM DIPUTUSKAN** atau **ASUMSI** dan tidak boleh dianggap sebagai aturan implementasi.

## 1. Visi

- **Nama game / map:** Garden Life.
- **Pitch:** Garden Life adalah game Roblox santai tentang membangun, merawat, dan mendekorasi kebun pribadi bersama teman, dengan aktivitas farming serta manajemen dan ekonomi ringan sebagai pendukung.
- **Genre / pengalaman:** Cozy garden building, decorating, light farming, dan social co-op.
- **Pengalaman utama:** Kreativitas, relaksasi, rasa memiliki terhadap kebun, dan kepuasan melihat kebun berkembang sesuai gaya pemain.
- **Prioritas desain:** Dekorasi dan ekspresi personal > pengalaman sosial/co-op > farming santai > manajemen dan ekonomi ringan.
- **Game referensi (3):** **BELUM DIPUTUSKAN**. Jangan menetapkan referensi tanpa persetujuan pemilik.

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

Loop di atas adalah rancangan konseptual; detail transaksi dan pertumbuhan tetap memerlukan spec.

### Tools & perawatan tanaman

Tools yang telah dirancang dicatat dalam [FEAT-002 Tools & Perawatan Tanaman](design/FEAT-002_tools_perawatan_tanaman.md), status DRAFT. Aturan yang telah dikonfirmasi:
- Shovel dan Trowel adalah alat permanen. Shovel menghapus tanaman; Trowel memindahkan tanaman tanpa mereset progres pertumbuhannya.
- Watering Can adalah consumable. Satu penggunaan menyiram semua tanaman di dalam area berbentuk lingkaran.
- Efek penyiraman dapat bertambah melalui penggunaan berulang, tetapi dibatasi oleh nilai maksimum (D-011).
- Setiap tanaman memiliki toleransi air. Kadar air yang melampaui toleransi dapat menyebabkan overwatering dan kematian tanaman (D-012). Kadar air dan bonus pertumbuhan adalah dua nilai terpisah.
- Sprinkler adalah perangkat consumable yang ditempatkan pada plot. Area jangkauannya berbentuk lingkaran; selama durasi aktif, perangkat menyiram otomatis, mempercepat pertumbuhan, dan meningkatkan ukuran buah. Setelah durasi berakhir, perangkat dikonsumsi dan menghilang.
- Seed Extractor mengorbankan satu tanaman untuk menghasilkan benih.
- Harvest Basket menghabiskan satu penggunaan untuk mengambil seluruh buah siap panen pada satu tanaman. Panen manual satu per satu tetap tersedia.
- Plant Sprayer adalah alat permanen; cairan aplikasinya consumable dan digunakan pada satu tanaman untuk efek khusus seperti mutasi, ukuran, atau variasi.
- Pupuk dari Starter Kit direncanakan mempercepat pertumbuhan, tetapi aturan penggunaan dan efek numeriknya belum diputuskan.

Radius area, batas maksimum bonus pertumbuhan, nilai penambahan/pengurangan kadar air, toleransi tiap tanaman, durasi sebelum tanaman mati akibat overwatering, durasi Sprinkler, interval penyiraman otomatis, bonus ukuran buah, hasil Seed Extractor, dan efek cairan Plant Sprayer masih BELUM DIPUTUSKAN. Detail tersebut tidak boleh ditebak saat implementasi.
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
| Tools & perawatan tanaman | Watering Can, Sprinkler, Shovel, Trowel, Seed Extractor, Harvest Basket, Plant Sprayer, dan Pupuk | S | FEAT-002 (DRAFT) |
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
