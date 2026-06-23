# Smena Otchot Bot — STRUKTURA (ma'lumot modeli)

> Holat: **dizayn bosqichi** (KOD YOZILMAYDI — avval struktura to'liq bo'ladi).
> Manba: Google Drive `smena_bot/STRUKTURA.md` + shu repodagi suhbat (2026-06-23).
> Oxirgi yangilanish: 2026-06-23.
> Bog'liq fayllar: `../MARKALAR.md` (markalar), `../YOMKOSTLAR.md` (tanklar),
> `../CONTEXT.md` (qoidalar), `HANDOFF.md`.

---

## 1. Bitta topshiriq (smena otchoti) tuzilmasi

### A. Sarlavha (smena ma'lumotlari) — bir marta so'raladi

| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `smena_turi` | tanlov | Den / Noch | **1-qadam** |
| `sana` | sana | 31.05.2026 | **2-qadam** |
| `vaqt_oraligi` | avtomat | — | sana + smena_turidan hisoblanadi |
| `boshlangich_uroven` | sikl | DI/R tanklar, ko'z bilan | **smena boshida** (B0-bo'lim) |
| `ishchilar.nachalnik` | son | 1 | начальник смены soni |
| `ishchilar.operator` | son | 3 | operator soni |
| `ishchilar.raznorabochiy` | son | 5 | разнорабочий soni |
| `brigada` | **avtomat** | A / B / C / D | smena grafikidan (sana + smena_turi) |
| `liniya` | tanlov | L1–L6 | mahsulot ro'yxatini belgilaydi |

**Vaqt oralig'i qoidasi (avtomat):**
- **Den:** sana 08:00 → sana 20:00 (obed 12:00–13:00 → 11 ish soat)
- **Noch:** sana 20:00 → (sana+1) 08:00 (obed 00:00–01:00 → 7 soat)
  - misol: 31.05.2026 (Noch) = 31.05 20:00 – 01.06 08:00

