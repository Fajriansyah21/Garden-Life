# PLAYER JOURNEY · Garden Life

**Status:** DRAFT  
**Versi:** 0.2  
**Tanggal:** 2026-11-15  
**Terkait:** D-008, D-009, D-010, D-023, D-024, D-025; GDD v1.8  
**Tujuan dokumen:** Menggambarkan perjalanan pengalaman pemain dari pertama kali masuk hingga memiliki kebun yang berkembang dan identitas personal.

> Dokumen ini adalah rancangan pengalaman pemain, bukan spesifikasi implementasi atau persetujuan scope rilis. Aturan, fitur, angka, dan sistem yang belum diputuskan tetap ditandai sebagai usulan atau BELUM DIPUTUSKAN. Status dokumen hanya dapat diubah menjadi READY oleh pemilik proyek.

## 1. Prinsip Player Journey

Player Journey Garden Life dibagi menjadi empat tahap pengalaman:

1. **First Visit** — mengenal dunia, plot, dan kebebasan yang dimiliki.
2. **Early Garden** — mulai membentuk kebun melalui dekorasi, penanaman, dan perawatan dasar.
3. **Growing Garden** — memperluas identitas kebun melalui koleksi, variasi, progres, dan interaksi sosial.
4. **Established Garden** — memiliki kebun dengan karakter kuat dan aktivitas berkelanjutan bersama atau tanpa pemain lain.

Tahap ini adalah **fase pengalaman**, bukan level karakter, ranking, atau gerbang waktu. Pemain dapat bergerak dengan kecepatan berbeda. Tidak ada kewajiban menyelesaikan semua aktivitas satu tahap sebelum menikmati aktivitas tahap lain.

### Prinsip yang berlaku di semua tahap

- **Decoration-first:** pemain harus selalu punya ruang untuk mengekspresikan gaya kebunnya.
- **Cozy, not demanding:** aktivitas tidak boleh menciptakan tekanan login harian atau hukuman offline yang bertentangan dengan visi cozy.
- **Progress is visible:** perkembangan kebun harus terlihat melalui ruang, koleksi, tanaman, dan hasil penataan.
- **Player agency:** pemain memilih fokus aktivitas; farming bukan kewajiban untuk menikmati game.
- **Social by choice:** kunjungan dan kolaborasi memperkaya pengalaman, tetapi pemain solo tetap dapat menikmati loop utama.
- **Short-session friendly:** pemain dapat melakukan aktivitas bermakna dalam sesi singkat dan melanjutkan kebunnya pada sesi berikutnya.
- **Consistent ownership:** objek, inventori, dan perubahan kebun mengikuti aturan kepemilikan serta izin yang berlaku.
- **Server-authoritative:** perubahan yang bernilai dan state persisten divalidasi server.

## 2. Ringkasan perjalanan

| Tahap | Pertanyaan pemain | Pengalaman yang harus terbentuk | Hasil pengalaman |
|---|---|---|---|
| First Visit | "Ini kebunku, dan aku bisa mulai dari mana?" | Aman, paham, tidak kewalahan | Mengenali plot, inventori awal, dan satu tindakan awal |
| Early Garden | "Bagaimana kebun ini mulai terlihat seperti milikku?" | Kreatif, produktif, mendapat feedback | Kebun mulai memiliki tata letak, dekorasi, dan tanaman |
| Growing Garden | "Apa lagi yang bisa kukoleksi dan kembangkan?" | Penasaran, punya tujuan pilihan | Kebun berkembang melalui koleksi, variasi, dan progres |
| Established Garden | "Apa yang ingin kulakukan dengan kebun yang sudah kubangun?" | Bangga, nyaman kembali, ingin berbagi | Kebun punya identitas dan aktivitas jangka panjang |

## 3. Tahap 1 · First Visit

### Tujuan pengalaman

