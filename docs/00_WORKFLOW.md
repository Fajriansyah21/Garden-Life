# 00 · Alur Kerja & Workflow

## 1. Prinsip kolaborasi tiga pihak

- **Repo = sumber kebenaran.** Chat tidak dianggap resmi sampai hasilnya di-commit.
- **Satu pemilik per dokumen** (lihat tabel). Pihak lain boleh mengusulkan, tidak menimpa.
- **Serah-terima lewat `HANDOFF.md`.** Setiap sesi AI berakhir dengan blok handoff.
- **Keputusan lewat `DECISIONS.md`.** Hanya ditambah, tidak dihapus.
- **Pemilik (kamu) = gerbang persetujuan.** Spec baru jalan setelah kamu ubah statusnya ke `READY`.

| Dokumen | Pemilik | Boleh diedit oleh |
|---|---|---|
| `02_GAME_DESIGN_DOCUMENT.md`, `design/*`, `01_DESIGN_ANALYSIS_SYSTEM.md` | ChatGPT | Kamu; Claude hanya mengusulkan lewat HANDOFF |
| `03_TECH_ARCHITECTURE.md`, `src/*`, `tests/*` | Claude | Kamu; ChatGPT hanya mengusulkan |
| `04_ASSET_PIPELINE.md`, `assets/*`, `maps/*` | Kamu | Semua mengusulkan |
| `DECISIONS.md`, `HANDOFF.md` | Bersama | Semua (hanya menambah) |

## 2. Status spec fitur

```
DRAFT -> READY -> IN_PROGRESS -> IMPLEMENTED -> VERIFIED
 (CG)    (Kamu)     (Claude)       (Claude)       (Kamu)
                          \-> BLOCKED (ada pertanyaan; kembali ke ChatGPT)
```

## 3. Fase proyek

| Fase | Tujuan | Pemimpin | Syarat selesai (exit criteria) |
|---|---|---|---|
| 0 Discovery | Tentukan visi, target pemain, referensi | Kamu + ChatGPT | Visi 1 paragraf, target pemain, 3 game referensi tertulis |
| 1 Konsep & GDD | Core loop, ekonomi dasar, daftar fitur | ChatGPT | GDD terisi, kamu setujui, fitur diberi prioritas MoSCoW |
| 2 Vertical Slice | Satu loop utuh yang bisa dimainkan: tanam -> tumbuh -> panen -> jual -> beli bibit | ChatGPT spec, Claude kode | Pemain bisa menyelesaikan loop 5 menit tanpa bug fatal |
| 3 Produksi | Tambah fitur: tanaman, lahan, upgrade, hewan, quest, dll | Siklus fitur (bagian 4) | Semua fitur MUST berstatus VERIFIED |
| 4 Playtest & Analisis | Uji ke teman/komunitas, ukur, analisis | Kamu + ChatGPT | Laporan playtest + daftar perbaikan |
| 5 Balancing & Polish | Setel ekonomi, UI, suara, efek | ChatGPT angka, Claude implementasi | Metrik target tercapai (lihat 01_DESIGN_ANALYSIS_SYSTEM) |
| 6 Rilis | Publish, thumbnail, deskripsi, monetisasi | Kamu | Game publik, checklist rilis lengkap |
| 7 Live-ops | Update berkala berdasarkan data | Semua | Backlog update per 2-4 minggu |

## 4. Siklus satu fitur (workflow harian)

```
[1] Kamu: pilih fitur dari backlog (GDD)
      |
[2] ChatGPT: tulis spec FEAT-XXX (status DRAFT) + analisis dampak ekonomi
      |
[3] Kamu: review. Revisi? -> kembali ke [2].  Setuju? -> ubah status READY
      |
[4] Claude: baca spec -> kerjakan kode -> tulis checklist tes -> status IMPLEMENTED
      |    (ada yang ambigu? -> BLOCKED + pertanyaan di HANDOFF -> ke [2])
      |
[5] Kamu: tes di Roblox Studio via Rojo, ikuti tests/FEAT-XXX_checklist.md
      |
[6] Lolos? -> VERIFIED + commit.  Gagal? -> catat bug -> Claude perbaiki (FIX-XXX)
      |
[7] Kamu: update HANDOFF; ChatGPT: analisis hasil tes bila perlu
```

## 5. Ritual sesi AI

**Awal sesi** (tempel ke chat bila repo tidak bisa dibaca otomatis):
> "Baca README, GDD, DECISIONS, HANDOFF. Ringkas dalam 3 baris lalu tanyakan apa yang dikerjakan hari ini."

**Akhir sesi:** AI menulis blok HANDOFF. Kamu salin ke `docs/HANDOFF.md` (paling atas) lalu commit.

## 6. Aturan agar tidak miskomunikasi

1. Satu istilah satu arti. Kamus istilah ada di GDD bagian "Glosarium". Pakai nama yang sama di kode dan dokumen (mis. `Plot`, `Crop`, `Harvest`).
2. Angka hanya hidup di satu tempat: tabel di spec/GDD -> dipindah ke `src/shared/` oleh Claude. Kalau ada selisih, tabel spec yang menang, kode harus diperbaiki.
3. Perubahan desain setelah `READY` = entri baru di DECISIONS + spec direvisi ke versi baru (`v2`), bukan edit diam-diam.
4. Kalau dua AI berbeda pendapat, kamu yang memutuskan, hasilnya dicatat di DECISIONS.
5. Setiap file spec dan keputusan memakai ID tetap (`FEAT-`, `D-`, `FIX-`, `Q-`).

## 7. Cadangan bila AI tidak bisa membuka GitHub

Kemampuan akses repo tiap AI bisa berbeda dan berubah. Kalau salah satu tidak bisa membuka repo:
- Tempel isi file yang relevan langsung ke chat (minimal: GDD, spec aktif, HANDOFF terbaru).
- Atau unggah zip repo ke chat.
- Setelah itu tetap commit hasilnya ke repo, supaya repo tetap yang paling baru.
