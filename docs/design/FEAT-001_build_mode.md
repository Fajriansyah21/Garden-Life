# FEAT-001 · Build Mode & Hybrid Placement

| Field | Isi |
|---|---|
| Status | DRAFT |
| Versi | v1 |
| Prioritas | Must |
| Fase | 2 Vertical Slice (usulan; scope fase menunggu persetujuan pemilik) |
| Penulis | ChatGPT |
| Disetujui oleh | |
| Bergantung pada | D-003, D-004, D-005 |
| Perkiraan biaya | Belum dinilai Claude |

## 1. Tujuan pemain

Pemain dapat menata kebunnya dengan memasang, memindahkan, dan menyimpan tile, bangunan, tanaman, serta dekorasi secara intuitif. Sistem memberi struktur pada tile, tetapi tetap memberi kebebasan kreatif untuk objek kebun.

## 2. Aturan

### 2.1 Memasuki Build Mode
1. Pemain membuka Build Mode melalui tombol Build.
2. Build Mode menampilkan kategori inventori: Tiles, Decorations, Buildings, dan Plants.
3. Pemain hanya dapat melakukan perubahan pada plot yang sedang aktif dan jika server mengizinkan hak Build untuk pemain tersebut.
4. Saat Build Mode aktif, interaksi gameplay yang dapat mengubah objek yang sedang diedit dinonaktifkan untuk pemain tersebut.
5. Menutup Build Mode membatalkan preview yang belum dikonfirmasi dan mempertahankan seluruh perubahan yang sudah berhasil disimpan.

### 2.2 Memilih dan memasang objek
1. Pemain memilih objek yang jumlahnya tersedia di inventori.
2. Sistem membuat placement preview lokal. Preview tidak dianggap sebagai objek dunia yang tersimpan.
3. Pemain menggerakkan preview dengan mouse atau input sentuh.
4. Farm Tile dan Build Tile menggunakan grid placement 5×5 sesuai D-004.
5. Dekorasi, bangunan, dan tanaman menggunakan free placement sesuai D-004.
6. Snap to Grid merupakan opsi bagi objek free placement. Status ON/OFF dipertahankan selama sesi Build Mode; nilai default awal **ASUMSI: OFF** agar free placement terasa bebas.
7. Semua objek dapat diputar dalam interval 90° sesuai D-004. Rotasi preview tidak mengubah data inventori.
8. Preview menampilkan status valid atau tidak valid. Pemain tidak dapat mengonfirmasi preview yang tidak valid.
9. Saat Place ditekan, client mengirim permintaan penempatan. Server memvalidasi ulang hak Build, inventori, batas plot, metadata objek, dan collision.
10. Jika validasi server berhasil, server membuat objek pada posisi dan rotasi yang disetujui, menyimpan perubahan layout, lalu mengurangi inventori sebanyak 1.
11. Jika validasi gagal, tidak ada objek yang dibuat dan inventori tidak berubah.

### 2.3 Profil tabrakan (Hybrid Collision, D-005)
Setiap asset yang dapat ditempatkan wajib memiliki satu `PlacementProfile` dan bounding volume yang ditetapkan pada metadata asset.

| Profil | Contoh | Aturan tabrakan |
|---|---|---|
| GroundTile | Farm Tile, Build Tile | Tidak boleh overlap dengan GroundTile lain. Tidak memblokir Solid atau Detail. |
| Solid | Bangunan dan objek besar | Tidak boleh overlap dengan Solid atau Detail. |
| Detail | Tanaman, pot, lampu kecil, ornamen | Boleh overlap dengan Detail lain. Tidak boleh overlap dengan Solid. |

1. Tabrakan dihitung menggunakan bounding volume asset setelah rotasi diterapkan.
2. GroundTile hanya diuji terhadap GroundTile. Tile tetap merupakan permukaan dasar, bukan syarat untuk meletakkan objek lain.
3. Solid diuji terhadap Solid dan Detail.
4. Detail diuji terhadap Solid; Detail tidak diuji terhadap Detail.
5. Asset tanpa PlacementProfile atau bounding volume yang valid tidak dapat ditempatkan.
6. Surface placement (contoh: pot di atas meja) **tidak termasuk** dalam v1. Objek tidak dapat diletakkan di atas objek lain kecuali asset dan aturan surface placement telah disediakan pada fitur terpisah.

