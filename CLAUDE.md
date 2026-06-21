# CLAUDE.md

AI assistantlar (Claude Code) uchun ushbu repozitoriy bo'yicha qo'llanma.
Oxirgi yangilanish: 2026-06-19.

---

## 1. Bu repo nima?

Bu **VEKTAN ishlab chiqarish/buxgalteriya otchotini to'ldirish** ishining
konteksti saqlanadigan repozitoriy. Bu yerda **dasturiy kod yo'q** — asosiy
mazmun markdown holatdagi ish konteksti (handoff) hisoblanadi. Maqsad:
egasi (Kamoliddin) telefon yoki kompyuterda Claude Code orqali ishni
**uzilishsiz davom ettira olishi**.

> ⚠️ Repo nomi `Supper-bot` bo'lsa-da, mazmuni VEKTAN otchot loyihasidir.
> «Bot yasash» asosiy maqsad EMAS — avval ma'lumot aniqlanadi va otchot
> to'ldiriladi (qarang: `CONTEXT.md`).

## 2. Fayllar tuzilishi

| Fayl | Vazifasi |
|---|---|
| `CLAUDE.md` | Shu fayl — AI assistant uchun yo'riqnoma + konvensiyalar. |
| `CONTEXT.md` | **Asosiy manba.** Loyiha maqsadi, data oqimi, barcha qoidalar (НМП rangi, lot kodi, massa-balans, distillyat), manbalar (Google Sheet ID'lari) va «KEYINGI QADAMLAR». Har doim shundan boshlang. |
| `DRAFT_bosh_smenalar.md` | Bo'sh smenalar uchun tayyorlangan qoralama (DRAFT) — asl Excel hali o'zgartirilmagan; tekshirish uchun. |
| `MARKALAR.md` | To'liq marka/nomenklatura ma'lumotnomasi (L1–L6 mahsulotlar, xomashyo, chiqindi turlari, oil/grease qaysi markada). |
| `YOMKOSTLAR.md` | Tanklar (ёмкости) kuzatuvi — uroven ko'z bilan (smena nachalnigi yozadi); distillyat tank ostatkasi farqidan hisoblanadi. |

Haqiqiy ish fayllari (Excel/Sheets) **bu repoda emas** — egasining Mac'ida
(`~/Downloads/...`) va Google Drive'da (`vektan-otchot` papka + Google
Sheets ID'lari). To'liq ro'yxat `CONTEXT.md` → «Fayllar / manbalar».

## 3. Ish boshlash tartibi (AI uchun)

1. **`CONTEXT.md` ni to'liq o'qing** — ayniqsa «Asosiy qoidalar»,
   «HOZIRGI HOLAT» va «KEYINGI QADAMLAR».
2. **`DRAFT_bosh_smenalar.md` ni o'qing** — qaysi smenalar allaqachon
   qoralama qilingani.
3. `CONTEXT.md` dagi «KEYINGI QADAMLAR» bo'limidan davom eting.
4. Yangi ma'lumot/qaror chiqsa — `CONTEXT.md` va kerak bo'lsa
   `DRAFT_*` ni **yangilang**, so'ng commit + push qiling (4-bo'lim).

## 4. Git workflow

- Ishlash branchi: **`claude/claude-md-docs-rvgin1`** (ko'rsatma berilgan branch).
- Push: `git push -u origin <branch>`. Tarmoq xatosida 2s/4s/8s/16s
  kechikish bilan 4 martagacha qayta urinib ko'ring.
- **Pull request YARATMANG** — egasi aniq so'ramaguncha.
- Commit xabarlari aniq va qisqa bo'lsin (masalan: «CONTEXT: 18-19
  Dewatering smenasi qo'shildi»).

## 5. Domen konvensiyalari (qisqacha — to'lig'i CONTEXT.md da)

- **Xomashyo:** НМП (qopда «LMP»). Rang: odatda **oq**; FC2/Красный →
  **sariq**; Bleached → **qора + bentanit**.
- **Lot kodi** `L131226`: partiya `131` + liniya `2` + yil `26`
  (FC=1, PR=2, POWDER=3).
- **Massa-balans:** `Расход = ИЧ + oil + grease + otx + musor + poteri`;
  `НМП = Расход − qayta ishlatilgan`. Otchotda НМП va Расход — formula
  (avtomat); INPUT faqat: ИЧ / oil / grease / otx / musor.
- **ИЧ** = shu smena ko'rsatkichi (kümulativ EMAS).
- **Distillyat (oil/grease)** faqat POWDER/VTS/VTR/VTR-118 da; mahsulot
  kg'дан chiqmaydi — tank ostatkasidan, operator yozmasa keyingi smena
  bilan moslanadi.
- **otx** = ишлаб чиqarиш chiqindisi (qayta ишлатилади); **musor** =
  to'kilgan LMP.
- Smena belgisi: «16--16» = kunduz, «16--17» = tun.
- Har bir lot kümulativ jami **tekshirilishi shart** (DRAFT'dagi ✓ kabi).

## 6. Eslatmalar / xavfsizlik

- Egasining maxfiy API kalitlari yoki paroli **hech qachon** so'ralmaydi
  va saqlanmaydi. GitHub token kerak bo'lsa — vaqtinchalik, ish tugagach
  o'chiriladi.
- Google Sheet ID'lari `CONTEXT.md` da; ularga MCP (Google Drive/Sheets)
  orqali kirish mumkin bo'lsa, asl jadval o'zgartirilishidan oldin egasi
  bilan tasdiqlang.
- Asl Excel/Sheets fayllar **avtomatik o'zgartirilmaydi** — avval DRAFT
  tayyorlanadi, egasi tekshiradi, keyin qo'llanadi.
