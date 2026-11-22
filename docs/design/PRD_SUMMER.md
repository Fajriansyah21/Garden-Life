# PRD: Musim Summer (Garden Life - First Release)

## 1. Tujuan
Musim Summer berlangsung 30 hari in-game (180 jam real-time). Fokus pada manajemen panas, siklus cuaca ekstrem, dan perlindungan tanaman.

## 2. Kalender & Musim
- Durasi: 30 hari in-game.
- Transisi: Soft Transition 3 hari (Hari 28–30) dengan preview visual 20% cuaca musim Autumn. Tanaman freeze jika tidak cocok dengan musim aktif.
- Greenhouse: kapasitas 18 slot, kebal cuaca dan Mutation cuaca, tetap butuh air.

## 3. Roster Cuaca Normal Summer
| Cuaca | Bobot | Durasi | Efek Utama |
|---|---:|---|---|
| Sunny | 40 | 20 menit | Normal |
| Cloudy | 20 | 10 menit | WaterLevel awal, penalti tanaman high-sunlight |
| Windy | 15 | 10 menit | Pengeringan tanah, pertumbuhan 1,5×, netral |
| Heatwave | 10 | 10 menit | Penguapan -0,01/tick, Overheat, Sunburnt / Blazing |
| Summer Shower | 10 | 10 menit | WaterLevel +0,05/tick, pertumbuhan 1,0×, Verdant, Wet, mulai pemulihan Overheat |
| Muggy | 5 | 10 menit | WaterLevel 0,00/tick, pertumbuhan 0,85×, Lush, jeda pemulihan Overheat |

- Tidak ada pengulangan cuaca yang sama berturut-turut.
- Heatwave biasa dan Heatwave rantai memiliki efek dasar sama, state pemicu berbeda di UI.
- Summer Shower dan Muggy dapat muncul sebagai cuaca normal. Kemunculan normal tidak memajukan rantai Tornado.

## 4. Rantai Tornado
Urutan pemicu: **Heatwave → Summer Shower → Muggy → Tornado**

- Tornado event server-wide, minimal 1 kali dan maksimal 5 kali per Summer.
- Pemeriksaan progres musim: 50%, 60%, 70%, 80%, 85%.
- Empat pemeriksaan pertama masing-masing peluang 10%.
- Pemeriksaan 85%: jaminan rantai jika belum ada Tornado.
- Setelah Tornado selesai: cuaca beralih ke Sunny atau Cloudy 50/50.
- Muggy dalam status rantai menampilkan notifikasi peringatan Tornado.

## 5. Efek Tornado per Plot
- Tornado mendatangi setiap plot yang ditempati satu per satu.
- Radius dampak: **14 studs**.
- Plot kosong tidak mendapat lintasan. Greenhouse tidak terkena dan tidak mendapat Mutation cuaca.
- Tanaman dalam radius menerima penurunan instan **-1,000 WaterLevel** sekali (minimum 0,000).
- Buah eligible roll sekali saat terkena: Whirlwind (Rare, 35%), Tempest (Epic, 8%).
- Tanaman muda berisiko Uprooted; tanaman menengah/dewasa berisiko Windblown. Tidak ada kematian langsung dari Tornado.
- Uprooted menyimpan progres, buah, Variant, dan Mutation. Ditanam ulang dengan Trowel, lalu menerima Windblown sementara.

## 6. Heatwave & Overheat
- Klasifikasi tanaman: Heat-loving (1,25×), Heat-neutral (1,0×), Heat-sensitive (0,75×), Extremely Heat-sensitive (0,50×).
- Overheat muncul setelah 3 menit paparan berturut-turut pada tanaman Heat-sensitive dan Extremely Heat-sensitive.
- Risiko kematian saat Overheat mulai: Heat-sensitive 20%, Extremely Heat-sensitive 40%.
- Pemulihan: 30 menit online dalam kondisi sejuk atau hujan. Item **Cooling Balm** menghapus Overheat seketika.

## 7. Mutation & Variant Summer
| Mutation | Cuaca Sumber | Tingkat | Peluang per buah/tick |
|---|---|---|---:|
| Verdant | Summer Shower | Rare | 2% |
| Lush | Muggy | Uncommon | 1,5% |
| Whirlwind | Tornado | Rare | 35% |
| Tempest | Tornado | Epic | 8% |
| Sunburnt | Heatwave | Uncommon | 2,945% (~45% kumulatif) |
| Blazing | Heatwave | Rare | 0,5254% (~10% kumulatif) |

- Batas maksimum 15 Mutation unik per buah.
- Variant roll harian per plot: dasar 0,5%, +0,05 poin persentase tiap gagal, reset tiap musim.
- Roll hanya jika plot ditempati. Greenhouse tidak menerima Mutation cuaca.

## 8. Klasifikasi Tanaman Panas
- Heat-loving, Heat-neutral, Heat-sensitive, Extremely Heat-sensitive.
- Roster tanaman spesifik Summer ditunda.

## 9. Perlindungan Tanaman
- Storm Catcher: maksimal 2 per plot.
- Storm Shield: maksimal 1 per plot, radius dan efek dapat di-upgrade maksimal 3 level (mengorbankan 1 Storm Shield per upgrade).
- Small Protection Kit (Life Coin), Medium Protection Kit (Robux, isi lebih banyak tanpa keunggulan mekanik).

## 10. Ekonomi & Rarity
- Tier Benih: Common (100), Uncommon (500), Rare (2.500), Epic (10.000), Legendary (50.000), Mystic (250.000).
- Toko Summer terbatas pada tier Common, Uncommon, dan Rare.
- Season Pill: 80% harga jual buah dewasa.
- Multiplier harga per tier Mutation dan Variant masih belum ditetapkan.

## 11. Kriteria Penerimaan (Acceptance Criteria)
1. Durasi Summer 30 hari in-game berjalan konsisten.
2. Transisi 3 hari terakhir dengan preview visual 20% memicu tampilan musiman tanpa mengubah gameplay.
3. Rantai Tornado berjalan sesuai progres musim 50%–85%.
4. Tornado hanya memasuki plot ditempati, radius 14 studs, tidak memasuki Greenhouse atau plot kosong.
5. Heatwave menghasilkan penguapan WaterLevel dan Overheat sesuai klasifikasi tanaman.
6. Summer Shower dan Muggy muncul sebagai cuaca normal dan sebagai bagian rantai Tornado.
7. Tanaman Uprooted dapat ditanam ulang dengan Trowel; Windblown pulih otomatis.
8. Storm Catcher (maks 2/plot) dan Storm Shield (maks 1/plot) berfungsi untuk petir.
9. Toko Summer hanya menampilkan tier Common–Rare.
10. Tidak ada spec yang dinaikkan menjadi READY.
