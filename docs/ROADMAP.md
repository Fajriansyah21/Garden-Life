# ROADMAP · Garden Life

**Status dokumen:** DRAFT untuk ditinjau pemilik  
**Versi:** 0.2  
**Tanggal dibuat:** 2026-11-15  
**Pemilik keputusan:** Pemilik proyek  
**Penyusun:** ChatGPT (Game Designer)

> Roadmap ini adalah peta kerja dan inventaris perancangan. Roadmap bukan persetujuan scope rilis, bukan komitmen tanggal, dan bukan instruksi implementasi. Hanya pemilik proyek yang dapat menyetujui prioritas, scope, dan perubahan arah. Semua hal yang belum disepakati tetap berstatus usulan atau BELUM DIPUTUSKAN.

## 1. Tujuan

**Arah visi yang disetujui (D-023):** Garden Life adalah Cozy Garden Life Simulator. Kebun pribadi menjadi ruang personal yang terus berkembang melalui dekorasi, koleksi tanaman unik, perawatan santai, dan kunjungan sosial. Farming mendukung perkembangan kebun, bukan menjadi satu-satunya tujuan. Roadmap mencakup visi jangka panjang hingga Live-ops, dengan pemisahan First Release, Post-Release, dan Long-Term Vision; pemisahan ini tidak otomatis menyetujui scope fitur.

Roadmap digunakan untuk:
1. Memetakan pekerjaan dari Discovery hingga Live-ops.
2. Memastikan seluruh sistem penting Garden Life teridentifikasi sebelum produksi.
3. Menunjukkan urutan dan dependensi antarsistem.
4. Memisahkan visi jangka panjang dari scope rilis pertama dan Vertical Slice.
5. Menjadi checklist kemajuan yang konsisten untuk pemilik, ChatGPT, dan Claude.
6. Mencegah fitur baru masuk ke produksi tanpa prioritas, analisis, spec, dan persetujuan.

## 2. Prinsip pengelolaan Roadmap

- Repo GitHub adalah sumber kebenaran.
- Keputusan desain aktif harus merujuk docs/DECISIONS.md; Roadmap tidak menggantikan atau mengubah keputusan.
- GDD menjelaskan visi dan aturan tingkat tinggi; Feature Spec menjelaskan aturan implementasi yang dapat diuji.
- Semua angka tuning harus berada di GDD atau tabel spec yang relevan, bukan tersebar di catatan Roadmap.
- Status spec mengikuti docs/00_WORKFLOW.md: DRAFT -> READY -> IN_PROGRESS -> IMPLEMENTED -> VERIFIED. Hanya pemilik yang mengubah DRAFT menjadi READY.
- Roadmap boleh memuat ide masa depan, tetapi ide tersebut tidak otomatis menjadi scope.
- Fitur di luar fase aktif tidak boleh dikerjakan sebelum disetujui pemilik.
- Setiap fitur harus dianalisis terhadap core loop, ekonomi, risiko, biaya implementasi (dikonfirmasi Claude), dan metrik sukses sesuai docs/01_DESIGN_ANALYSIS_SYSTEM.md.
- Semua sistem harus mempertimbangkan PC dan perangkat sentuh, server-authoritative, persistence, keamanan, serta performa sesuai relevansinya.

## 3. Status proyek saat Roadmap dibuat

| Elemen | Status |
|---|---|
| Fase | Fase 0 Discovery, menuju Fase 1 Konsep & GDD |
| GDD | v1.6 |
| Gameplay | Belum ada implementasi |
| FEAT-001 Build Mode | DRAFT |
| FEAT-002 Tools & Perawatan Tanaman | DRAFT, v11 |
| Keputusan desain | D-001 sampai D-023 |
| Spec READY | Belum ada |
| Vertical Slice | Scope belum ditetapkan |
| Tanggal rilis | Belum ditetapkan |

## 4. Roadmap fase proyek

Fase mengikuti docs/00_WORKFLOW.md. Rincian di bawah memperjelas pekerjaan dan gerbang kelulusannya, bukan mengganti workflow yang sudah berlaku.

