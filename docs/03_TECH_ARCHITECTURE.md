# 03 · Arsitektur Teknis

**Pemilik:** Claude (Engineer) · **Versi:** 0.1

## 1. Prinsip
- **Server-authoritative:** server memegang kebenaran (uang, inventori, status tanaman). Client hanya meminta dan menampilkan.
- **Data-driven:** angka tuning ada di `src/shared/` (mis. `Config`, `CropData`). Mengubah balancing tidak boleh butuh mengubah logika.
- **Modul kecil:** satu modul satu tanggung jawab.
- **Aman-gagal:** error satu pemain tidak boleh menjatuhkan server.

## 2. Alat & versi
- Bahasa: Luau (`--!strict` bila memungkinkan)
- Sinkron: Rojo (`default.project.json`)
- Versi Rojo / alat lain: **[ISI saat setup]**

## 3. Pemetaan folder -> Roblox

| Folder repo | Lokasi di Studio |
|---|---|
| `src/shared/` | `ReplicatedStorage.Shared` |
| `src/server/` | `ServerScriptService.Server` |
| `src/client/` | `StarterPlayer.StarterPlayerScripts.Client` |

## 4. Modul rencana (diisi/direvisi Claude saat mengerjakan FEAT)

| Modul | Lokasi | Tanggung jawab |
|---|---|---|
| `Config` | shared | Konstanta global (batas, cooldown, mata uang awal) |
| `CropData` | shared | Tabel tanaman (dari spec FEAT-002) |
| `Remotes` | shared | Definisi RemoteEvent/Function terpusat |
| `PlayerData` | server | Muat/simpan DataStore, session lock, versi skema |
| `PlotService` | server | Kepemilikan & status lahan |
| `CropService` | server | Tanam, tumbuh, panen |
| `EconomyService` | server | Tambah/kurangi Coins, jual, beli (satu-satunya pintu uang) |
| `InputController` | client | Input & interaksi |
| `HudController` | client | UI uang, inventori, notifikasi |

## 5. Aturan jaringan (Remote)
- Semua remote didaftarkan di `Remotes` (satu tempat).
- Validasi di server: tipe argumen, nilai dalam batas, jarak pemain ke objek, cooldown, kepemilikan.
- Jangan pernah menerima nilai uang, jumlah, atau hasil dari client; hanya **niat** (mis. "panen plot 3").
- Batasi laju (rate limit) per pemain untuk setiap remote.

## 6. Data pemain
- Skema berversi: `SchemaVersion` di setiap profil.
- Jangan menghapus field lama tanpa migrasi.
- Simpan berkala (mis. tiap 60-120 dtk) dan saat keluar; retry dengan backoff bila DataStore gagal.
- Cegah dua server menulis profil yang sama (session lock).

Skema awal (diperbarui oleh Claude sesuai spec):

```lua
{
  SchemaVersion = 1,
  Coins = 0,
  Inventory = { Seeds = {}, Harvest = {} },
  Plots = {},
  Level = 1,
  XP = 0,
}
```

## 7. Performa
- Hindari loop per-frame untuk tanaman. Pakai timestamp tanam (`PlantedAt`) dan hitung tahap tumbuh dari selisih waktu.
- Batasi jumlah Instance aktif; gunakan pooling atau tampilkan hanya yang dekat.
- Uji di perangkat rendah (ponsel) sebelum rilis.

## 8. Pengujian
- Setiap fitur punya `tests/FEAT-XXX_checklist.md`: langkah uji manual di Studio + kasus tepi + kasus exploit.
- Uji multi-pemain (Studio: Test -> Clients and Servers).

## 9. Kebijakan dependensi
Library pihak ketiga hanya boleh masuk setelah dicatat di `DECISIONS.md` dan disetujui pemilik. Contoh kandidat yang dipertimbangkan nanti (belum diputuskan): library penyimpanan data, library UI.