Pemain mengenali plot sebagai ruang personal, mengetahui bahwa Starter Kit tersedia di Inventory, lalu memilih sendiri cara pertama untuk mulai membentuk kebun. Onboarding memberi arah tanpa mengambil alih kontrol atau memaksa pemain mengikuti tutorial panjang.

### Prinsip onboarding

- **Contextual guidance:** petunjuk muncul saat relevan dengan tindakan pemain.
- **Player-controlled:** pemain sendiri yang membuka dan menutup Inventory.
- **Visible choices:** isi Starter Kit dan tiga kelompok item dapat dilihat sejak Inventory dibuka.
- **Guided, not locked:** highlight dan penjelasan memberi arahan, tetapi pemain tetap bebas menjelajahi UI.
- **Free choice, farming guided:** pemain dapat memilih bertani atau mendekorasi; farming boleh menjadi jalur rekomendasi, bukan kewajiban.
- **One meaningful action:** onboarding awal berakhir setelah pemain berhasil melakukan satu tindakan kreatif pada jalur pilihannya.

### Alur pengalaman yang disepakati (D-025)

| Urutan | Pemicu / tindakan pemain | Respons game | Catatan desain |
|---:|---|---|---|
| 1 | Pemain masuk ke plot pertamanya | Tampilkan plot kosong dan identitas plot | Plot kosong mengikuti D-008; item awal tidak otomatis ditempatkan |
| 2 | Pemain sudah mendapat kesempatan mengenali plot | Beri penanda visual pada tombol Inventory dan prompt singkat | Contoh teks: "Perlengkapan kebunmu sudah tersedia. Buka Inventory untuk melihatnya!" |
| 3 | Pemain menekan tombol Inventory | Buka panel Inventory | Panel tidak dibuka otomatis |
| 4 | Inventory tampil | Tampilkan ketiga kelompok: Tools, Farming, Decorations | Ketiganya terlihat sekaligus sejak awal |
| 5 | Pengenalan kelompok dimulai | Highlight dan tooltip memperkenalkan Tools, lalu Farming, lalu Decorations | Navigasi tidak dikunci; pemain bebas memilih kelompok lain |
| 6 | Pemain menjelajah atau menyelesaikan pengenalan | Biarkan Inventory tetap interaktif | Penjelasan dapat dilewati; detail kontrol final UI belum ditetapkan |
| 7 | Pemain menutup Inventory | Tutup panel atas tindakan pemain | Tidak ada penutupan otomatis |
| 8 | Inventory sudah ditutup | Tampilkan pilihan Mulai Bertani atau Mulai Mendekorasi | Farming dapat diberi penekanan visual sebagai rekomendasi, tetapi kedua pilihan setara sebagai jalur onboarding |
| 9A | Pemain memilih Mulai Bertani | Pandu pemain menempatkan Farm Tile, memilih Benih Wortel, lalu menanam | Jangan menambahkan waktu tumbuh, hasil, harga, atau reward yang belum diputuskan |
| 9B | Pemain memilih Mulai Mendekorasi | Pandu pemain menempatkan Kursi Kayu atau Lampu Taman | Pemain bebas menentukan posisi dan tata letak |
| 10 | Pemain berhasil melakukan tindakan kreatif pertama | Akhiri onboarding awal dan kembalikan kendali penuh kepada pemain | Tidak ada kewajiban mencoba jalur lainnya |

### Kelompok Starter Kit

| Kelompok | Item | Fungsi yang dikenalkan |
|---|---|---|
| Tools | Shovel | Menghapus tanaman |
| Tools | Trowel | Memindahkan tanaman |
| Tools | Watering Can | Menyiram tanaman |
| Tools | Pupuk | Direncanakan membantu pertumbuhan; efek dan aturan penggunaan belum ditetapkan |
| Farming | Farm Tile | Menyediakan area untuk aktivitas tanam |
| Farming | Benih Wortel | Benih awal untuk mulai menanam |
| Decorations | Kursi Kayu | Dekorasi kebun |
| Decorations | Lampu Taman | Dekorasi kebun |