### Fase 0 · Discovery

**Tujuan:** memastikan identitas dan arah produk.

Pekerjaan:
- [x] Visi dan pitch Garden Life, termasuk identitas jangka panjang Cozy Garden Life Simulator (D-023).
- [x] Genre dan pilar desain.
- [ ] Menentukan target pemain yang lebih spesifik.
- [ ] Menentukan tiga game referensi dan pelajaran desain dari masing-masing.
- [ ] Menetapkan konteks perangkat prioritas dan karakteristik sesi pemain.
- [ ] Meninjau batasan proyek dan risiko utama.

**Exit criteria:**
- Visi satu paragraf disetujui.
- Target pemain ditulis dengan jelas.
- Tiga referensi game disepakati dan dianalisis.
- Batasan produk dan prinsip desain dipahami bersama.

### Fase 1 · Konsep & GDD

**Tujuan:** mendefinisikan pengalaman, sistem, dan scope sebelum implementasi.

Pekerjaan:
- [ ] Melengkapi player journey dari pemain baru hingga progres jangka panjang.
- [ ] Memastikan core loop utama dan loop pendukung.
- [ ] Menetapkan pengalaman 5 menit pertama sebagai rancangan yang dapat diuji.
- [ ] Memetakan seluruh sistem pada Master System Checklist (bagian 5).
- [ ] Menentukan prioritas MoSCoW berdasarkan visi dan analisis dampak/biaya.
- [ ] Menetapkan sumber dan penguras Life Coin tingkat tinggi.
- [ ] Mengidentifikasi dependensi dan risiko antarsistem.
- [ ] Menentukan scope Vertical Slice dan kriteria kelulusannya.
- [ ] Menautkan setiap sistem yang disetujui ke GDD, Decision Log, atau Feature Spec yang relevan.

**Exit criteria:**
- GDD lengkap untuk scope yang disetujui.
- Semua sistem memiliki prioritas atau status eksplisit (di luar scope/masa depan/belum diputuskan).
- Scope Vertical Slice disetujui pemilik.
- Dependensi kritis dan risiko utama tercatat.
- Tidak ada aturan penting Vertical Slice yang hanya tersimpan di percakapan.

### Fase 2 · Vertical Slice

**Tujuan:** membuktikan bahwa satu bagian kecil Garden Life sudah menyenangkan dan berjalan utuh.

**Kandidat loop berdasarkan workflow saat ini:**
1. Pemain masuk dan memperoleh akses ke plot.
2. Pemain menerima Starter Kit sesuai keputusan aktif.
3. Pemain memperoleh atau menempatkan area tanam.
4. Pemain menanam bibit.
5. Tanaman tumbuh berdasarkan aturan yang ditetapkan.
6. Pemain memanen.
7. Pemain menjual hasil panen.
8. Pemain menggunakan Life Coin untuk membeli bibit kembali.

**Usulan tambahan untuk diuji:** satu interaksi dekorasi sederhana agar Vertical Slice juga menguji identitas dekorasi-first Garden Life. Ini belum menjadi keputusan scope.

Pekerjaan pendukung:
- [ ] Spec Vertical Slice disetujui sebelum implementasi.
- [ ] Alur save/load minimum dan pemulihan kegagalan data diuji.
- [ ] Validasi server untuk uang, inventori, pertumbuhan, dan hasil panen.
- [ ] UI minimum untuk PC dan perangkat sentuh.
- [ ] Checklist pengujian manual dan kasus exploit.

**Exit criteria:**
- Satu loop lengkap dapat dimainkan dari awal sampai akhir.
- Tidak ada bug fatal atau kehilangan progres pada skenario uji utama.
- Transaksi dan hasil bernilai divalidasi server.
- UI minimum dapat digunakan pada perangkat target.
- Pemilik menyetujui hasil uji Vertical Slice.

### Fase 3 · Produksi

**Tujuan:** membangun fitur yang telah diprioritaskan dan disetujui.

