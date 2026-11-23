# PRD: Musim Spring (Garden Life - First Release)

## 1. Tujuan
Spring memperkenalkan cuaca, WaterLevel, Mutation cuaca, dan perlindungan petir dengan identitas visual **Fresh Nature** serta pola cuaca **Balanced**.

## 2. Kalender
- Durasi: 30 hari in-game.
- Soft Transition: hari 28-30, preview visual Summer sebesar 20%; efek gameplay Summer baru aktif pada hari pertama Summer.
- Satu server menggunakan satu cuaca bersama untuk semua plot.
- Saat plot kosong, kalender dan visual cuaca tetap berjalan; WaterLevel, pertumbuhan, dan Mutation tanaman pada plot tersebut freeze.
- 1 tick = 30 detik. Sunny berlangsung 40 tick (20 menit); cuaca non-Sunny berlangsung 20 tick (10 menit).

## 3. Roster dan distribusi cuaca
| Cuaca | Bobot | Durasi | Efek utama |
|---|---:|---|---|
| Sunny | 34 | 20 menit | Netral, tanpa Mutation |
| Cloudy | 16 | 10 menit | +0,25 WaterLevel sekali; tanaman Sun-loving 0,85× |
| Drizzle | 14 | 10 menit | +0,05 WaterLevel/tick; pertumbuhan 0,85×; Wet |
| Windy | 12 | 10 menit | -0,005 WaterLevel tiap 2 tick; pertumbuhan 1,5× |
| Rainy | 10 | 10 menit | +0,075 WaterLevel/tick; pertumbuhan 0,80×; Wet dan evolusi Flooded |
| Misty | 8 | 10 menit | +0,25 WaterLevel sekali; pertumbuhan 0,85×; Wet, Misty/Foggy |
| Thunderstorm | 6 | 10 menit | Wet, petir, Shocked/Charged, risiko Scorched atau tanaman mati |

- Bobot adalah tabel balancing D-048 dan berjumlah 100.
- Cuaca yang baru selesai tidak boleh langsung berulang.
- Thunderstorm hanya dapat mengikuti Cloudy atau Rainy, maksimal 2 episode per hari in-game.
- Misty hanya dapat mengikuti Cloudy, Drizzle, atau Rainy.
- Windy tidak dapat mengikuti Windy.
- Setelah Thunderstorm, cuaca berikutnya Sunny atau Cloudy dengan peluang 50/50.

## 4. Shared Weather & Mutation
- Cloudy, Drizzle, Rainy, Windy, dan Misty mengikuti angka final pada dokumen Shared Weather Specification (D-061).
- Wet dapat diperoleh dari semua cuaca basah, dan hanya dari cuaca (D-086). Sumber basah Spring: Drizzle, Rainy, Misty, dan Thunderstorm. Aktivitas pemain, alat penyiraman, dan WaterLevel tinggi tidak menghasilkan Wet.
- Peluang Wet final belum ditetapkan; angka 2,5% pada keputusan lama merupakan baseline terdahulu yang akan ditinjau dalam balancing Mutation (D-086).
- Rainy: buah yang sudah memiliki Wet dapat berevolusi menjadi Flooded, yang secara konsep menggambarkan buah tergenang atau terlalu basah (D-089). Peluang evolusi final mengikuti balancing Mutation. Flooded menggantikan Wet; Wet tidak lagi tercatat dan multiplier Wet tidak lagi berlaku setelah evolusi berhasil (D-088).
- Flooded dari WaterLevel tinggi dihapus. Flooded hanya diperoleh melalui evolusi Wet → Flooded selama Rainy (D-087).
- WaterLevel disimpan dengan presisi 0,001, rentang 0,000-5,000.
- Mutation cuaca hanya roll pada plot yang ditempati. Greenhouse tidak menerima Mutation cuaca.
- Maksimal 15 Mutation unik per buah.

## 5. Thunderstorm dan perlindungan petir
- Setiap plot melakukan roll sambaran 1% per tick; maksimal 5 sambaran per plot per episode.
- Titik sambaran acak dalam plot, radius dampak 8 studs.
- Buah pada tanaman terdampak mendapat Shocked 100%; setiap buah melakukan roll Charged 15%.
- Hasil kondisi tanaman per sambaran bersifat mutually exclusive: 60% tidak rusak, 25% Scorched, 15% mati.
- WaterLevel bertambah +0,075/tick dan pertumbuhan tanaman menggunakan multiplier 0,80× selama Thunderstorm.
- **Storm Catcher** (nama final Lightning Rod) radius 24 studs, peluang redirect 50%, maksimal 3 redirect berhasil per item.
- **Storm Shield** (nama final Thunderstorm Relief) radius 20 studs. Setiap item mengurangi peluang Scorched dan mati masing-masing 5 poin persentase; maksimal 3 item aktif. Durabilitas 3 sambaran per item.
- **Scorch Balm** menghapus status Scorched pada satu tanaman. Tanaman mati mengikuti alur cabut, buang/kompos, atau revive Robux yang ditetapkan sistem plant-death.

## 6. Ekonomi dan item
- Harga benih mengikuti D-052: Common 100, Uncommon 500, Rare 2.500, Epic 10.000, Legendary 50.000, Mystic 250.000 Life Coin.
- Toko Spring First Release terbatas Common, Uncommon, dan Rare.
- Harga Storm Catcher, Storm Shield, Scorch Balm, dan multiplier Mutation belum final.
- Season Pill mengikuti aturan lintas musim: 80% harga jual buah dewasa.

## 7. Kriteria penerimaan
1. Spring berlangsung 30 hari in-game dan transisi hari 28-30 hanya mengubah visual.
2. Cuaca mengikuti bobot, durasi, dan batas transisi pada tabel.
3. Shared Weather mengikuti klasifikasi sumber Wet D-086; peluang Wet final menunggu balancing Mutation.
4. Thunderstorm mematuhi roll sambaran, radius, batas, Mutation Wet/Shocked/Charged, dan hasil kondisi tanaman.
5. Storm Catcher, Storm Shield, dan Scorch Balm mengikuti aturan perlindungan yang ditetapkan.
6. Plot kosong tidak menerima efek tanaman atau roll Mutation catch-up.
7. Tidak ada spec yang dinaikkan menjadi READY.