# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

> AI assistantlar (Claude Code) uchun ushbu repozitoriy bo'yicha qo'llanma.
> Oxirgi yangilanish: 2026-06-21.

---

## 1. Bu repo nima?

Bu **VEKTAN TRADING** (mum/parafin ishlab chiqarish, Toshkent) ishlari
konteksti saqlanadigan **hujjat (handoff) repozitoriysi**. Bu yerda hozircha
**dasturiy kod yo'q** — build/test/lint buyruqlari, paket fayllari yo'q.
Mazmun butunlay markdown holatdagi ish konteksti. Maqsad: egasi
(Kamoliddin, Бегматов К.А.) telefon yoki kompyuterda Claude Code orqali ishni
**uzilishsiz davom ettira olishi**.

> ⚠️ Repo nomi `Supper-bot`. Ichida ikki bog'liq yo'nalish bor (pastga qarang).

Repoda **ikki ish yo'nalishi** bor:

1. **Smena Otchot Bot — dizayn (HOZIRGI faol ish, 2026-06-21).**
   Operator/brigadirlar smena tugagach botga **tuzilgan** otchot topshiradigan
   Telegram bot. Hozir **faqat dizayn/struktura** tuzilmoqda — **KOD HALI
   YOZILMAYDI**, hammasi tayyor bo'lgach boshlanadi. Manba: `HANDOFF.md`,
   `STRUKTURA.md`.
2. **VEKTAN buxgalteriya otchotini to'ldirish (oldingi ish).**
   Telegram guruh ma'lumotini buxgalteriya otchotiga aniq ko'chirish.
   Manba: `CONTEXT.md`, `DRAFT_bosh_smenalar.md`.

Ikkala yo'nalish ham bir domen (VEKTAN ishlab chiqarish) ustida; qoidalar
(lot kodi, massa-balans, distillyat va h.k.) umumiy.

## 2. Fayllar tuzilishi

| Fayl | Yo'nalish | Vazifasi |
|---|---|---|
| `CLAUDE.md` | — | Shu fayl — AI uchun yo'riqnoma + konvensiyalar. |
| `HANDOFF.md` | Bot | Botni davom ettirish uchun kirish nuqtasi: loyiha tavsifi, wizard oqimi, egadan so'raladigan checklist. |
| `STRUKTURA.md` | Bot | **Botning asosiy hujjati** — ma'lumot modeli (smena otchoti maydonlari, avtomat hisoblar, ochiq savollar). `???` belgilangan joylar to'ldiriladi. |
| `CONTEXT.md` | Otchot | Buxgalteriya otchoti ishining to'liq konteksti: data oqimi, barcha domen qoidalari, manbalar (Google Sheet ID'lari), «HOZIRGI HOLAT» + «KEYINGI QADAMLAR». |
| `DRAFT_bosh_smenalar.md` | Otchot | Bo'sh smenalar uchun qoralama + «buxgalteriyaga ko'chirishga tayyor» jadval. |

Haqiqiy ish fayllari (Excel/Sheets, grafik, bot kodi) **bu repoda emas** —
egasining Mac'ida (`~/Downloads/...`, `/Users/kamoliddin/smena_bot/`) va
Google Drive'da. To'liq ro'yxat tegishli faylda.

## 3. Ish boshlash tartibi (AI uchun)

**Bot dizayni ustida ishlayotgan bo'lsang (hozirgi asosiy ish):**
1. `HANDOFF.md` → `STRUKTURA.md` ni to'liq o'qing.
2. Egadan (Kamoliddin) `STRUKTURA.md` dagi `???` / «TO'LDIRILADI» va
   `HANDOFF.md` dagi checklist'ni so'rab to'ldiring.
3. Har yangilanishda **`STRUKTURA.md` ni qayta yozib qo'y** (sana yangilansin).
4. **KOD YOZMA** — bu hali dizayn bosqichi.

