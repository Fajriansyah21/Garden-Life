# PRD: Musim Autumn (Garden Life - First Release)

## 1. Tujuan
Autumn berlangsung 30 hari in-game. Fokus: Cozy Harvest, pembersihan daun, pupuk organik, dan persiapan dingin sebelum Winter.

## 2. Kalender
- Durasi: 30 hari in-game.
- Soft Transition hari 28–30: preview visual musim berikutnya 20%, tanpa efek gameplay musim depan.
- Frost mulai hari 25 sampai pergantian Winter. Hari 25–27: peluang Frost 10% per pemilihan cuaca. Durasi Frost 10 menit.
- Status berhenti tumbuh bernama **Rest**, bukan Dormant. Rest membekukan pertumbuhan. Bukan mati. Greenhouse mencegah tanaman masuk Rest karena ketidakcocokan musim, tetapi tidak menghapus Rest yang sudah aktif. Rest yang sudah aktif berakhir melalui Season Pill atau saat musim kembali cocok (D-063).

## 3. Roster cuaca normal
| Cuaca | Bobot | Durasi | Efek |
|---|---:|---|---|
| Sunny | 35 | 20 menit | Netral, tanpa Mutation khusus |
| Cloudy | 20 | 10 menit | Transisi |
| Windy | 15 | 10 menit | Mekanik shared Windy, tanpa Mutation khusus |
| Drizzle | 10 | 10 menit | Mekanik shared Drizzle, Wet |
| Rainy | 8 | 10 menit | Mekanik shared Rainy, Wet menuju Flooded |
| Misty | 7 | 10 menit | Mekanik shared Misty |
| Leaffall | 5 | 10 menit | Menaruh tumpukan daun di plot aktif; Mutation Fall |

- Cuaca tidak mengulang dirinya sendiri langsung.
- Sunny, Windy, Rainy, Drizzle, dan Misty memakai mekanik shared lintas musim.

## 4. Frost dan toleransi dingin
- Frost bukan cuaca normal. Memberi status **Frosted**. Menurunkan suhu. Tidak membunuh langsung.
- Cold-hardy: pertumbuhan normal.
- Temperature-sensitive: tumbuh 0,75× selama Frost.
- Cold-sensitive: berhenti tumbuh selama Frost. Setelah Frost berakhir, masuk Rest jika tidak terlindungi Greenhouse atau Season Pill. Greenhouse mencegah Rest baru, tetapi tidak memulihkan tanaman yang sudah Rest
- Mutation Frost: **Chill**, Rare, 1% per buah eligible per tick. Kumulatif sekitar 18,2% per episode 20 tick. ASUMSI.

## 5. Leaf Accumulation
- Leaffall menaruh 1-3 tumpukan daun per plot per episode. Setiap tumpukan berisi 10-20 Fallen Leaves (D-061); pemilihan jumlah dalam rentang ini belum memiliki distribusi final.
- Fallen Leaves hanya bertambah pada plot aktif. Plot kosong tidak menghasilkan tumpukan catch-up.
- Kapasitas inventory Fallen Leaves: 500.
- Garden Rake: menyapu daun ke satu titik, bisa dipakai berulang, tidak masuk inventory.
- Tangan: ambil daun satu per satu dari titik tumpukan.
- Leaf Basket: sekali pakai, ambil semua daun dalam radius lingkaran langsung ke inventory.
- Daun tidak dibersihkan selama 2 hari in-game: tanaman di bawahnya status **Blocked**, pertumbuhan −50%.
- Satu bahan organik hanya dapat dialokasikan ke Heater atau Leafy Compost Bin, tidak keduanya. UI wajib meminta konfirmasi tujuan bahan (D-061).
- Mutation Leaffall: **Fall**, Epic, 0,5% per buah eligible per tick. Kumulatif sekitar 9,5% per episode 20 tick. ASUMSI. Chance tidak bergantung jumlah daun.

## 6. Leafy Compost Bin
- Fasilitas ditempatkan di plot, seperti Greenhouse.
- 100 poin bahan = 1 pupuk. Sisa poin tersimpan di Bin.
- 1 daun = 5 poin. 20 daun = 1 pupuk.
- Poin tanaman mati ASUMSI: Common 10, Uncommon 25, Rare 50, Epic 100, Legendary 200, Mystic 500.
- Tier Ceiling: daun atau Common maksimal Basic; Uncommon atau Rare maksimal Medium; Epic, Legendary, atau Mystic maksimal Super. Bahan tertinggi di batch menentukan batas.
- Waktu proses: 30 menit real-time per batch, persistent saat offline.
- Antrean: maksimal 3 batch berurutan.
- UI menampilkan progres 0/100 dan tier hasil sebelum proses. Konfirmasi wajib sebelum tanaman mati masuk Bin.
- Tanaman mati: cabut masuk inventory, lalu buang atau kompos. Revive Robux hanya sebelum dicabut.
- Leaf Mold / pupuk hasil Bin mengikuti aturan pupuk D-049: satu pupuk aktif per tanaman; tidak bisa pada Rest, Layu, atau mati.

## 7. Mutation
| Mutation | Sumber | Tier | Roll |
|---|---|---|---|
| Chill | Frost | Rare | 1%/buah/tick |
| Fall | Leaffall | Epic | 0,5%/buah/tick |

- Roll hanya jika plot ditempati. Greenhouse tidak menerima Mutation cuaca.
- Maksimal 15 Mutation unik per buah.
- Multiplier harga belum ditetapkan.

## 8. Ekonomi
- Tier benih mengikuti D-052: Common 100 sampai Mystic 250.000.
- Toko Autumn terbatas Common, Uncommon, dan Rare. ASUMSI, mengikuti pola Spring/Summer.
- Season Pill = 80% harga jual buah dewasa.
- Harga Garden Rake, Leaf Basket, dan Leafy Compost Bin belum ditetapkan.

## 9. Kriteria penerimaan
1. Autumn berjalan 30 hari in-game.
2. Bobot cuaca normal sesuai tabel. Tidak ada cuaca yang mengulang langsung.
3. Leaffall menghasilkan 1-3 tumpukan/plot/episode, 10-20 daun/tumpukan, inventory maksimal 500 daun, hanya pada plot aktif
4. Garden Rake, tangan, dan Leaf Basket bekerja sesuai peran masing-masing.
5. Daun tidak dibersihkan 2 hari memberi Blocked −50%.
6. Bin: 100 poin, 30 menit, 3 batch, sisa poin tersimpan, Tier Ceiling benar.
7. Frost mulai hari 25. Frosted tidak membunuh. Cold-sensitive tanpa perlindungan masuk Rest setelah Frost berakhir; Greenhouse mencegah Rest baru tetapi tidak menghapus Rest aktif
8. Label UI memakai Rest, bukan Dormant.
9. Chill dan Fall hanya roll pada buah eligible di plot ditempati.
10. Tidak ada spec yang dinaikkan menjadi READY.