**Brigada qoidasi (avtomat):** `2026_4smena_grafik.xlsx`, list `ГРАФИК_2026`
(д=kunduz, Н=tun, bo'sh=выход). `(sana, smena_turi)` → brigada. Operator kiritmaydi.

### B0. Boshlang'ich uroven (smena boshida) — YANGI
Smena nachalnigi **ko'z bilan** tank urovenini yozadi (distillyat hisobi uchun).
| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `tank` | tanlov | DI-A (25) / R-5 ... | `../YOMKOSTLAR.md` registri |
| `uroven_boshi` | son | 40% / kg | ⚠️ birlik aniqlanadi (kg/%/belgi) |

### B. Mahsulotlar ro'yxati — 1 dan 6 tagacha takrorlanadi

| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `marka` | tanlov | VTR-118 | liniyaga mos ro'yxatdan (`../MARKALAR.md`) |
| `lot` | avtomat | L136226 | L + partiya + liniya + yil(26) |
| `miqdor_kg` (ИЧ) | son | 5000 | ishlab chiqarilgan kg |
| `vaqt_boshlanish` | vaqt | 09:00 | **majburiy** |
| `vaqt_tugash` | vaqt | 16:30 | **majburiy** |
| `qadoq_turi` | tanlov | 25 kg ko'k qop | ro'yxatdan (2-bo'lim) |
| `qop_soni` | avtomat | 20 | = miqdor_kg / qadoq birlik kg |
| `distillat_oil_kg` | son | 220 | har mahsulotdan (DI tank) |
| `distillat_griz_kg` | son | 95 | har mahsulotdan (DI tank) |
| `otx_kg` | son | 1650 | **Производственные чистий отходы** (Элак) |
| `musor_kg` | son | — | **Сортировочный мусор** |
| `chiqindi_kg` | son | — | **Отходы, не подлежащие переработке** |

> oil/griz va 3 chiqindi **har mahsulotga alohida** yoziladi.
> **oil/griz beradi:** L2 PR (VTR-110/114/118, VTS-114), L3 Powder (VT-110P, VTS-110P).
> **bermaydi (odatda):** FC, Flake, Bleached, Micronizer. **ZOROX-E 3326** — istisno (bo'lishi mumkin).
> ✅/❌ qattiq qoida emas — chiqsa, katakchaga yoziladi (`../MARKALAR.md`).

### C. Skladdan olingan xomashyo (НМП) — KIRISH, 1 dan N gacha
| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `siryo_nomi` | tanlov | НМП oq / sariq / qora | (+ ikkilamchi: otx/musor qaytgan) |
| `umumiy_kg` | son | 12000 | obshi kg |
| `qop_soni` | son | 24 | **kiritiladi** (mahsulotdan farqli) |

### D. Smena oxiri — YANGI
| Maydon | Tur | Izoh |
|---|---|---|
| `uroven_oxiri` | sikl | tank yakuniy uroven (ko'z bilan) |
| `toxtash` | tanlov | ишлаб чиqarиш bo'lmasa → sabab (3-bo'lim) |
| `rasm` | fayl | forma / tarozi surati (ixtiyoriy) |

---

## 2. Qadoq turlari ro'yxati (`../MARKALAR.md` dan)
| Qadoq turi | Birlik kg |
|---|---|
| Биг бег (big bag) | 500 |
| кўк қоп 25 кг | 25 |
| кўк қоп 20 кг | 20 |
| оқ қоп 25 кг | 25 |
| қизил қоп 25 кг | 25 |
| клариянт қоп 20 кг | 20 |
| қоғоз қоп 12 кг | 12 |
| қоғоз қоп 15 кг | 15 |
> Boshqa turlar chiqsa qo'shiladi.

## 3. Chiqindi va to'xtash ro'yxatlari (HAL QILINDI)
**3 chiqindi turi** (`../CONTEXT.md`):
1. **Производственные чистий отходы (otx)** — Элак, toza, qayta ishlanadi
2. **Сортировочный мусор (musor)** — to'kilgan LMP
3. **Отходы, не подлежащие переработке** — qayta ishlanmaydi (yo'qotish)

**To'xtash sabablari:** svet yo'q · gaz yo'q · сырьё yo'q · ремонт · boshqa ish

## 4. Avtomat hisoblanadigan qiymatlar
- `qop_soni` = miqdor_kg ÷ qadoq birlik kg
- `vaqt_oraligi` = smena_turi + sana qoidasi
- `lot` = L + partiya + liniya + 26
- `distillyat` = tank uroven farqi (boshi − oxiri, ko'z bilan → keyin moslanadi)
- `massa-balans` = Расход = ИЧ + oil + grease + otx + musor + poteri
- `tannarx` (себестоимость) = mehnat + xomashyo + energiya — ⏳ formula kerak

## 5. Natija (saqlash)
- Toza, tuzilgan yozuv → jadvalga (Google Sheets / Excel — ⏳ tanlanadi)
- Egaga (Kamoliddin) xabar; guruhdagi tartibsiz rasm muammosi yo'qoladi

## 6. Ochiq savollar (qoldi)
1. **Tannarx (mehnat) formulasi** — stavkalar (ish soat: kunduz 11, tun 7)
2. **Saqlash joyi** — Google Sheets / Excel / ikkalasi
3. **Kim ishlatadi** — faqat ega (sinov) yoki bir nechta brigadir
4. **Grafik fayl** — botga nusxa yoki Google Drive'dan o'qish
5. **Xomashyo kirish** — lot/partiya kerakmi yoki nomi+kg+qop yetarli
6. **Uroven birligi** — kg / % / belgi (tanklar uchun)

✅ **HAL QILINGAN:** brigada (avtomat), 3 chiqindi nomi, qadoq turlari,
distillyat markalar, tanklar ro'yxati, to'xtash sabablari.
