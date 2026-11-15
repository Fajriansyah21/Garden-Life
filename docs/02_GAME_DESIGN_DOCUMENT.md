# 02 · Game Design Document (GDD)

**Pemilik:** ChatGPT (Perancang) · **Penyetuju:** Kamu
**Versi:** 0.1 · **Terakhir diubah:** [ISI]

> Bagian bertanda **[ISI]** diisi bersama ChatGPT di Fase 0-1. Jangan biarkan kosong saat fitur terkait mulai dikerjakan.

## 1. Visi
- Satu kalimat pitch: **[ISI]**
- Rasa utama yang ingin dirasakan pemain (mis. santai, memuaskan, kompetitif): **[ISI]**
- Game referensi (3): **[ISI]**

## 2. Target pemain
- Usia & perangkat dominan: **[ISI]**
- Solo / multiplayer / co-op: **[ISI]**
- Panjang sesi yang diharapkan: **[ISI]**

## 3. Core loop
Lihat `01_DESIGN_ANALYSIS_SYSTEM.md` bagian 2. Versi final untuk game ini: **[ISI]**

## 4. Sistem utama (isi satu per satu; tiap sistem -> satu atau lebih FEAT)

| Sistem | Ringkasan | Prioritas (M/S/C/W) | Spec |
|---|---|---|---|
| Lahan (Plot) | [ISI] | M | FEAT-001 |
| Tanaman (Crop) | [ISI] | M | FEAT-002 |
| Panen & Jual | [ISI] | M | FEAT-003 |
| Toko bibit | [ISI] | M | FEAT-004 |
| Progres (level/XP) | [ISI] | S | - |
| Upgrade lahan & alat | [ISI] | S | - |
| Hewan ternak | [ISI] | C | - |
| Quest / hadiah harian | [ISI] | C | - |
| Sosial (kunjungi, trade) | [ISI] | C/W | - |

## 5. Ekonomi
- Mata uang utama: **[ISI]**
- Mata uang kedua (jika ada): **[ISI]**
- Tabel tanaman: lihat spec FEAT-002 (angka tuning di `src/shared/CropData.luau`)
- Sink & source utama: **[ISI]**

## 6. Dunia / Map
- Tema visual & suasana: **[ISI]**
- Ukuran area & zona (kebun, toko, area sosial, dll.): **[ISI]**
- Jumlah pemain per server: **[ISI]**

## 7. UI / UX
- Layar utama (HUD): **[ISI]**
- Menu: inventori, toko, pengaturan: **[ISI]**
- Prinsip: besar, jelas, ramah sentuhan.

## 8. Monetisasi
- Strategi: **[ISI]** (Game Pass / Developer Product / tanpa monetisasi)
- Batas adil: pemain gratis tetap bisa maju. **[ISI detail]**

## 9. Cakupan per fase (MVP -> rilis)
- **Vertical Slice:** FEAT-001 .. FEAT-004
- **Rilis 1.0:** **[ISI]**
- **Pasca-rilis:** **[ISI]**

## 10. Glosarium (satu istilah, satu arti, dipakai juga di kode)

| Istilah | Arti | Nama di kode |
|---|---|---|
| Plot | Satu petak lahan tanam | `Plot` |
| Crop | Jenis tanaman | `Crop` |
| Seed | Bibit yang dibeli | `Seed` |
| Harvest | Hasil panen di inventori | `Harvest` |
| Coins | Mata uang utama | `Coins` |
| **[ISI]** | | |

## 11. Risiko & pertanyaan terbuka
Lihat `HANDOFF.md` dan `DECISIONS.md`. Daftar di sini hanya yang bersifat desain besar.