Pekerjaan:
- [ ] Mengembangkan fitur berdasarkan prioritas dan dependensi.
- [ ] Setiap fitur memiliki spec DRAFT yang ditinjau dan disetujui pemilik.
- [ ] Claude mengimplementasikan hanya spec READY.
- [ ] Setiap implementasi memiliki checklist tes.
- [ ] Pemilik melakukan verifikasi dan hanya fitur lolos yang menjadi VERIFIED.
- [ ] Integrasi antarsistem dan migrasi data diuji.

**Exit criteria:** seluruh fitur MUST untuk scope rilis telah VERIFIED; fitur SHOULD/COULD ditangani sesuai keputusan scope dan kapasitas.

### Fase 4 · Playtest & Analisis

**Tujuan:** mengetahui apakah game benar-benar mudah dipahami, menyenangkan, dan stabil bagi pemain.

Pekerjaan:
- [ ] Menyusun skenario playtest solo dan multiplayer.
- [ ] Menguji PC dan perangkat sentuh.
- [ ] Mengamati onboarding dan waktu menuju aktivitas bermakna pertama.
- [ ] Mencatat titik kebingungan, frustrasi, dan drop-off.
- [ ] Mengukur metrik yang tersedia secara sah dan sesuai privasi.
- [ ] Membuat laporan analisis dan daftar perbaikan.

**Exit criteria:** laporan playtest terdokumentasi, temuan diprioritaskan, dan keputusan tindak lanjut dibuat.

### Fase 5 · Balancing & Polish

**Tujuan:** menyelaraskan ekonomi, progres, usability, performa, dan kualitas presentasi.

Pekerjaan:
- [ ] Simulasi ekonomi dan progres berdasarkan data tuning.
- [ ] Menguji strategi pemain aktif dan pemain santai.
- [ ] Memeriksa inflasi, sink/source, dan nilai koleksi.
- [ ] Menyempurnakan UI, feedback, animasi, efek, audio, dan ambience.
- [ ] Menguji performa pada perangkat rendah.
- [ ] Memperbaiki bug dan regresi.

**Exit criteria:** target metrik yang disetujui tercapai atau penyimpangan memiliki keputusan tertulis; masalah kritis terselesaikan.

### Fase 6 · Rilis

**Tujuan:** menyiapkan build publik yang aman dan layak dimainkan.

Pekerjaan:
- [ ] Finalisasi map, asset, dan manifest.
- [ ] Checklist keamanan, DataStore, kapasitas server, dan pemulihan.
- [ ] Finalisasi ikon, thumbnail, deskripsi, dan metadata Roblox.
- [ ] Meninjau monetisasi dan fairness free-to-play.
- [ ] Melakukan uji build kandidat rilis.
- [ ] Menyiapkan rencana rollback dan dukungan awal.

**Exit criteria:** checklist rilis disetujui pemilik dan game dipublikasikan.

### Fase 7 · Live-ops

**Tujuan:** menjaga game tetap sehat dan berkembang setelah rilis.

Pekerjaan:
- [ ] Mengelola backlog update berdasarkan feedback dan data.
- [ ] Menjadwalkan konten dan event dengan scope yang realistis.
- [ ] Memantau bug, ekonomi, retensi, dan performa.
- [ ] Menguji update sebelum dipublikasikan.
- [ ] Mencatat hasil tiap update untuk keputusan berikutnya.

**Exit criteria:** tersedia siklus update dan evaluasi berkala. Workflow saat ini menyarankan backlog update per 2-4 minggu; frekuensi aktual tetap mengikuti kapasitas dan keputusan pemilik.

## 5. Master System Checklist

Daftar ini adalah inventaris area desain, bukan daftar fitur yang otomatis wajib masuk rilis pertama. Status awal selain yang sudah memiliki dokumen dicatat sebagai NOT_STARTED atau EXPLORING.

