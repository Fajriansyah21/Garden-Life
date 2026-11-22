# PRD: Musim Winter (Garden Life - First Release)

## 1. Tujuan
Musim Winter berlangsung 30 hari in-game (180 jam real-time). Fokus: Silent Snow, kebekuan, perlindungan tanaman, dan efisiensi bahan bakar.

## 2. Kalender & Musim
- Durasi: 30 hari in-game.
- Transisi: Soft Transition hari 28–30 (preview visual 20% Spring).
- Status Tanaman: Tanaman tidak tahan dingin masuk fase Rest saat suhu/musim tidak cocok.

## 3. Roster Cuaca Winter
| Cuaca | Bobot | Durasi | Efek Utama |
|---|---:|---|---|
| Sunny | 35 | 20 menit | Baseline sejuk, cerah |
| Overcast | 20 | 10 menit | Mendung dingin |
| Snowfall | 15 | 10 menit | Salju tenang |
| Heavy Snow | 10 | 10 menit | Salju menumpuk di plot |
| Frost | 10 | 10 menit | Mulai hari 25-30, status Frosted |
| Freezing Rain | 6 | 10 menit | Hujan es |
| Blizzard | 4 | 10 menit | Badai salju (event khusus) |

- Blizzard adalah event server-wide (14 studs, risiko Uprooted/Frozen).
- Cuaca tidak mengulang dirinya sendiri secara langsung.

## 4. Mekanik Salju & Frozen
- Heavy Snow & Blizzard menaruh tumpukan salju di plot aktif.
- Salju >2 hari = status **Frozen** (pertumbuhan 0×; freeze total, bukan mati).
- **Snow Shovel**: membersihkan salju dalam radius 8 studs, hasilkan **Snow Block**.
- **Snow Block**: dekorasi, rumah salju, bola salju, atau dilelehkan jadi air.

## 5. Blizzard (Event Ekstrem)
- Event mendatangi plot aktif satu per satu (radius 14 studs).
- Plot kosong & Greenhouse kebal.
- Tanaman dalam radius: Uprooted (muda, 30%), Frozen (menengah/dewasa, 50%).
- Mutation: **Glacial** (Epic, 8%), **Blizzard** (Legendary, 1%).
- Uprooted menyimpan progres/Mutation/Variant, ditanam ulang pakai Trowel.

## 6. Heater & Bahan Bakar
- Fasilitas plot, maksimal 2/plot.
- Radius 10 studs, kebal Frozen/Frosted.
- Kapasitas 500 unit. Konsumsi 0,5 unit/tick (8 jam 20 menit real-time saat penuh).
- Nilai Bahan: Daun (1), Tanaman Mati (5-20), Kayu (50).
- Bonus **Hot Embers**: tanaman mati memberi 1,5× durasi panas.

## 7. Mutation Winter
| Mutation | Sumber | Tier | Roll |
|---|---|---|---|
| Chill | Frost | Rare | 1% |
| Glacial | Blizzard | Epic | 8% |
| Blizzard | Blizzard | Legendary | 1% |

- Roll hanya saat terkena trigger cuaca di plot ditempati. Greenhouse kebal Mutation cuaca.

## 8. Ekonomi
- Tier benih: Common (100) s/d Mystic (250.000).
- Season Pill: 80% harga jual buah dewasa.
- Heater & bahan bakar: Beli di shop event atau tebang pohon/kumpulkan daun.

## 9. Kriteria Penerimaan
1. Winter 30 hari in-game dengan Soft Transition.
2. Mekanik Snow Accumulation + Snow Shovel + Frozen fungsional.
3. Blizzard (Event) mendatangi plot aktif sesuai aturan radius/Mutation.
4. Heater beroperasi dengan durasi/bonus bahan bakar yang benar.
5. Tanaman tidak mati langsung akibat Blizzard/Frost.
6. Status label Rest (bukan Dormant).
7. Tidak ada spec berstatus READY.
