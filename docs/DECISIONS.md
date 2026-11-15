# DECISIONS · Log Keputusan

Aturan: **hanya ditambah, tidak dihapus.** Untuk mengubah keputusan, tulis entri baru yang menyebut "Menggantikan D-0xx".
Entri terbaru di paling atas.

## Format

```
### D-XXX · Judul singkat
- Tanggal:
- Diputuskan oleh: Pemilik / ChatGPT disetujui / Claude disetujui
- Status: Aktif / Digantikan oleh D-YYY
- Konteks: kenapa ini perlu diputuskan
- Keputusan: apa yang dipilih
- Alternatif yang ditolak: dan alasannya
- Dampak: ke desain / kode / asset
```

---

### D-001 · Repo GitHub sebagai sumber kebenaran
- Tanggal: [ISI]
- Diputuskan oleh: Pemilik
- Status: Aktif
- Konteks: Dua AI (ChatGPT dan Claude) bekerja di proyek yang sama dan perlu konteks yang identik.
- Keputusan: Semua dokumen, spec, kode, dan daftar asset disimpan di repo ini. Pembagian peran: ChatGPT = Perancang, Claude = Engineer, Pemilik = penyetuju.
- Alternatif yang ditolak: Menyalin konteks manual antar chat (rawan selisih).
- Dampak: Semua alur kerja mengikuti `00_WORKFLOW.md`.
