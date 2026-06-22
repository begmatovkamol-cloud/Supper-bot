# VEKTAN — Ёмкостlar (tanklar) kuzatuvi

> Distillyat (oil/grease) mahsulot kg'дан emas, **tank ostatkasi farqidan** chiqadi.
> Tuzildi: 2026-06-21.

## Qanday o'lchanadi (muhim)

- Uroven (ostatok) **ko'z bilan (vizual)** baholanadi — **smena nachalnigi** ko'rib yozadi.
- Shuning uchun har smena ko'rsatkichi **taxminiy**.
- **Aniqlash:** tank **bo'shaганда / to'lganда** haqiqiy kg ma'lum bo'ladi →
  oradagi smenalar distillyati **shu aniq raqamga moslanadi** (reconcile).
- Operator yozmagan smena → **keyingi smena bilan moslanadi** (CONTEXT qoidasi).

## Hisoblash mantig'i

```
Smena distillyati ≈ (smena boshidagi uroven + qo'shilgan) − ketish vaqtidagi uroven
Tank bo'shaганда   → aniq jami = moslab taqsimlanadi (smenalar bo'yicha)
```

## Kuzatuv shabloni (har smena uchun to'ldiriladi)

| Smena | Tank | Ichidagi material | Smena boshi uroven | Ketish uroven | Chiqqan (≈) | Izoh |
|---|---|---|---|---|---|---|
| 16--17 | ? | oil / grease / xomashyo | ? | ? | ? | ko'z bilan |
| 17--17 | ? | | ? | ? | ? | |
| 17--18 | ? | | ? | ? | ? | |

> ⏳ Tank nomlari, o'lchov birligi (kg / % / belgi) va boshlang'ich urovenlar
> egasidan kelgach to'ldiriladi.

## Tanklar ro'yxati (registr)

> Hajm — **куб (m³)**. «Ichida nima» va uroven birligi egasi har biri bo'yicha
> aniqlab bergach to'ldiriladi.

| Guruh | Tank | Hajm (m³) | Ichida (nima) |
|---|---|---|---|
| **M** (yuklash/мешалка?) | M-100 | 10 | xomashyo (сырьё) |
| | M-200 | 10 | xomashyo (сырьё) |
| **HV** | HV-100 | 4 | xomashyo (сырьё) |
| | HV-200 | 4 | xomashyo (сырьё) |
| **R** (reaktor) | R-1 | 5.5 | xomashyo (сырьё) |
| | R-2 | 5.5 | xomashyo (сырьё) |
| | R-3 | 5 | xomashyo (сырьё) |
| | R-4 | 5 | xomashyo (сырьё) |
| | R-5 | 15 | xomashyo (сырьё) |
| **DI** (distillyat) | DI-A (katta) | 25 | oil yoki grease |
| | DI-B (katta) | 25 | oil yoki grease |
| | DI-A (o'rta) | 8.2 | oil yoki grease |
| | DI-B (o'rta) | 8.2 | oil yoki grease |
| | DI-A (kichik) | 3.5 | oil yoki grease |
| | DI-B (kichik) | 3.5 | oil yoki grease |

> ⚠️ DI-A va DI-B nomlari **3 xil hajmда takrorlanadi** (25 / 8.2 / 3.5 m³) —
> ularni ajratish uchun hajmni ham yozib boramiz.
> **DI tankда istalganida oil yoki grease bo'lishi mumkin** (qattiq biriktirilmagan).
> **M / HV / R tanklarида — xomashyo (сырьё).**

## Aniqlanishi kerak (egasidan)

1. **Uroven nimaда yoziladi:** kg, foiz (%), yoki tankdagi belgi (sm)?
2. Boshlang'ich (hozirgi) urovenlar.