### 2.4 Batas plot dan rotasi
1. Seluruh bounding volume objek harus berada di dalam batas area plot aktif.
2. Pemeriksaan batas menggunakan bounding volume setelah rotasi, bukan hanya posisi pivot.
3. Rotasi dilakukan satu langkah 90° per input dan berputar dalam siklus 0°, 90°, 180°, 270°.
4. Objek yang sudah ditempatkan tidak berpindah ketika pemain memulai placement objek baru.
5. Objek yang berada di luar area plot aktif tidak dapat dipindahkan lebih jauh ke luar area.

### 2.5 Move dan Store
1. Pemain memilih objek yang sudah terpasang lalu memilih Move atau Store.
2. Move membuat preview dari objek yang dipilih. Objek asli tetap tersimpan pada posisi lama sampai posisi baru dikonfirmasi.
3. Jika Move dibatalkan atau validasi posisi baru gagal, objek asli tetap berada pada posisi dan rotasi semula.
4. Jika Move berhasil, server mengganti transform objek yang sama dan menyimpan layout. Inventori tidak berubah.
5. Store menghapus objek dari dunia dan mengembalikan 1 item dengan ID yang sama ke inventori pemilik item.
6. Store tidak menghasilkan Life Coin dan tidak menghapus kepemilikan item.
7. Store untuk tanaman yang memiliki state pertumbuhan atau hasil panen **ditunda** sampai aturan farming/inventori tanaman ditetapkan. Pada v1, tanaman hanya dapat dipindahkan jika asset crop ditandai mendukung Move; tidak dapat di-Store melalui Build Mode.

### 2.6 Cancel dan penyimpanan
1. Cancel selama preview placement membatalkan preview tanpa mengubah inventori atau layout.
2. Cancel selama Move membatalkan perpindahan dan mempertahankan objek pada posisi semula.
3. Setiap Place, Move, atau Store yang berhasil merupakan satu operasi server-authoritative dan disimpan ke data layout plot.
4. Tidak ada tombol Delete permanen pada v1. Store adalah jalur pengambilan objek.
5. Undo multi-operasi tidak termasuk v1.
6. Jika pemain keluar saat preview berlangsung, preview dibuang. Jika pemain keluar setelah operasi server berhasil, perubahan tetap tersimpan.

### 2.7 Multiplayer dan keamanan
1. Server menjadi otoritas untuk inventori, hak Build, transform objek, collision, dan penyimpanan layout.
2. Client tidak boleh menentukan sendiri bahwa penempatan berhasil.
3. Server menolak permintaan untuk plot yang bukan plot aktif pemain atau ketika pemain tidak memiliki hak Build.
4. Saat satu objek sedang dipindahkan oleh seorang pemain, server memberi lock sementara pada objek tersebut. Permintaan Move/Store lain untuk objek yang sama ditolak sampai operasi selesai atau lock dilepas.
5. Lock dilepas setelah operasi berhasil, dibatalkan, pemain keluar, atau sesi Build Mode berakhir.
6. Permintaan Place/Move/Store yang dikirim berulang dengan operation ID yang sama hanya boleh diterapkan satu kali.
7. Model hak Build untuk Original Owner, Active Owner, dan anggota plot **BELUM DIPUTUSKAN**. Implementasi multiplayer tidak boleh menebak matriks izin; perlu keputusan pemilik atau spec permission terpisah.

## 3. Data & angka tuning