| ID | Area sistem | Cakupan yang perlu dirancang | Status awal |
|---|---|---|---|
| SYS-01 | Identitas & pengalaman | Target pemain, referensi, player journey, panjang sesi, fantasi pemain | EXPLORING |
| SYS-02 | Onboarding | Tutorial, pengenalan plot, Starter Kit, panduan awal, skip/return flow | NOT_STARTED |
| SYS-03 | World & Map | Dunia utama, area publik, navigasi, lingkungan, interaksi map | NOT_STARTED |
| SYS-04 | Plot | Kepemilikan, kapasitas, assignment, ekspansi, persistensi, transfer Active Owner | EXPLORING |
| SYS-05 | Build Mode | Placement, preview, rotasi, collision, move, store, batas objek, validasi | DRAFT |
| SYS-06 | Dekorasi & bangunan | Kategori, koleksi, rarity, variasi, sumber perolehan, batas placement | NOT_STARTED |
| SYS-07 | Farming loop | Farm Tile, penanaman, pertumbuhan, panen, interaksi tanaman | EXPLORING |
| SYS-08 | Data tanaman & benih | Daftar tanaman, seed, level unlock, waktu tumbuh, yield, musim, data tanaman | NOT_STARTED |
| SYS-09 | Perawatan tanaman | WaterLevel, toleransi, Overwatered, pengeringan, kebutuhan air | DRAFT |
| SYS-10 | Tools | Fungsi, konsumsi, cooldown, radius, target, upgrade, interaksi | DRAFT |
| SYS-11 | Buah & hasil panen | Tahap buah, ukuran, kualitas, jumlah, Base Price, penyimpanan dan penjualan | EXPLORING |
| SYS-12 | Variant | Variant yang tersedia, rarity, kondisi, peluang, tampilan, multiplier | EXPLORING |
| SYS-13 | Mutation | Jenis, multiplier, peluang, kondisi, efek, stacking dan visual | EXPLORING |
| SYS-14 | Musim | Kalender dunia, durasi, transisi, perubahan map, aktivitas musiman | EXPLORING |
| SYS-15 | Cuaca | Jenis cuaca, pola, peluang, dampak lingkungan dan tanaman | EXPLORING |
| SYS-16 | Tanaman langka | Spawn di plot/map, kondisi khusus, batas spawn, musim, benih dan persistensi | EXPLORING |
| SYS-17 | Ekonomi | Life Coin, source/sink, harga, transaksi, balancing dan anti-inflasi | NOT_STARTED |
| SYS-18 | Toko | Kategori barang, stok, unlock, rotasi stok bila ada, transaksi dan UI | NOT_STARTED |
| SYS-19 | Progres | Level, XP, unlock, milestone, upgrade plot dan pacing | NOT_STARTED |
| SYS-20 | Inventori | Kategori item, kapasitas, stack, penyimpanan, pemindahan, overflow | NOT_STARTED |
| SYS-21 | Multiplayer & izin | Invite, peran, hak akses, konflik edit, disconnect dan transfer kendali | EXPLORING |
| SYS-22 | Shared Savings | Pembuatan, akses, deposit, penarikan, spending limit, audit transaksi | EXPLORING |
| SYS-23 | Sosial | Kunjungan, interaksi, kolaborasi, aktivitas bersama dan moderasi | NOT_STARTED |
| SYS-24 | UI/UX | HUD, menu, inventory, shop, notifikasi, build UI, mobile/touch | EXPLORING |
| SYS-25 | Audio & presentasi visual | Animasi, VFX, SFX, ambience, musik, feedback interaksi | NOT_STARTED |
| SYS-26 | Data & keamanan | DataStore, save/load, session lock, schema migration, server validation, exploit prevention | EXPLORING |
| SYS-27 | Performa & skalabilitas | Batas instance, update tanaman, server load, streaming, perangkat rendah | NOT_STARTED |
| SYS-28 | Monetisasi | Game Pass, Developer Product, fairness free-to-play, batas pay-to-win | NOT_STARTED |
| SYS-29 | Analytics | Event analytics, retensi, sesi, penggunaan fitur, ekonomi, privasi | NOT_STARTED |
| SYS-30 | Live-ops | Event, update, konten baru, feedback, cadence dan evaluasi | NOT_STARTED |

