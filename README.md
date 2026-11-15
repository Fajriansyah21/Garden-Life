# Garden Life

Map Roblox bertema pertanian. Repo ini adalah **satu-satunya sumber kebenaran** (single source of truth) untuk tiga pihak:

| Peran | Siapa | Tugas utama |
|---|---|---|
| Produser / pemilik | Kamu | Memutuskan arah, menyetujui spec, menguji di Roblox Studio |
| Perancang (Designer) | ChatGPT | Menulis GDD, spec fitur, balancing, analisis |
| Engineer | Claude | Mengubah spec jadi kode Luau, review, menandai spec yang ambigu |

Aturan emas: **kalau tidak tertulis di repo, dianggap belum diputuskan.**

## Struktur folder

```
farm-roblox/
├── README.md                    <- kamu di sini
├── default.project.json         <- konfigurasi Rojo (sinkron kode ke Studio)
├── docs/
│   ├── ai/
│   │   ├── CHATGPT_DESIGNER_INSTRUCTIONS.md   <- tempel ke ChatGPT
│   │   └── CLAUDE_ENGINEER_INSTRUCTIONS.md    <- tempel ke Claude Project
│   ├── 00_WORKFLOW.md           <- alur kerja & fase proyek
│   ├── 01_DESIGN_ANALYSIS_SYSTEM.md  <- cara menganalisis desain & ekonomi
│   ├── 02_GAME_DESIGN_DOCUMENT.md    <- GDD (milik ChatGPT)
│   ├── 03_TECH_ARCHITECTURE.md  <- arsitektur kode (milik Claude)
│   ├── 04_ASSET_PIPELINE.md     <- aturan asset & penamaan
│   ├── DECISIONS.md             <- log keputusan (jangan dihapus, hanya ditambah)
│   ├── HANDOFF.md               <- catatan serah-terima antar AI
│   ├── design/                  <- spec fitur (satu file per fitur)
│   │   └── _TEMPLATE_FEATURE_SPEC.md
│   └── specs/                   <- spec teknis hasil turunan (opsional)
├── src/
│   ├── server/                  <- skrip server (otoritatif)
│   ├── client/                  <- skrip client (UI, input, efek)
│   └── shared/                  <- modul bersama + data config (Config, CropData)
├── assets/
│   ├── ASSET_MANIFEST.md        <- daftar asset + Roblox asset ID
│   ├── models/  textures/  audio/  ui/
├── maps/                        <- file .rbxl / .rbxlx hasil ekspor Studio
├── tests/                       <- tes & checklist playtest
└── tools/                       <- skrip bantu (opsional)
```

## Cara mulai (urutan)

1. Buat repo di GitHub, upload isi folder ini.
2. Buka `docs/ai/CHATGPT_DESIGNER_INSTRUCTIONS.md` -> tempel ke ChatGPT (Project Instructions atau Custom GPT).
3. Buka `docs/ai/CLAUDE_ENGINEER_INSTRUCTIONS.md` -> tempel ke Claude (Project Instructions).
4. Isi bagian **[ISI]** di `docs/02_GAME_DESIGN_DOCUMENT.md` bersama ChatGPT.
5. Ikuti `docs/00_WORKFLOW.md`.

## Alat yang disarankan

- [Rojo](https://rojo.space) untuk sinkron file `src/` ke Roblox Studio.
- Bahasa: **Luau**.
- Git untuk versi. `maps/*.rbxl` berupa biner, jadi hindari dua orang mengedit bersamaan.