Kuantitas Starter Kit tetap mengikuti D-010. Pengelompokan ini hanya mengatur cara item diperkenalkan di UI, bukan mengubah inventori atau kepemilikan item.

### Aturan kebebasan pemain

- Pemain boleh memilih kelompok lain saat highlight sedang menjelaskan satu kelompok.
- Pemain tidak perlu membaca semua tooltip untuk menggunakan item.
- Pemain boleh melewati pengenalan kelompok.
- Pemain boleh menutup Inventory setelah melihat isi kit, meskipun belum menyelesaikan semua penjelasan.
- Pemain boleh memilih jalur dekorasi tanpa mencoba farming, atau sebaliknya.
- Jika pemain tidak mengikuti petunjuk atau menutup panel lebih awal, onboarding tidak boleh memaksa panel terbuka kembali. Petunjuk berikutnya dapat muncul secara kontekstual sesuai alur, tanpa mengunci kontrol.
- Kondisi teknis untuk memulihkan onboarding setelah pemain keluar/disconnect belum ditentukan dan perlu dirinci pada spec onboarding.

### Aktivitas inti

1. Mengenali plot dan batas ruang pribadi.
2. Menemukan tombol Inventory dan membukanya sendiri.
3. Melihat Starter Kit dalam tiga kelompok yang langsung terlihat.
4. Memahami fungsi item melalui penjelasan singkat yang bertahap dan dapat dilewati.
5. Memilih jalur awal: bertani atau mendekorasi.
6. Melakukan satu tindakan kreatif pertama.
7. Mengetahui bahwa kebun dapat terus dikembangkan dengan kebebasan memilih aktivitas.

### Feedback yang dibutuhkan

- Identitas plot dan kepemilikan mudah dikenali.
- Tombol Inventory mendapat penanda visual yang jelas tanpa menutupi kontrol lain.
- Prompt Inventory singkat dan mudah dipahami.
- Kategori Tools, Farming, dan Decorations terlihat bersamaan.
- Highlight/tooltip menunjukkan kelompok yang sedang diperkenalkan tanpa menghalangi navigasi Inventory.
- Aksi placement pertama memiliki preview dan feedback berhasil/gagal yang jelas sesuai Build Mode.
- Pemain memahami bahwa memilih dekorasi tidak berarti melewatkan atau gagal dalam permainan.

### Hasil tahap / sinyal transisi

First Visit dianggap berhasil ketika pemain:
- mengenali plot sebagai ruang personal;
- mengetahui Starter Kit tersedia di Inventory;
- memahami bahwa item awal dikelompokkan menjadi Tools, Farming, dan Decorations;
- memilih salah satu jalur aktivitas awal;
- berhasil melakukan satu tindakan kreatif pada jalur tersebut.

Ini bukan syarat unlock atau gerbang progres. Pemain boleh mengabaikan arahan dan mengeksplorasi game. Onboarding awal tidak boleh menahan akses ke kebun.

### Risiko desain

| Risiko | Mitigasi rancangan |
|---|---|
| Plot kosong terasa seperti tidak ada yang bisa dilakukan | Tunjukkan bahwa Starter Kit tersedia di Inventory |
| Inventory otomatis terbuka dan terasa mengambil alih kontrol | Biarkan pemain membuka panel sendiri melalui penanda visual |
| Tutorial terlalu padat | Gunakan tooltip singkat dan penjelasan bertahap yang dapat dilewati |
| Pemain mengira harus menyelesaikan seluruh tutorial kategori | Izinkan navigasi bebas dan penutupan Inventory kapan saja |
| Pemain mengira farming wajib | Tampilkan jalur dekorasi sebagai pilihan yang sama-sama valid |
| Pemain salah mengira item telah ditempatkan | Jelaskan bahwa Starter Kit berada di Inventory, bukan di plot |
| Detail farming yang belum diputuskan terlanjur dijanjikan | Batasi arahan pada penempatan tile, pemilihan benih, dan tindakan menanam; jangan menyebut waktu/reward |

