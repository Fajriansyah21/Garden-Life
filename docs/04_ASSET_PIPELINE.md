# 04 · Asset Pipeline

**Pemilik:** Kamu · Semua pihak boleh mengusulkan.

## 1. Masalah yang dipecahkan
Asset Roblox (model, gambar, suara) hidup di Roblox dengan **asset ID**, bukan sebagai file yang otomatis terbaca AI. Maka repo menyimpan **daftar (manifest)** berisi ID, nama, dan kegunaannya, supaya ChatGPT dan Claude merujuk asset yang sama.

## 2. Aturan penamaan

Format: `[Jenis]_[Kategori]_[Nama]_[Varian]` dalam `PascalCase` dipisah garis bawah.

| Jenis | Awalan | Contoh |
|---|---|---|
| Model 3D | `MDL_` | `MDL_Crop_Carrot_Stage1` |
| Tekstur | `TEX_` | `TEX_Soil_Dry` |
| UI / ikon | `UI_` | `UI_Icon_Coin` |
| Audio | `SFX_` / `MUS_` | `SFX_Harvest_Pop` |
| Animasi | `ANM_` | `ANM_Player_Water` |
| Partikel/efek | `FX_` | `FX_Sparkle_Harvest` |

## 3. ASSET_MANIFEST.md

Satu baris per asset di `assets/ASSET_MANIFEST.md`:

| Nama | Jenis | Roblox Asset ID | Sumber/Lisensi | Dipakai di | Status |
|---|---|---|---|---|---|
| `UI_Icon_Coin` | UI | `rbxassetid://[ISI]` | buatan sendiri | HUD (FEAT-004) | final |

Status: `placeholder` -> `wip` -> `final`.
Sumber/Lisensi wajib diisi: buatan sendiri, Toolbox (cek izin), atau lisensi lain.

## 4. Alur menambah asset

1. **Perancang** menulis kebutuhan asset di spec (nama, ukuran/gaya, jumlah varian).
2. **Kamu** membuat atau mengambil asset, mengunggah ke Roblox, mendapat Asset ID.
3. **Kamu** menambah baris ke `ASSET_MANIFEST.md` dan (opsional) menaruh file sumber di `assets/<jenis>/`.
4. **Engineer** merujuk asset memakai nama manifest. ID dipusatkan di satu modul (`src/shared/AssetIds.luau`), jangan tersebar di kode.
5. Selama asset belum ada, pakai `placeholder` (kotak/ikon sederhana) supaya pengerjaan tidak terhenti.

## 5. File sumber di repo
- Taruh file sumber (PNG, FBX, WAV, dll.) di `assets/<jenis>/` hanya bila ukurannya wajar.
- File besar: pakai Git LFS atau simpan di drive terpisah dan catat tautannya di manifest.
- Jangan commit file yang lisensinya tidak jelas.

## 6. File map
- Ekspor dari Studio ke `maps/` (`.rbxl` atau `.rbxlx`).
- `.rbxl` itu biner, jadi tidak bisa digabung otomatis. Aturan: **satu orang mengedit map pada satu waktu**, commit sering, tulis pesan jelas.
- Bagian yang bisa berupa kode/data harus ada di `src/`, bukan terkubur di dalam file map.