**Catatan status:**
- Status di tabel adalah kemajuan perancangan, bukan status implementasi.
- SYS-05 terkait FEAT-001; SYS-09 dan SYS-10 terkait FEAT-002. Keduanya masih DRAFT.
- SYS-12 dan SYS-13 memiliki keputusan tingkat tinggi D-022, tetapi detail individual belum lengkap.
- Status harus diperbarui ketika dokumen atau spec terkait berubah.

## 6. Dependensi dan urutan desain

Urutan berikut adalah rekomendasi dependensi. Pekerjaan dapat berjalan paralel jika input yang dibutuhkan sudah tersedia dan tidak menciptakan keputusan yang bertentangan.

| Kelompok | Sistem utama | Input/dependensi penting | Output yang diharapkan |
|---|---|---|---|
| A. Fondasi pengalaman | SYS-01, SYS-02 | Visi, target pemain, referensi | Player journey, onboarding, core loop |
| B. Dunia & kreativitas | SYS-03, SYS-04, SYS-05, SYS-06 | Fondasi pengalaman, aturan plot | Dunia, plot, Build Mode, katalog dekorasi |
| C. Farming | SYS-07, SYS-08, SYS-09, SYS-10, SYS-11 | Core loop, data tanaman, alat | Loop tanam-rawat-panen dan data hasil |
| D. Ekonomi & progres | SYS-17, SYS-18, SYS-19, SYS-20 | Yield, Base Price, biaya item, inventory | Sink/source, toko, progres, kapasitas inventori |
| E. Koleksi khusus & dunia dinamis | SYS-12, SYS-13, SYS-14, SYS-15, SYS-16 | Buah, harga dasar, kalender, cuaca | Variant, Mutation, musim, cuaca, rare plants |
| F. Sosial & kolaborasi | SYS-21, SYS-22, SYS-23 | Plot, kepemilikan, inventori, ekonomi | Co-op, izin, bank bersama, fitur sosial |
| G. Integrasi & kesiapan rilis | SYS-24 sampai SYS-30 | Sistem yang telah diprioritaskan | UI, asset, data, keamanan, performa, monetisasi, analytics, live-ops |

**Dependensi kritis:**
1. Harga jual buah memerlukan definisi hasil panen, Base Price, Variant, dan Mutation.
2. Balancing ekonomi memerlukan sumber pendapatan dan seluruh penguras utama yang masuk scope.
3. Seasonal Variant dan tanaman langka memerlukan kalender musim, aturan transisi, dan kondisi spawn.
4. Multiplayer aman memerlukan kepemilikan objek, role permission, validasi server, dan aturan konflik.
5. UI final memerlukan perilaku sistem yang cukup stabil; wireframe dapat dibuat lebih awal.
6. Produksi memerlukan aturan save/load, schema versioning, dan pemulihan kegagalan data.

## 7. Prioritas dan pemisahan scope

Prioritas MoSCoW ditetapkan setelah Fase 1 dianalisis. Tabel ini sengaja belum menetapkan SYS-01 sampai SYS-30 sebagai Must/Should/Could/Won't.

| Kategori | Arti | Aturan |
|---|---|---|
| MUST | Wajib untuk target rilis yang disetujui | Tidak boleh rilis tanpa terpenuhi |
| SHOULD | Sangat bernilai, tetapi masih mungkin ditunda | Perlu alasan tertulis jika ditunda |
| COULD | Nilai tambah jika kapasitas tersedia | Tidak menghambat rilis |
| WON'T (this release) | Sengaja tidak masuk rilis ini | Boleh masuk backlog masa depan |

Scope dibagi menjadi:
- **Vertical Slice:** subset minimum untuk membuktikan core loop; harus disetujui terpisah.
- **First Release:** kumpulan fitur yang memenuhi visi dan kriteria rilis pertama; belum ditentukan.
- **Future / Live-ops:** fitur tambahan setelah rilis; tidak otomatis menjadi komitmen.

## 8. Checklist lintas sistem

Checklist berikut harus diperiksa pada sistem yang relevan sebelum spec READY atau sebelum rilis.

