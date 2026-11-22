# Master Release Plan: Garden Life First Release

**Status:** DRAFT — review pemilik diperlukan
**Scope:** Spring, Summer, Autumn, Winter
**Sumber:** PRD musim, GDD, DECISIONS.md, ROADMAP.md

## 1. PRD Musim

| Musim | Dokumen | Status desain |
|---|---|---|
| Spring | `docs/design/PRD_SPRING.md` | DRAFT |
| Summer | `docs/design/PRD_SUMMER.md` | DRAFT |
| Autumn | `docs/design/PRD_AUTUMN.md` | DRAFT |
| Winter | `docs/design/PRD_WINTER.md` | DRAFT |

Tidak ada dokumen yang dinaikkan ke `READY`.

## 2. Pola lintas musim

- Setiap musim berdurasi 30 hari in-game.
- Soft Transition berlangsung 3 hari dan preview musim berikutnya hanya visual.
- Cuaca dan Mutation hanya melakukan roll pada plot yang ditempati, kecuali aturan fasilitas yang eksplisit.
- Greenhouse memberi perlindungan dari efek cuaca dan Mutation cuaca, tetapi tanaman tetap membutuhkan air.
- Rest adalah status freeze tanaman, bukan kematian.
- Uprooted universal untuk Tornado, Storm, dan Blizzard; Trowel menanam ulang tanaman.
- Leafy Compost Bin universal untuk bahan tanaman mati; daun adalah bahan khusus Autumn.
- Variant dan Mutation tetap terpisah; batas Mutation buah adalah 15 unik.

## 3. Urutan dependensi implementasi

1. Fondasi kalender, server tick, plot active/empty, dan persistensi.
2. Farm Tile, tanaman, WaterLevel, pertumbuhan, panen, dan inventori.
3. Cuaca shared: Sunny, Cloudy, Windy, Drizzle, Rainy, Misty.
4. Rest, toleransi musim, Greenhouse, Season Pill, dan status pemulihan.
5. Mutation/Variant roll dan penyimpanan persisten.
6. Spring Thunderstorm dan perlindungan petir.
7. Summer Heatwave, rantai Tornado, Uprooted, dan Windblown.
8. Autumn Leaffall, Garden Rake, Leaf Basket, Blocked, dan Leafy Compost Bin.
9. Winter salju, Snow Shovel, Snow Block, Frozen, Blizzard, dan Heater.
10. UI, mobile/touch, server validation, exploit checks, performa, dan playtest.

## 4. Macro Check: status ekonomi

### Sudah tersedia

- Harga beli benih baseline: Common 100, Uncommon 500, Rare 2.500, Epic 10.000, Legendary 50.000, Mystic 250.000 Life Coin.
- Toko musim pada rancangan PRD dibatasi Common–Rare.
- Season Pill diarahkan 80% harga jual buah dewasa.
- Harga jual buah, Base Price, multiplier Mutation, multiplier Variant, harga pupuk, item, dan biaya bahan bakar belum final.
- Leafy Compost Bin mengubah daun/tanaman mati menjadi pupuk; tidak menghasilkan Life Coin langsung.

### Loop yang perlu diuji

| Loop | Risiko | Status |
|---|---|---|
| Leaffall → daun → kompos → pupuk | Produksi pupuk gratis mungkin mengurangi sink toko | Terbuka; butuh simulasi jumlah daun per episode |
| Tanaman mati → kompos | Pemain sengaja membiarkan tanaman mati demi Super Fertilizer | Terbuka; perlu bandingkan biaya kehilangan tanaman dan nilai pupuk |
| Snow Block → air | Bisa menjadi sumber air murah untuk mengatasi Flooded/Overwatered | Terbuka; perlu aturan konversi dan batas produksi |
| Kayu shop → Heater | Sink Life Coin belum punya harga | Terbuka |
| Pohon → kayu → Heater | Risiko loop bahan bakar tanpa batas atau eksploit penebangan | Terbuka; perlu cooldown, kapasitas, atau biaya tanam |
| Heater → perlindungan Frozen/Frosted | Dua Heater per plot bisa memudahkan Winter terlalu besar | Terbuka; perlu coverage overlap dan konsumsi final |
| Season Pill → bypass musim | Harga belum bisa diuji tanpa Base Price buah | Menunggu ekonomi buah |

## 5. Bug/inkonsistensi yang sudah ditemukan

- PRD Winter diselaraskan: Frozen = pertumbuhan 0× sesuai D-059.
- PRD Spring diselaraskan: Dormant diganti Rest.
- D-060 mengunci kapasitas 500 dan konsumsi 0,5 unit/tick. Dengan 1 tick = 30 detik, durasi penuh adalah 1.000 tick = 500 menit waktu aktif = 8 jam 20 menit real-time.
- Shared weather effects belum memiliki satu tabel pusat final; PRD tiap musim perlu dirujukkan ke tabel shared agar angka tidak bercabang.
- Frost dan Blizzard sama-sama dapat memberi status dingin; prioritas status, timer, dan interaksi Heater belum lengkap.

## 6. Pekerjaan setelah macro check

- Uji balancing Heater dengan baseline 8 jam 20 menit.
- Tetapkan satu tabel shared weather.
- Tetapkan konversi Snow Block → air.
- Tetapkan produksi daun per Leaffall dan kapasitas inventory.
- Buat Economy Ledger setelah Base Price buah dan multiplier disepakati.
- Buat/selaraskan Feature Spec DRAFT; jangan naikkan ke READY tanpa persetujuan pemilik.
- Tentukan Vertical Slice Scope sebelum implementasi.
