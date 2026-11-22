# Shared Weather & Status Specification (Garden Life)

## 1. Shared Weather Table
| Cuaca | Δ WaterLevel | Modifier Tumbuh | Mutation Main | Special Rules |
|---|---|---:|---|---|
| **Sunny** | 0,000 | 1,0× | — | Base weather |
| **Cloudy** | +0,250 (1×) | 1,0× (Sun-loving 0,85×) | — | Transisi |
| **Windy** | -0,005 (tiap 2t) | 1,5× | — | Angin sepoi |
| **Drizzle** | +0,050 / tick | 0,85× | Wet (2,5%) | Hujan ringan |
| **Rainy** | +0,075 / tick | 0,80× | Wet (2,5%), Flooded (2,5%) | Hujan deras |
| **Misty** | +0,250 (1×) | 0,85× | Misty (6,697%), Foggy (0,809%) | Foggy evolusi |

- 1 tick = 30 detik.
- Multiplier Wet global = 2,5%/tick.

## 2. Status Priority
```text
Dead > Uprooted > Rest > Frozen > Frosted > Overwatered > Blocked > Windblown > Normal
```

## 3. Rules Matrix
- **Rest:** WaterLevel freeze, kebal mutasi/cuaca, butuh Season Pill/Greenhouse/musim cocok.
- **Frozen:** Butuh Heater (salju hilang tidak menghapus Frozen).
- **Uprooted:** Menyimpan status lama (Blocked/Frosted/Windblown). Trowel tanam ulang.
- **Greenhouse:** Masih bisa Overwatered. Kebal badai/mutasi/Rest.
- **Meltwater:** 1 Snow Block -> 5 min -> Meltwater Bottle (+1,000 WaterLevel). Dilarang saat Overwatered.
