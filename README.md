# Garden Life

**Garden Life** adalah **Cozy Garden Life Simulator** di Roblox. Pemain membangun, merawat, dan mendekorasi kebun pribadi yang terus berkembang, mengoleksi tanaman unik, serta mengunjungi kebun teman. Kreativitas dan ekspresi personal menjadi pusat pengalaman; farming, progres, dan ekonomi ringan menjadi aktivitas pendukung, bukan tujuan tunggal.

> **Prinsip sumber kebenaran:** keputusan desain yang sudah disetujui harus tercatat di repo. Ide yang belum disetujui atau belum memiliki aturan lengkap harus ditandai sebagai usulan, asumsi, atau belum diputuskan.

## Identitas game

| Elemen | Rancangan |
|---|---|
| Nama game / map | **Garden Life** |
| Platform | Roblox |
| Genre / pengalaman | Cozy Garden Life Simulator: garden building, decorating, light farming, social co-op |
| Fokus utama | Kebun pribadi sebagai ruang personal yang terus berkembang; dekorasi, ekspresi, koleksi tanaman, dan perawatan santai |
| Prioritas pengalaman | Dekorasi & ekspresi personal > sosial/co-op > farming santai > manajemen dan ekonomi ringan |
| Mode bermain | Solo dan multiplayer dalam plot bersama |
| Mata uang | **Life Coin** |
| Identitas mata uang | Koin emas dengan ikon daun |
| Saldo awal pribadi | **1.000 Life Coin** |
| Item awal | Starter Kit gratis: perlengkapan farming dan dua dekorasi (D-009, D-010) |

## Pilar desain

1. **Kreativitas tanpa tekanan.** Pemain bebas menyusun kebun dan mengekspresikan gaya masing-masing.
2. **Kebun sebagai ruang personal.** Plot tetap terikat pada Original Owner dan progres layout disimpan.
3. **Kolaborasi yang aman.** Teman dapat membantu membangun, dengan hak yang dibedakan berdasarkan peran dan kepemilikan objek.
4. **Farming sebagai pendukung.** Menanam, merawat, dan memanen memberi aktivitas serta potensi sumber Life Coin, tetapi tidak mengambil alih fokus dekorasi.
5. **Ekonomi ringan.** Life Coin digunakan untuk membeli tile, dekorasi, tanaman, ekspansi, dan upgrade setelah harga serta sumber pendapatan ditetapkan dalam spec.

## Fondasi dunia dan plot

- Satu server menyediakan **4 plot persisten**.
- Setiap plot memiliki **Original Owner** (pemilik permanen) dan **Active Owner** (pemegang kendali aktif).
- Kapasitas awal plot adalah **2 pemain**, dapat ditingkatkan hingga **3 pemain**.
- Pemain yang menerima undangan berpindah dari plot asalnya ke plot pengundang; plot asalnya menjadi tersedia kembali.
- Jika Active Owner terputus, kendali berpindah ke anggota lain. Saat Original Owner kembali, kendali kembali kepadanya. Urutan pemilihan pengganti masih belum diputuskan.
- Ukuran plot:
  
  | Stage | Ukuran |
  |---|---:|
  | 1 | 80 × 80 studs |
  | 2 | 160 × 160 studs |
  | 3 | 240 × 240 studs |
  | 4 | 320 × 320 studs |

- Setiap upgrade stage memperluas area **40 studs ke kiri, 40 studs ke kanan, 80 studs ke belakang, dan 0 studs ke depan**. Objek yang sudah ditempatkan tidak bergeser.

## Fondasi Build Mode

- Farm Tile dan Build Tile ditempatkan dengan grid.
- Satu sel grid berukuran **4 × 4 studs**.
- Satu tile terdiri dari **5 × 5 sel grid**, sehingga footprint tile adalah **20 × 20 studs**.
- Dekorasi, bangunan, dan tanaman menggunakan free placement dan tidak wajib berada di atas tile.
- Snap to Grid tersedia sebagai opsi untuk objek free placement.
- Rotasi menggunakan interval **90°**.
- Sistem tabrakan memakai Hybrid Collision:
  - GroundTile tidak boleh overlap dengan GroundTile lain dan tidak memblokir objek di atasnya.
  - Solid tidak boleh overlap dengan Solid atau Detail.
  - Detail boleh overlap dengan Detail lain, tetapi tidak boleh overlap dengan Solid.
- Hak Build:
  - Original Owner dan Active Owner dapat Place, Move, dan Store seluruh objek di plot.
  - Anggota dapat Place dari inventori sendiri dan hanya Move/Store objek miliknya sendiri.
  - Anggota tidak dapat mengelola hak anggota plot.

## Ekonomi dan Shared Savings

- Life Coin pribadi terpisah dari **Shared Savings**, yaitu saldo bersama milik plot.
- Anggota yang sudah berada di plot saat Shared Savings dibuat mendapat akses otomatis.
- Anggota yang bergabung setelah Shared Savings dibuat membayar biaya administrasi **5.000 Life Coin** dan memerlukan persetujuan Original Owner.
- Spending Limit berlaku mingguan untuk pembelian yang menggunakan Shared Savings. Original Owner dapat mengubah atau menghapus batas tersebut (Unlimited).
- Biaya pembuatan Shared Savings, sumber pendapatan, harga item, dan aturan transaksi lainnya masih belum diputuskan. Biaya akses 5.000 Life Coin bukan biaya pembuatan Shared Savings.

