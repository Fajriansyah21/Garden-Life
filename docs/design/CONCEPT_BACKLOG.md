# CONCEPT BACKLOG · Garden Life

**Status dokumen:** Catatan desain konsep, bukan instruksi implementasi.
**Terakhir diperbarui:** 2026-11-15

Dokumen ini mengumpulkan gagasan Garden Life yang pernah dibahas agar tidak hilang saat GDD disusun ulang. Hanya hal yang dikonfirmasi pemilik yang diperlakukan sebagai keputusan. Hal yang belum lengkap tetap berstatus eksplorasi.

## 1. Identitas yang dikonfirmasi

- Garden Life adalah pengalaman Roblox santai yang berfokus pada membangun dan mendekorasi kebun.
- Manajemen dan ekonomi hanya menjadi lapisan pendukung, bukan tantangan utama.
- Life Coin adalah mata uang utama, divisualisasikan sebagai koin emas berikon daun.
- Saldo awal pribadi: 1.000 Life Coin.

## 2. Plot dan multiplayer

| Elemen | Detail yang pernah diputuskan | Status |
|---|---|---|
| Plot per server | 4 plot persisten | Dikonfirmasi |
| Kepemilikan | Original Owner permanen; Active Owner mengatur plot selama sesi | Dikonfirmasi |
| Kapasitas awal | 2 pemain | Dikonfirmasi |
| Kapasitas maksimum | 3 pemain setelah upgrade | Dikonfirmasi |
| Undangan | Pemain yang menerima undangan berpindah dari plot asal ke plot pengundang; plot asal tersedia kembali | Dikonfirmasi |
| Disconnect | Active Owner berpindah ke anggota lain; kembali ke Original Owner saat ia bergabung lagi | Dikonfirmasi; urutan pemilihan pengganti belum ditentukan |

## 3. Tile, dekorasi, dan ekspansi

| Elemen | Detail | Status |
|---|---|---|
| Farm Tile | Ukuran 5×5; dibeli dan masuk inventori sebelum ditempatkan | Dikonfirmasi |
| Build Tile | Ukuran 5×5; dibeli dan masuk inventori sebelum ditempatkan | Dikonfirmasi |
| Dekorasi | Tidak membutuhkan tile sebagai alas/slot | Dikonfirmasi |
| Stage 1 | 80×80 | Dikonfirmasi |
| Stage 2 | 160×160 | Dikonfirmasi |
| Stage 3 | 240×240 | Dikonfirmasi |
| Stage 4 | 320×320 | Dikonfirmasi |
| Arah ekspansi per upgrade | +40 kiri, +40 kanan, +80 belakang, +0 depan | Dikonfirmasi |
| Posisi objek | Objek yang sudah ditempatkan tetap pada posisi tetap saat plot berkembang | Dikonfirmasi |
| Harga dan syarat upgrade | Belum ditentukan | Terbuka |

**Aturan penempatan yang telah dikonfirmasi (D-004):** Farm Tile dan Build Tile memakai grid placement 5×5. Dekorasi, bangunan, dan tanaman memakai free placement. Snap to Grid tersedia sebagai opsi yang dapat diaktifkan/dinonaktifkan. Rotasi objek menggunakan interval 90° sebagai aturan awal.

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

## 6. Prinsip penyaringan fitur

Sebelum sebuah gagasan dipindahkan menjadi FEAT spec:
1. Pastikan fitur memperkuat pengalaman santai dan kreativitas dekorasi.
2. Hindari kebutuhan login harian atau grind yang menghukum pemain yang tidak aktif.
3. Ekonomi harus sederhana dan tidak mengambil alih fokus dekorasi.
4. Tetapkan source dan sink Life Coin agar ekonomi tidak menciptakan inflasi tanpa tujuan.
5. Pisahkan keputusan yang telah dikonfirmasi dari asumsi dan usulan baru.
6. Setiap angka implementasi harus masuk tabel tuning pada spec fitur.

## 7. Pertanyaan desain berikutnya

- Bagaimana detail Build Mode (preview, konfirmasi, undo/move) dan batas area penempatan?
- Apakah perlu aturan tabrakan berbeda untuk tile, dekorasi, bangunan, dan tanaman?
- Apa loop farming minimum yang cukup untuk mendukung pembelian dekorasi?
- Bagaimana pemain memperoleh, menyimpan, dan membelanjakan Life Coin?
- Bagaimana hak anggota plot dibedakan (build, farm, bank, invite, remove)?
- Apa aturan penyelesaian sesi dan penyimpanan layout saat beberapa pemain mengedit bersamaan?
