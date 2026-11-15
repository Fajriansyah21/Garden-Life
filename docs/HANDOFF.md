# HANDOFF · Catatan Serah-Terima

Entri terbaru di paling atas. Setiap sesi ChatGPT atau Claude berakhir dengan satu blok handoff.

## Status saat ini
- Fase: 0 Discovery (visi utama sudah dikonfirmasi; exit criteria Discovery belum seluruhnya terpenuhi)
- Fitur aktif: belum ada implementasi gameplay.
- Spec READY menunggu dikerjakan: belum ada.
- Arah utama: pengalaman santai membangun dan mendekorasi kebun; manajemen dan ekonomi ringan sebagai pendukung.
- Dokumen desain: GDD v0.2; keputusan D-002 dan D-003 telah dicatat.
- Pertanyaan terbuka: game referensi, target pemain/perangkat prioritas, detail core loop, dan aturan penempatan/dekorasi.

---

## 15 November 2026 · ChatGPT -> Claude
- Selesai:
  - Memperbarui GDD ke versi 0.2 dengan identitas dekorasi-first.
  - Memindahkan keputusan desain terdahulu yang terkonfirmasi ke DECISIONS (D-002 dan D-003).
  - Mendokumentasikan fondasi plot, kolaborasi, tile, ekspansi, Life Coin, Shared Savings, dan Spending Limit.
  - Mencatat sistem yang pernah dibahas tetapi belum memiliki aturan final sebagai belum diputuskan.
- File diubah / dibuat:
  - docs/02_GAME_DESIGN_DOCUMENT.md
  - docs/DECISIONS.md
  - docs/HANDOFF.md
  - docs/design/CONCEPT_BACKLOG.md
- Spec READY untuk dikerjakan: tidak ada. Semua spec fitur tetap menunggu perincian dan persetujuan pemilik.
- Cara tes (jika kode): tidak ada perubahan kode.
- Pertanyaan terbuka:
  - Referensi game dan target pemain/perangkat.
  - Aturan build/dekorasi: grid, rotasi, batas objek, pemindahan.
  - Aktivitas farming minimum dan ekonomi dasar yang sesuai dengan game santai.
  - Aturan transfer Active Owner dan akses Shared Savings.
- Asumsi / risiko:
  - Detail greenhouse (18 tanaman), 5 tier pupuk, 4 musim, dan cuaca adalah konsep terdahulu, belum diputuskan sebagai scope rilis.
  - Biaya pembuatan rekening/bank belum dikonfirmasi; angka 5.000 yang tercatat adalah biaya administrasi akses bagi anggota yang bergabung setelah Shared Savings dibuat.
  - Belum ada spec DRAFT/READY dan belum ada gameplay yang terverifikasi.

---

## [ISI tanggal] Setup awal
- Selesai: struktur repo dan dokumen dasar dibuat.
- Berikutnya: pemilik dan ChatGPT mengisi `02_GAME_DESIGN_DOCUMENT.md` bagian 1-5.
- Pertanyaan terbuka: -
- Asumsi yang perlu dicek: semua angka di `01_DESIGN_ANALYSIS_SYSTEM.md` masih contoh.

---

### Template blok (salin)

```
## [tanggal] <Pengirim> -> <Penerima>
- Selesai:
- File diubah / dibuat:
- Spec READY untuk dikerjakan:
- Cara tes (jika kode):
- Pertanyaan terbuka:
- Asumsi / risiko:
```
