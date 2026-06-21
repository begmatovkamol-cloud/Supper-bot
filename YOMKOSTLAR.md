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

## Aniqlanishi kerak (egasidan)

1. **Tank nomlari/soni** (masalan: DI-A, DI-B, № 1/2/3...).
2. **Uroven nimaда yoziladi:** kg, foiz (%), yoki tankdagi belgi (sm)?
3. Har tankда **nima bor:** oil, grease, xomashyo (LMP), yoki suyuq mum?