## 4. Tahap 2 · Early Garden

### Tujuan pengalaman

Pemain mulai mengubah plot kosong menjadi kebun yang terasa personal. Tahap ini harus memperlihatkan identitas utama Garden Life: kreativitas dan kepuasan menata ruang.

### Aktivitas inti

1. Menempatkan dekorasi awal, misalnya Kursi Kayu dan Lampu Taman dari Starter Kit.
2. Menempatkan Farm Tile dan menentukan area tanam.
3. Menanam benih yang tersedia dan mengenali interaksi perawatan dasar.
4. Mengamati perubahan tanaman hingga siap dipanen, mengikuti aturan pertumbuhan yang nantinya disepakati.
5. Mencoba menjual hasil panen jika sistem penjualan sudah tersedia dalam scope.
6. Menggunakan hasil aktivitas untuk memperoleh pilihan dekorasi, tile, tanaman, atau kebutuhan kebun lain jika sistem toko dan ekonomi telah ditetapkan.

### Pengalaman yang harus terbentuk

- Pemain melihat perubahan nyata dari plot kosong menjadi kebun awal.
- Dekorasi memberi nilai ekspresi, bukan hanya bonus statistik.
- Farming menjadi aktivitas alternatif yang memberi bahan atau nilai ekonomi untuk mengembangkan kebun.
- Pemain dapat memilih apakah ingin lebih banyak mendekorasi, menanam, atau mencoba keduanya.
- Kesalahan penataan sebisa mungkin dapat diperbaiki tanpa kehilangan item secara tidak adil.

### Feedback yang dibutuhkan

- Preview placement dan indikator posisi valid/tidak valid.
- Feedback saat objek berhasil ditempatkan, dipindahkan, atau disimpan.
- Status tanaman dan kebutuhan perawatan dapat dipahami.
- Hasil panen dan transaksi ditampilkan secara transparan setelah sistemnya ditetapkan.
- Pemain memahami item apa yang dimiliki dan apa yang masih perlu diperoleh.

### Hasil tahap / sinyal transisi

Tahap Early Garden mulai terlewati ketika:
- plot tidak lagi hanya berupa ruang kosong;
- pemain telah membuat beberapa pilihan tata letak/dekorasi miliknya sendiri;
- pemain memahami setidaknya satu aktivitas berulang yang dapat dilakukan, seperti merawat tanaman atau mengembangkan dekorasi.

Tidak ada jumlah objek, tanaman, atau durasi minimum yang diwajibkan.

### Risiko desain

| Risiko | Mitigasi rancangan |
|---|---|
| Farming terasa wajib untuk memperoleh semua dekorasi | Sediakan atau evaluasi jalur perolehan dekorasi yang tidak hanya bergantung pada farming |
| Pemain kehabisan tujuan setelah menempatkan item awal | Berikan tujuan opsional yang terlihat dan bertahap |
| Build Mode terlalu rumit untuk pemain baru | Prioritaskan kontrol inti dan bantuan kontekstual |
| Pertumbuhan tanaman menuntut pemain terus online | Hindari penalti offline yang tidak sesuai pilar cozy; aturan waktu tumbuh perlu dianalisis |

## 5. Tahap 3 · Growing Garden

### Tujuan pengalaman

Pemain memiliki alasan untuk terus mengembangkan kebun melalui pilihan koleksi, variasi visual, progres, dan aktivitas sosial. Tahap ini memperluas pilihan, bukan mengganti kebebasan yang sudah dipelajari.

### Aktivitas inti yang dapat dirancang

- Membuka atau memperoleh tanaman dengan karakter dan kebutuhan berbeda.
- Mengoleksi dekorasi, bangunan, dan variasi objek.
- Mengembangkan ukuran atau tata ruang plot melalui sistem ekspansi yang sudah memiliki fondasi ukuran.
- Mengenal sistem koleksi khusus seperti Variant dan Mutation sesuai aturan D-022.
- Berinteraksi dengan musim dan cuaca jika sistem tersebut disetujui sebagai scope.
- Mengunjungi kebun pemain lain, mendapat inspirasi, atau berkolaborasi sesuai izin plot.
- Mengembangkan inventori dan pilihan aktivitas tanpa membuat manajemen menjadi beban utama.

