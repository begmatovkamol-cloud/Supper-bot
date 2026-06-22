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
| **M** (yuklash/мешалка?) | M-100 | 10 | ? |
| | M-200 | 10 | ? |
| **HV** | HV-100 | 4 | ? |
| | HV-200 | 4 | ? |
| **R** (reaktor) | R-1 | 5.5 | ? |
| | R-2 | 5.5 | ? |
| | R-3 | 5 | ? |
| | R-4 | 5 | ? |
| | R-5 | 15 | ? |
| **DI** (distillyat) | DI-A (katta) | 25 | oil/grease? |
| | DI-B (katta) | 25 | oil/grease? |
| | DI-A (o'rta) | 8.2 | oil/grease? |
| | DI-B (o'rta) | 8.2 | oil/grease? |
| | DI-A (kichik) | 3.5 | oil/grease? |
| | DI-B (kichik) | 3.5 | oil/grease? |

> ⚠️ DI-A va DI-B nomlari **3 xil hajmда takrorlanadi** (25 / 8.2 / 3.5 m³) —
> ularni ajratish uchun hajmni ham yozib boramiz.

## Aniqlanishi kerak (egasidan)

1. Har tankда **nima bor:** oil, grease, xomashyo (LMP), suyuq mum, reaktor mahsuloti?
   (Ayniqsa: qaysi DI tank **oil**, qaysi biri **grease**?)
2. **Uroven nimaда yoziladi:** kg, foiz (%), yoki tankdagi belgi (sm)?
3. Boshlang'ich (hozirgi) urovenlar.