| Parameter | Nilai | Satuan | Catatan |
|---|---:|---|---|
| Tile grid footprint | 5×5 | ukuran tile | Sesuai D-003/D-004; konversi ke world studs belum ditetapkan |
| Rotation step | 90 | derajat | D-004 |
| Rotation states | 4 | orientasi | 0°, 90°, 180°, 270° |
| Snap to Grid default | OFF | boolean | ASUMSI desain, perlu persetujuan |
| Undo history | 0 | operasi | Tidak termasuk v1 |
| Permanent delete | Tidak tersedia | boolean | Gunakan Store |
| Placement preview | 1 | objek aktif per pemain | Mencegah beberapa preview yang membingungkan |
| Object lock | 1 | pemegang lock per objek | Lock hanya saat Move/Store |
| Store refund | 1 | item | Kembali ke inventori tanpa Life Coin |

## 4. Kondisi tepi & kegagalan

- Inventori kosong: tombol Place dinonaktifkan dan UI menampilkan pesan "Item tidak tersedia".
- Preview di luar plot: preview berstatus tidak valid dan Place dinonaktifkan.
- Collision tidak valid: preview berstatus tidak valid; tidak ada perubahan data.
- Metadata asset tidak lengkap: asset tidak dapat dipilih untuk placement.
- Pemain tidak memiliki hak Build: server menolak permintaan dan UI menampilkan pesan izin.
- Pemain keluar saat preview: preview dibuang tanpa perubahan.
- Pemain keluar setelah server menerima operasi: server menyelesaikan operasi secara atomik atau menolak seluruh operasi; inventori dan layout tidak boleh berada pada kondisi setengah berubah.
- Dua pemain memindahkan objek yang sama: hanya pemegang lock yang dapat menyelesaikan operasi.
- Inventori gagal disimpan: operasi placement tidak boleh dianggap berhasil; server harus menjaga konsistensi layout dan inventori.
- Remote palsu atau data posisi di luar batas: server memvalidasi ulang seluruh field dan menolak permintaan tidak valid.
- Plot diperluas: objek yang sudah ditempatkan tetap pada koordinat dunia semula sesuai D-003; area baru menjadi area placement yang tersedia.
- Tanaman dengan state farming: Store tidak tersedia pada v1; aturan Move perlu mengikuti dukungan asset dan tidak boleh mereset state tanaman.

## 5. Data yang disimpan

### Data layout plot
| Field | Tipe | Keterangan |
|---|---|---|
| PlotId | string | ID plot persisten |
| PlacedObjectId | string | ID unik instance objek |
| AssetId | string | ID asset dari katalog |
| Category | enum | GroundTile / Decoration / Building / Plant |
| Position | Vector3 atau representasi serializable | Posisi dunia yang tervalidasi |
| RotationY | number | Sudut rotasi 0/90/180/270 |
| PlacementProfile | enum | GroundTile / Solid / Detail |
| OwnerUserId | number | Pemilik item, bila item bersifat personal |
| StateData | table | State tambahan objek; tanaman dikelola sistem farming |

### Inventori
- Menyimpan jumlah item berdasarkan AssetId dan pemilik inventori.
- Place mengurangi jumlah 1 hanya setelah server berhasil menyimpan objek.
- Store menambahkan kembali jumlah 1 setelah server berhasil menghapus objek dari layout.
- Move tidak mengubah jumlah inventori.

### Data sesi (tidak persisten)
- BuildModeActive
- ActivePreviewAssetId
- SnapToGridEnabled
- ActiveRotation
- ObjectLockOwner
- OperationId

## 6. UI yang dibutuhkan

1. Tombol Build pada HUD.
2. Panel kategori: Tiles, Decorations, Buildings, Plants.
3. Daftar item dengan thumbnail, nama, dan jumlah inventori.
4. Placement preview dengan indikator valid/tidak valid.
5. Tombol Place dan Cancel.
6. Tombol Rotate kiri/kanan atau satu tombol Rotate 90°.
7. Toggle Snap to Grid untuk objek free placement.
8. Saat memilih objek terpasang: menu Move dan Store.
9. Pesan kesalahan singkat untuk inventori kosong, posisi tidak valid, izin ditolak, atau objek sedang diedit pemain lain.
10. Kontrol harus tersedia untuk mouse/keyboard dan layar sentuh.