**Catatan scope:** Variant, Mutation, musim, cuaca, tanaman langka, ekspansi lanjutan, dan fitur sosial yang lebih luas memiliki keputusan atau konsep tingkat tinggi dengan detail yang belum seluruhnya lengkap. Penyebutan di tahap ini tidak menjadikannya otomatis fitur First Release.

### Pengalaman yang harus terbentuk

- Pemain menemukan tujuan personal, misalnya menyusun tema kebun, mengoleksi tanaman tertentu, atau membuat area khusus.
- Progres membuka pilihan baru, bukan mengunci kreativitas pemain.
- Koleksi memiliki nilai visual dan emosional, bukan hanya nilai jual.
- Interaksi sosial memberi inspirasi dan rasa komunitas tanpa mengharuskan pemain bermain bersama.
- Pemain dapat memilih fokus jangka menengahnya sendiri.

### Feedback yang dibutuhkan

- Pemain dapat mengetahui item/varian yang sudah dan belum dimiliki.
- Syarat memperoleh koleksi khusus dijelaskan secara wajar tanpa membocorkan seluruh kejutan.
- Progres plot dan koleksi terlihat.
- Sistem sosial menunjukkan role, izin, dan kepemilikan dengan jelas.
- Sistem ekonomi tidak membuat item dekorasi terasa mustahil dijangkau.

### Hasil tahap / sinyal transisi

Pemain mulai berada pada tahap Growing Garden ketika:
- sudah memiliki preferensi atau tujuan pengembangan kebun;
- mulai mengejar koleksi, variasi, atau ruang tambahan berdasarkan pilihannya;
- memahami beberapa sistem kebun dan dapat memilih aktivitas tanpa selalu diarahkan tutorial.

Tidak ada level atau jam bermain yang ditetapkan sebagai batas.

### Risiko desain

| Risiko | Mitigasi rancangan |
|---|---|
| Koleksi langka menciptakan grind atau FOMO berlebihan | Hindari tenggat yang menghukum pemain; evaluasi peluang dan jalur perolehan |
| Ekonomi membuat dekorasi penting terlalu mahal | Analisis source/sink dan aksesibilitas dekorasi |
| Banyak sistem baru membingungkan | Perkenalkan sistem bertahap dan jelaskan hubungan antarfitur |
| Multiplayer menimbulkan konflik kepemilikan | Tegakkan role permission, ownership, dan validasi server |
| Variant/Mutation membuat nilai jual tidak terkendali | Simulasikan kombinasi multiplier dan dampak ekonomi sebelum rilis |

## 6. Tahap 4 · Established Garden

### Tujuan pengalaman

Pemain memiliki kebun yang mencerminkan identitasnya dan tetap memiliki alasan menyenangkan untuk kembali, bahkan setelah banyak tujuan awal tercapai.

Tahap ini bukan "tamat". Ini adalah keadaan berkelanjutan ketika kebun menjadi ruang personal yang terus dapat diperbarui.

### Aktivitas inti yang dapat dirancang

- Menata ulang, mempercantik, atau memperluas tema kebun.
- Menyelesaikan proyek dekorasi personal.
- Melengkapi koleksi tanaman atau dekorasi yang diinginkan.
- Mengunjungi kebun teman dan mengundang pemain lain.
- Membantu proyek kebun bersama dengan izin yang sesuai.
- Mengikuti event atau konten musiman jika sistem Live-ops disetujui dan memiliki kapasitas produksi.
- Mengambil jeda dan kembali tanpa kehilangan rasa aman terhadap progres kebun.

### Pengalaman yang harus terbentuk