### Pengalaman pemain
- [ ] Tujuan pemain dan hasil interaksi jelas.
- [ ] Pemain baru memahami tindakan berikutnya.
- [ ] Fitur mendukung identitas cozy/dekorasi-first.
- [ ] Tidak menciptakan kewajiban login atau tekanan yang tidak disengaja.
- [ ] Perilaku saat pemain pergi dan kembali telah ditentukan.

### Ekonomi
- [ ] Source dan sink dicatat.
- [ ] Dampak terhadap harga, pendapatan, dan progres dianalisis.
- [ ] Risiko exploit, duplikasi, dan inflasi diperiksa.
- [ ] Angka tuning berada dalam tabel spec.
- [ ] Nilai belum tervalidasi ditandai ASUMSI.

### Multiplayer & keamanan
- [ ] Hak akses dan kepemilikan objek jelas.
- [ ] Aksi bersamaan memiliki aturan konflik.
- [ ] Server memvalidasi uang, inventori, hasil, dan perubahan state.
- [ ] Remote divalidasi terhadap tipe, jarak, cooldown, rate limit, dan izin.
- [ ] Disconnect, server shutdown, dan rejoin ditangani.

### Data & persistensi
- [ ] Data yang disimpan dan sumber kebenarannya jelas.
- [ ] Save/load dan kegagalan DataStore ditangani.
- [ ] Perubahan schema memiliki strategi migrasi.
- [ ] Progres tidak hilang saat plot unload atau pemain berpindah server.
- [ ] Item/objek yang sedang diproses tidak dapat diduplikasi.

### UI, aksesibilitas, dan performa
- [ ] UI mendukung mouse dan layar sentuh.
- [ ] Feedback aksi berhasil/gagal jelas.
- [ ] UI tidak menutupi objek penting.
- [ ] Jumlah Instance dan update berkala memiliki batas.
- [ ] Pengujian dilakukan pada perangkat dengan performa rendah.

### Konten & asset
- [ ] Kebutuhan asset dicatat di spec.
- [ ] Asset memiliki nama dan status manifest.
- [ ] Sumber dan lisensi asset jelas.
- [ ] Placeholder tersedia jika asset final belum siap.
- [ ] Asset memiliki skala, pivot, collision, dan placement profile bila relevan.

## 9. Risk Register awal

Risiko berikut adalah identifikasi awal, bukan klaim bahwa masalah telah terjadi.

| ID | Risiko | Dampak potensial | Mitigasi / pekerjaan |
|---|---|---|---|
| R-01 | Scope melebar sebelum Vertical Slice | Waktu produksi meningkat, core loop belum terbukti | Kunci scope fase dan gunakan MoSCoW |
| R-02 | Dekorasi-first tidak tercermin di pengalaman awal | Game terasa seperti farming simulator biasa | Uji ekspresi dekorasi sejak onboarding/Vertical Slice |
| R-03 | Ekonomi belum memiliki source/sink lengkap | Inflasi atau pemain kehabisan tujuan belanja | Buat ledger source/sink dan simulasi |
| R-04 | Sistem Variant/Mutation kompleks | Harga dan visual sulit dipahami atau dieksploitasi | Definisikan satu per satu dan uji kombinasi |
| R-05 | Kalender dan rare plant belum lengkap | Pemain kehilangan akses atau merasa dihukum saat pergantian musim | Tetapkan spawn, persistensi, dan transisi musim |
| R-06 | Build Mode dan dekorasi berat pada perangkat rendah | FPS turun dan pengalaman mobile buruk | Tetapkan batas objek dan uji performa |
| R-07 | Konflik multiplayer pada objek/data bersama | Duplikasi, kehilangan item, atau perubahan tidak sah | Server authority, izin, locking/serialisasi aksi |
| R-08 | DataStore gagal atau schema berubah | Kehilangan progres | Session lock, retry, versioning, migrasi, uji pemulihan |
| R-09 | Onboarding terlalu padat | Pemain baru bingung dan keluar | Player journey, tutorial bertahap, playtest |
| R-10 | Fitur offline menimbulkan tekanan | Pemain merasa wajib login untuk menyelamatkan progres | Hindari penalti offline yang tidak sejalan dengan pilar cozy |