## Batas scope yang perlu dijaga

Greenhouse (kapasitas 18 tanaman), 4 musim, siklus cuaca, dan dua tier pupuk ditargetkan masuk First Release melalui keputusan desain. Detail implementasi, ekonomi, dan spec fitur tetap belum otomatis siap dikerjakan. 5 tier pupuk, Watering Can 100 ml, dan gudang bersama tetap konsep terbuka. Scope Vertical Slice masih perlu ditentukan.

## Status proyek

- Fase: **1 Konsep & GDD**.
- Gameplay: belum ada implementasi.
- GDD: v3.45 (2026-11-27).
- Build Mode: `FEAT-001`, status `DRAFT`.
- Tools & Perawatan Tanaman: `FEAT-002`, status `DRAFT` (v12).
- Log keputusan: D-001 sampai D-094. Balancing ekonomi tanaman terbaru: Common D-065, Uncommon D-076, Rare D-077/D-080, Epic D-079/D-080, Legendary D-082, Mystic D-083. Kalender global dan siklus spawn buah dicatat pada D-085; sumber Mutation Wet, penghapusan jalur Flooded dari WaterLevel tinggi, dan aturan evolusi Wet yang digantikan Flooded dicatat pada D-086/D-087/D-088; identitas Foggy sebagai buah tertutup kabut tebal dicatat pada D-091 dan nama Mutation Hazy untuk cuaca Misty dicatat pada D-092; identitas Shocked sebagai dampak listrik langsung dan Charged sebagai energi tersimpan dicatat pada D-093; aturan urutan evaluasi roll Wet dan Flooded pada tick yang sama, peluang baseline per tick, serta multiplier Mutation Spring dan Variant dicatat pada D-094; titik epoch kalender ditetapkan sebelum launch. Roster reguler kini 21 tanaman setelah Starfruit ditambahkan melalui D-081. D-066 adalah riwayat provisional Uncommon dan telah digantikan D-076.
- Tidak ada spec yang berstatus `READY`; hanya pemilik yang dapat menyetujui status tersebut.

## Dokumen utama

| Dokumen | Fungsi |
|---|---|
| [Roadmap](docs/ROADMAP.md) | Peta fase proyek, master system checklist, dependensi, risiko, dan scope yang masih terbuka |
| [GDD](docs/02_GAME_DESIGN_DOCUMENT.md) | Visi, core loop, sistem, ekonomi, dunia, dan scope |
| [Player Journey](docs/design/PLAYER_JOURNEY.md) | Perjalanan pengalaman pemain dari First Visit hingga Established Garden |
| [DECISIONS](docs/DECISIONS.md) | Log keputusan yang disetujui; hanya ditambah, tidak menghapus |
| [HANDOFF](docs/HANDOFF.md) | Status kerja dan serah-terima ChatGPT ↔ Claude |
| [Concept Backlog](docs/design/CONCEPT_BACKLOG.md) | Ide terdahulu, status, dan pertanyaan desain |
| [PRD Spring](docs/design/PRD_SPRING.md) | Draft kebutuhan produk Spring untuk First Release; belum disetujui |
| [FEAT-001 Build Mode](docs/design/FEAT-001_build_mode.md) | Spec Build Mode dan Hybrid Placement |
| [Workflow](docs/00_WORKFLOW.md) | Alur persetujuan, implementasi, dan verifikasi |
| [Design Analysis System](docs/01_DESIGN_ANALYSIS_SYSTEM.md) | Kerangka analisis desain dan ekonomi |
| [Feature Spec Template](docs/design/_TEMPLATE_FEATURE_SPEC.md) | Format standar spec fitur |

## Pembagian peran

| Peran | Penanggung jawab | Tugas |
|---|---|---|
| Pemilik / Producer | Pemilik proyek | Menentukan arah, menyetujui keputusan dan spec, menguji game |
| Game Designer | ChatGPT | GDD, keputusan desain yang diusulkan, spec, balancing, analisis |
| Engineer | Claude | Implementasi Luau, arsitektur teknis, pengujian kode, dan laporan hambatan |

**Aturan kerja:** ChatGPT hanya menyetel spec ke `DRAFT`. Pemilik mengubahnya ke `READY` setelah menyetujui. Claude mengimplementasikan spec yang `READY` dan tidak menebak aturan yang belum diputuskan.

## Struktur repo

```
Garden-Life/
├── README.md
├── default.project.json
├── docs/
│   ├── ai/
│   ├── 00_WORKFLOW.md
│   ├── 01_DESIGN_ANALYSIS_SYSTEM.md
│   ├── 02_GAME_DESIGN_DOCUMENT.md
│   ├── 03_TECH_ARCHITECTURE.md
│   ├── 04_ASSET_PIPELINE.md
│   ├── DECISIONS.md
│   ├── HANDOFF.md
│   ├── design/
│   └── specs/
├── src/
│   ├── server/
│   ├── client/
│   └── shared/
├── assets/
├── maps/
├── tests/
└── tools/
```

## Tools

- Luau untuk implementasi Roblox.
- Git/GitHub untuk version control dan dokumentasi bersama.
