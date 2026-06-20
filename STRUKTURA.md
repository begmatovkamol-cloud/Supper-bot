# Smena Otchot Bot — struktura (ma'lumot modeli)

> Holat: dizayn bosqichi. `???` va «to'ldiriladi» belgilangan joylarni birga to'ldiramiz.
> Oxirgi yangilanish: 2026-06-21.

## 1. Bitta topshiriq (smena otchoti) tuzilmasi

### A. Sarlavha (smena ma'lumotlari) — bir marta so'raladi

| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `smena_turi` | tanlov | Den / Noch | **1-qadam**, birinchi so'raladi |
| `sana` | sana | 31.05.2026 | **2-qadam** |
| `vaqt_oraligi` | avtomat | — | sana va smena_turi dan hisoblanadi (pastga qarang) |
| `ishchilar.nachalnik` | son | 1 | начальник смены soni |
| `ishchilar.operator` | son | 3 | operator soni |
| `ishchilar.raznorabochiy` | son | 5 | разнорабочий soni |
| `brigada` | **avtomat** | A / B / C / D | smena grafikidan: sana + smena_turi → brigada |
| `liniya` | tanlov | L1–L6 | mahsulot ro'yxatini belgilaydi |

**Vaqt oralig'i qoidasi (avtomat):**
- **Den:**  sana 08:00  →  sana 20:00  (obed 12:00–13:00 → 11 ish soat)
- **Noch:** sana 20:00  →  (sana + 1 kun) 08:00  (obed 00:00–01:00 → tunги 7 soat)
  - misol: 31.05.2026 (Noch) = 31.05.2026 20:00 – 01.06.2026 08:00

**Brigada qoidasi (avtomat — smena grafikidan):**
- Manba fayl: `2026_4smena_grafik.xlsx`, list `ГРАФИК_2026` (д=kunduz, Н=tun, bo'sh=выход).
- Har kuni aniq 1 brigada kunduz, 1 brigada tun. Misol 01.01.2026: A=kunduz, B=tun.
- Bot: `(sana, smena_turi)` → grafikdan brigadani topadi. Operator brigadani kiritmaydi.
- ❓ Grafik fayli botga nusxa qilib qo'yiladimi yoki to'g'ridan Google Drive'dan o'qiydimi.

### B. Mahsulotlar ro'yxati — 1 dan 6 tagacha takrorlanadi

Bitta smenada bir nechta (5–6) xil mahsulot chiqishi mumkin. Har biri uchun:

| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `marka` | tanlov | VTR-118 | liniyaga mos ro'yxatdan |
| `lot` | avtomat | L136226 | L + partiya + liniya + yil(26) |
| `miqdor_kg` | son | 5000 | ishlab chiqarilgan kg |
| `vaqt_boshlanish` | vaqt | 09:00 | **majburiy** |
| `vaqt_tugash` | vaqt | 16:30 | **majburiy** |
| `qadoq_turi` | tanlov | 25 kg ko'k qop | ro'yxatdan (3-bo'lim) |
| `qop_soni` | avtomat | 20 | = miqdor_kg / qadoq birlik kg (kiritilmaydi) |
| `distillat_oil_kg` | son | 220 | har mahsulotdan ajraladigan distillat oil |
| `distillat_griz_kg` | son | 95 | har mahsulotdan ajraladigan distillat griz (grease) |
| `otxod_1_kg` | son | — | ??? 1-otxod nomi to'ldiriladi |
| `otxod_2_kg` | son | — | ??? 2-otxod nomi to'ldiriladi |
| `otxod_3_kg` | son | — | ??? 3-otxod nomi to'ldiriladi |

> Eslatma: oil/griz va 3 otxod **har mahsulotga alohida** yoziladi (smena umumiy emas).
> FC / Bleached kabi liniyalarda oil/griz = 0 bo'lishi mumkin (loyiha qoidasi — tekshiriladi).

### C. Skladdan olingan xomashyo (НМП) — KIRISH, 1 dan N gacha takrorlanadi

Smenada skladdan qancha xomashyo (сырьё) olib kirilgani. Massa-balans uchun zarur.
Bir nechta xil bo'lishi mumkin, har biri uchun:

| Maydon | Tur | Misol | Izoh |
|---|---|---|---|
| `siryo_nomi` | tanlov | НМП oq / sariq / qora | ??? to'liq ro'yxat to'ldiriladi |
| `umumiy_kg` | son | 12000 | obshi kg |
| `qop_soni` | son | 24 | **kiritiladi** (mahsulotdan farqli) |

> Eslatma: mahsulot (CHIQISH)da qop soni avtomat; xomashyo (KIRISH)da qop soni qo'lda kiritiladi.

### D. Qo'shimcha (smena bo'yicha) — ixtiyoriy

| Maydon | Tur | Izoh |
|---|---|---|
| `rasm` | fayl | forma / tarozi surati (ixtiyoriy) |

> oil/griz va 3 otxod endi **mahsulot darajasida** (B-bo'lim), smena darajasida emas.

## 2. Qadoq turlari ro'yxati (TO'LDIRILADI)

Hozircha ma'lum:
- 25 kg ko'k qop  → birlik 25 kg
- 500 kg big bag → birlik 500 kg
- 25 kg oq qop   → birlik 25 kg
- ??? (boshqa turlar keyin qo'shiladi)

## 3. Avtomat hisoblanadigan qiymatlar

- **`qop_soni`** = miqdor_kg ÷ qadoq birlik kg
- **`vaqt_oraligi`** = smena_turi + sana qoidasi
- **`lot`** = L + partiya + liniya + 26
- **`tannarx` (себестоимость)** = mehnat (ishchilar soni × ???) + xomashyo (НМП × ???) + energiya (???)
  - mehnat formulasi: TO'LDIRILADI (har lavozim stavkasi yoki umumiy fond?)
- **massa-balans** = ишлаб чиqarиш ↔ расход (loyiha qoidalari bo'yicha)

## 4. Natija (saqlash)

- Toza, tuzilgan yozuv → jadvalga (Google Sheets / Excel — ??? tanlanadi)
- Egaga (Kamoliddin) xabar
- Guruhdagi tartibsiz rasm/izoh muammosi yo'qoladi

## 5. Ochiq savollar (keyin hal qilamiz)

1. Qadoq turlarining to'liq ro'yxati
2. Tannarx (mehnat) formulasi — stavkalar (ish soat ma'lum: kunduz 11, tun 7)
3. ~~Brigada~~ ✅ HAL: avtomat — smena grafikidan (sana + smena_turi)
4. Saqlash joyi: Google Sheets yoki Excel yoki ikkalasi
5. Kim ishlatadi: faqat ega (sinov) yoki bir nechta brigadir
6. Grafik faylni botga nusxalaymizmi yoki Google Drive'dan o'qiymizmi