- Pemain merasa kebunnya memiliki identitas yang unik.
- Kebun menjadi alasan untuk berbagi, berkunjung, atau berkolaborasi.
- Pemain memiliki tujuan yang dapat dibuat sendiri, bukan hanya daftar tugas sistem.
- Konten baru memperkaya pilihan dan tidak membuat hasil dekorasi lama terasa usang.
- Pemain yang tidak mengejar koleksi tetap dapat menikmati game.

### Feedback yang dibutuhkan

- Layout dan koleksi pemain tersimpan dengan aman.
- Pemain dapat melihat perubahan kebunnya dari waktu ke waktu.
- Aktivitas sosial menghormati izin dan kepemilikan.
- Konten baru dapat dinikmati tanpa mewajibkan pemain menyelesaikan seluruh konten sebelumnya.

### Hasil tahap

Tidak ada kondisi selesai. Established Garden adalah siklus berkelanjutan:
**menata → menikmati → berbagi → menemukan inspirasi → mengembangkan kembali.**

### Risiko desain

| Risiko | Mitigasi rancangan |
|---|---|
| Pemain lama kehabisan tujuan | Dukung proyek personal, koleksi, dan konten opsional |
| Update membuat pemain merasa tertinggal | Hindari progres musiman yang menghukum ketidakhadiran |
| Event menjadi kewajiban login | Buat event dapat diikuti secara fleksibel |
| Konten baru mengurangi nilai koleksi lama | Pertahankan kegunaan dan nilai visual konten terdahulu |

## 7. Loop lintas tahap

### Loop utama kebun

**Bayangkan → Tata → Rawat → Nikmati → Bagikan → Kembangkan lagi**

Loop ini menjadi payung pengalaman. Farming loop (tanam → tumbuh → panen → jual → gunakan hasil) adalah salah satu loop pendukung, bukan keseluruhan identitas game.

### Loop sesi singkat

Pemain yang hanya punya sedikit waktu tetap perlu dapat:
- masuk dan melihat kebunnya;
- melakukan satu perubahan kecil atau satu interaksi yang bermakna;
- memperoleh feedback yang jelas;
- keluar tanpa kehilangan progres yang sudah tersimpan.

Durasi target sesi dan batas numeriknya **BELUM DIPUTUSKAN**.

### Loop kembali bermain

Alasan kembali sebaiknya berasal dari:
- keinginan melanjutkan proyek kebun;
- rasa penasaran pada koleksi atau pilihan dekorasi;
- keinginan melihat hasil perkembangan tanaman/kebun;
- interaksi sosial yang memang dipilih pemain;
- konten baru yang tidak menghukum pemain yang absen.

Hindari membuat pemain kembali karena takut tanaman, item, atau progresnya hilang akibat tidak login, kecuali konsekuensi tersebut kelak secara eksplisit disetujui dan terbukti sesuai visi cozy.

## 8. Analisis desain awal

| Aspek analisis | Temuan |
|---|---|
| Masalah / tujuan | Memberi arah pengalaman yang konsisten dari onboarding hingga kebun matang |
| Pemain target | Pemain cozy/casual yang menyukai kreativitas, koleksi, dan interaksi sosial opsional; profil demografis spesifik BELUM DIPUTUSKAN |
| Mekanik | Empat fase pengalaman dengan transisi berbasis pemahaman dan tujuan personal, bukan angka level/waktu |
| Dampak core loop | Menjaga dekorasi sebagai loop utama dan farming sebagai loop pendukung |
| Dampak ekonomi | Tidak menetapkan source/sink baru. Tahap Early dan Growing membutuhkan sistem toko, koleksi, dan ekonomi yang seimbang agar pilihan dekorasi tetap dapat dijangkau |
| Risiko | Scope melebar, koleksi menciptakan grind, tutorial terlalu padat, dan fitur sosial menambah kompleksitas |
| Biaya implementasi | Belum dinilai; Player Journey adalah artefak desain. Estimasi teknis fitur ditentukan Claude pada masing-masing spec |
| Metrik sukses | Akan ditentukan dalam playtest setelah target pemain, onboarding, dan scope Vertical Slice disepakati |

