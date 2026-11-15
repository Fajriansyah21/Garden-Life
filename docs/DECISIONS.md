# DECISIONS · Log Keputusan

Aturan: **hanya ditambah, tidak dihapus.** Untuk mengubah keputusan, tulis entri baru yang menyebut "Menggantikan D-0xx".
Entri terbaru di paling atas.

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