## 10. Dokumen dan artefak yang perlu dibuat

| Artefak | Lokasi yang disarankan | Tujuan | Status |
|---|---|---|---|
| Roadmap utama | docs/ROADMAP.md | Peta fase, sistem, dependensi, risiko | DRAFT |
| GDD | docs/02_GAME_DESIGN_DOCUMENT.md | Visi dan aturan tingkat tinggi | v1.5 |
| Decision Log | docs/DECISIONS.md | Keputusan pemilik yang disetujui | D-001–D-022 |
| Player Journey | docs/design/PLAYER_JOURNEY.md | Pengalaman pemain dari awal hingga progres lanjut | Belum dibuat |
| Economy Ledger | docs/design/ECONOMY_LEDGER.md | Semua source, sink, dan aliran Life Coin | Belum dibuat |
| Vertical Slice Scope | docs/design/VERTICAL_SLICE_SCOPE.md | Batas fitur dan acceptance criteria Vertical Slice | Belum dibuat |
| Risk Register | Bagian 9 dokumen ini; dapat dipisah nanti | Risiko dan mitigasi | DRAFT |
| Feature Specs | docs/design/FEAT-XXX_*.md | Aturan implementasi per fitur | FEAT-001/002 DRAFT |
| Asset Manifest | assets/ASSET_MANIFEST.md | ID, lisensi, dan status asset | Belum dibuat |
| Test checklist | tests/FEAT-XXX_checklist.md | Verifikasi tiap fitur | Belum dibuat |

Lokasi dan pemisahan dokumen dapat disesuaikan pemilik. Jangan membuat dokumen tambahan hanya untuk memecah isi tanpa manfaat yang jelas.

## 11. Pertanyaan terbuka untuk pemilik

Pertanyaan berikut harus dibahas sebelum Roadmap dianggap final. Tidak ada jawaban yang diasumsikan dari dokumen ini.

1. **Terjawab (15 November 2026):** Roadmap mencakup seluruh visi hingga Live-ops dan pengembangan jangka panjang. Pembagian First Release, Post-Release, dan Long-Term Vision digunakan untuk memisahkan horizon scope.
2. Apakah Vertical Slice menguji farming saja, atau farming sekaligus satu interaksi dekorasi dasar?
3. Seberapa rinci Roadmap perlu mengatur urutan pekerjaan: fase/sistem saja, atau sampai estimasi implementasi?
4. Apa target pemain yang lebih spesifik dan tiga game referensi yang disepakati?
5. Apa batas scope rilis pertama dan fitur yang sengaja ditunda?
6. Bagaimana target pengalaman 5 menit pertama diukur?
7. Sistem mana yang benar-benar MUST untuk rilis pertama?

## 12. Aturan pembaruan Roadmap

- Perbarui status hanya setelah ada bukti dokumen, persetujuan, implementasi, atau verifikasi.
- Jangan mengubah keputusan aktif secara diam-diam; perubahan keputusan harus dicatat sebagai entri baru di DECISIONS.md.
- Perubahan scope harus menyebut alasan, dampak dependensi, risiko, dan dokumen yang perlu diselaraskan.
- Roadmap tidak boleh menaikkan status Feature Spec menjadi READY.
- Setiap sesi desain yang mengubah status Roadmap harus menambahkan catatan ringkas di HANDOFF.md.
- Review Roadmap pada akhir setiap fase dan ketika ada perubahan besar yang disetujui.

## 13. Riwayat revisi

| Versi | Tanggal | Perubahan | Status |
|---|---|---|---|
| v0.2 | 2026-11-15 | Mencatat visi Cozy Garden Life Simulator (D-023), cakupan Roadmap hingga jangka panjang, dan status pertanyaan cakupan Roadmap | DRAFT |
| v0.1 | 2026-11-15 | Draft awal fase proyek, 30 area sistem, dependensi, checklist lintas sistem, risiko, dan pertanyaan terbuka | DRAFT |