### Metrik yang perlu dipertimbangkan pada tahap playtest

Angka target belum ditetapkan. Metrik kandidat:
- persentase pemain yang memahami plot dan inventori awal;
- persentase pemain yang berhasil melakukan placement pertama;
- waktu menuju tindakan kreatif pertama;
- persentase pemain yang mencoba aktivitas dekorasi dan farming;
- distribusi pilihan aktivitas (dekorasi, farming, sosial);
- persentase pemain yang kembali melanjutkan proyek kebun;
- titik kebingungan atau drop-off per tahap.

Jangan menetapkan target angka sebelum ada baseline playtest.

## 9. Dependensi sistem

| Tahap | Sistem yang dibutuhkan atau terkait | Status desain |
|---|---|---|
| First Visit | Plot, onboarding, Starter Kit, inventori, UI dasar, persistensi | Prinsip onboarding dicatat dalam D-025; detail UI, state, dan edge case masih perlu dirinci dalam spec |
| Early Garden | Build Mode, dekorasi, Farm Tile, tanaman, tools, pertumbuhan, panen, toko/ekonomi | FEAT-001 dan FEAT-002 DRAFT; sistem tanaman dan ekonomi belum lengkap |
| Growing Garden | Katalog tanaman/dekorasi, progres, ekspansi, koleksi, Variant/Mutation, musim/cuaca, sosial | Beberapa keputusan tingkat tinggi tersedia; detail dan scope belum disetujui |
| Established Garden | Persistensi jangka panjang, kunjungan/co-op, konten lanjutan, event/Live-ops, moderasi, performa | Sebagian besar belum dirancang atau belum ditetapkan sebagai scope |

## 10. Pertanyaan terbuka

1. Siapa target pemain yang lebih spesifik dan perangkat mana yang menjadi prioritas uji?
2. Apa tiga game referensi dan pelajaran yang ingin diambil dari masing-masing?
3. Apakah First Visit perlu tutorial terpandu, onboarding kontekstual, atau kombinasi keduanya?
4. Apa definisi "tindakan kreatif pertama" yang harus dicapai pemain baru?
5. Apakah dekorasi awal dapat diperoleh melalui jalur selain farming?
6. Apa jenis progres jangka menengah yang paling cocok: ekspansi plot, level, katalog koleksi, atau kombinasi?
7. Aktivitas sosial apa yang benar-benar dibutuhkan untuk First Release?
8. Bagaimana pemain dapat kembali setelah lama absen tanpa merasa tertinggal?
9. Apa metrik dan target yang akan digunakan untuk menilai pengalaman 5 menit pertama?

## 11. Batas keputusan dan scope

- Empat tahap dalam dokumen ini adalah struktur Player Journey yang disetujui pemilik.
- Detail aktivitas di setiap tahap adalah rancangan pengalaman DRAFT, bukan keputusan implementasi baru.
- Penyebutan fitur yang belum disetujui tidak memasukkannya ke First Release.
- Tidak ada level, harga, durasi, peluang, atau target metrik numerik baru yang ditetapkan di dokumen ini.
- Semua fitur implementasi tetap membutuhkan Feature Spec, analisis, dan persetujuan pemilik.
- Perubahan keputusan aktif harus dicatat sebagai entri baru di DECISIONS.md.

## 12. Riwayat revisi

| Versi | Tanggal | Perubahan | Status |
|---|---|---|---|
| v0.2 | 2026-11-15 | Memperinci alur First Visit berdasarkan D-025: Inventory dibuka pemain, pengenalan tiga kelompok Starter Kit, pilihan bertani/dekorasi, dan tindakan kreatif pertama | DRAFT |
| v0.1 | 2026-11-15 | Draft awal empat tahap perjalanan pemain, loop lintas tahap, analisis, dependensi, dan pertanyaan terbuka | DRAFT |