**Buxgalteriya otchoti ustida ishlayotgan bo'lsang:**
1. `CONTEXT.md` ni to'liq o'qing («Asosiy qoidalar», «HOZIRGI HOLAT»,
   «KEYINGI QADAMLAR») → keyin `DRAFT_bosh_smenalar.md`.
2. «KEYINGI QADAMLAR» dan davom eting; yangilik chiqsa fayllarni yangilang.

> Bu repo'da ishlash = markdown hujjatlarini o'qish/yangilash.
> Test yoki build yugurtirish kerak EMAS (ular mavjud emas).

## 4. Git workflow

- Ishlash branchi: seans ko'rsatmasidagi branch
  (joriy: **`claude/claude-md-docs-esm1m4`**). Egasining ruxsatisiz
  boshqa branchga push QILMANG.
- Push: `git push -u origin <branch>`. Tarmoq xatosida 2s/4s/8s/16s
  kechikish bilan 4 martagacha qayta urinib ko'ring.
- **Pull request YARATMANG** — egasi aniq so'ramaguncha.
- Commit xabarlari aniq va qisqa (mas: «STRUKTURA: qadoq turlari to'ldirildi»).

## 5. Domen konvensiyalari (qisqacha — to'lig'i CONTEXT.md / STRUKTURA.md da)

- **Liniyalar↔mahsulot:** L1 FC (VT-110), L2 PR (VTR/VTS), L3 Powder,
  L4 Flake, L5 Micronizer (VTMX), L6 Dewatering (Безвоз порошок, LMP-siz).
- **Xomashyo:** НМП (qopда «LMP»). Rang: odatda **oq**; FC2/Красный →
  **sariq**; Bleached → **qора + bentanit**.
- **Lot kodi** `L131226`: `L` + partiya `131` + liniya `2` + yil `26`
  (FC=1, PR=2, POWDER=3).
- **Massa-balans:** KIRISH (НМП) ≈ CHIQISH (mahsulot) + otxodlar + oil + griz.
  Otchotda: `Расход = ИЧ + oil + grease + otx + musor + poteri`;
  `НМП = Расход − qayta ishlatilgan`. INPUT faqat: ИЧ / oil / grease / otx / musor.
- **ИЧ** = shu smena ko'rsatkichi (kümulativ EMAS).
- **Distillyat (oil/grease)** faqat POWDER/VTS/VTR/VTR-118 da (FC & Bleached=0);
  mahsulot kg'дан chiqmaydi — tank ostatkasidan; operator yozmasa keyingi
  smena bilan moslanadi.
- **otx** = ишлаб чиqarиш chiqindisi (qayta ишлатилади); **musor** = to'kilgan LMP.
- **Smena:** Den (kunduz, 08:00–20:00, 11 soat) / Noch (tun, 20:00–ertasi
  08:00, 7 soat). Otchot belgisi: «16--16» = kunduz, «16--17» = tun.
- **Brigada — avtomat:** smena grafikidan (`(sana, smena_turi)` → brigada),
  operator kiritmaydi. Manba: `2026_4smena_grafik.xlsx`, list `ГРАФИК_2026`.
- Har bir lot kümulativ jami **tekshirilishi shart** (DRAFT'dagi ✓ kabi).

## 6. Eslatmalar / xavfsizlik

- Egasining maxfiy API kalitlari yoki paroli **hech qachon** so'ralmaydi va
  saqlanmaydi. GitHub token kerak bo'lsa — vaqtinchalik, ish tugagach o'chiriladi.
- Google Sheet/Drive ID'lari hujjatlarda; ularga MCP (Google Drive/Sheets)
  orqali kirish mumkin bo'lsa, asl jadval o'zgartirilishidan oldin egasi bilan
  tasdiqlang.
- Asl Excel/Sheets fayllar **avtomatik o'zgartirilmaydi** — avval DRAFT
  tayyorlanadi, egasi tekshiradi, keyin qo'llanadi.