## 7. Asset yang dibutuhkan

| Asset | Status |
|---|---|
| Build button icon | Placeholder |
| Tile category icon | Placeholder |
| Decoration category icon | Placeholder |
| Building category icon | Placeholder |
| Plant category icon | Placeholder |
| Placement valid indicator | Placeholder |
| Placement invalid indicator | Placeholder |
| Rotate icon | Placeholder |
| Snap to Grid toggle icon | Placeholder |
| Move icon | Placeholder |
| Store icon | Placeholder |
| Item thumbnails | Menunggu katalog asset |

Setiap model yang dapat ditempatkan wajib menyediakan metadata PlacementProfile dan bounding volume. Skala, pivot, dan konfigurasi collision tiap asset harus mengikuti asset pipeline.

## 8. Analisis dampak

- **Dampak core loop:** Sangat langsung memperkuat loop dekorasi dan ekspresi personal. Pemain dapat bereksperimen tanpa kehilangan item saat membatalkan placement.
- **Source/sink ekonomi:** Build Mode tidak menciptakan Life Coin. Pembelian item/tile tetap menjadi sink pada sistem toko yang terpisah. Move dan Store tidak menghasilkan uang.
- **Risiko:**
  - Bounding volume yang tidak sesuai visual dapat membuat placement terasa terlalu ketat atau terlalu longgar.
  - Detail yang boleh overlap dapat menghasilkan clipping visual; tuning per asset diperlukan.
  - Multiplayer lock dan penyimpanan atomik menambah kompleksitas.
  - Aturan hak Build belum ditetapkan.
  - Surface placement dan Store tanaman belum termasuk v1.
- **Metrik sukses (target playtest awal, ASUMSI):**
  - ≥95% operasi Place/Move/Store yang valid berhasil tanpa inkonsistensi inventori/layout.
  - 0 kasus duplikasi item dari pengiriman operasi berulang.
  - ≥90% pemain uji dapat memasang objek pertama tanpa bantuan moderator.
  - Median waktu dari memilih item hingga berhasil Place ≤15 detik setelah pemain memahami kontrol.
  - 0 objek tersimpan di luar batas plot.

## 9. Kriteria selesai (acceptance criteria)

- [ ] Pemain dapat membuka Build Mode dan melihat kategori inventori.
- [ ] Pemain dapat memilih objek dan melihat placement preview.
- [ ] Farm Tile dan Build Tile mengikuti grid placement 5×5.
- [ ] Dekorasi, bangunan, dan tanaman mendukung free placement.
- [ ] Snap to Grid dapat diaktifkan dan dimatikan untuk objek free placement.
- [ ] Objek dapat diputar dalam interval 90°.
- [ ] GroundTile tidak dapat overlap dengan GroundTile lain.
- [ ] Solid tidak dapat overlap dengan Solid atau Detail.
- [ ] Detail dapat overlap dengan Detail tetapi tidak dengan Solid.
- [ ] GroundTile tidak memblokir penempatan Solid atau Detail.
- [ ] Preview di luar batas plot atau dengan collision tidak valid tidak dapat dikonfirmasi.
- [ ] Place mengurangi inventori tepat satu kali setelah server menyimpan objek.
- [ ] Move yang dibatalkan mempertahankan posisi dan rotasi objek asli.
- [ ] Store mengembalikan satu item ke inventori dan tidak memberikan Life Coin.
- [ ] Dua pemain tidak dapat mengubah objek yang sama secara bersamaan.
- [ ] Permintaan palsu atau tidak berizin ditolak server.
- [ ] Perubahan layout tetap tersimpan setelah pemain keluar dan masuk kembali.
- [ ] Tidak ada error di Output selama seluruh skenario pengujian.

## 10. Riwayat revisi

| Versi | Tanggal | Perubahan | Alasan |
|---|---|---|---|
| v1 | 2026-11-15 | Draft awal Build Mode, Hybrid Placement, dan Hybrid Collision | Merinci keputusan D-003, D-004, dan D-005 |
