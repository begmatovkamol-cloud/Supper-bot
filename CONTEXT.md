# VEKTAN Otchot — Ish konteksti (Claude Code handoff)

> Telefon/Claude orqali davom ettirish uchun to'liq holat. Oxirgi yangilanish: 2026-06-19.

## Maqsad
VEKTAN TRADING (mum/parafin, Toshkent) ishlab chiqarish hisobotini avtomatlashtirish:
Telegram guruh ma'lumotini **buxgalteriya otchotiga** aniq ko'chirish → oylik balansga.
Ega: **Kamoliddin (Бегматов К.А.)**. **Bot yasash YO'Q** — avval ma'lumotni aniq qilib, otchot to'ldiriladi.

## Tizim / data oqimi
> Vizual sxema: `struktura.png` (repo ildizida).
```
Telegram guruh «VEKTAN Production L1–L6 | Фото + кг» (forum, har tema=liniya)
 + balans formalari (rasm)
 ↓
«Сменалар таҳлили» (har smena: produced + oil/grease + sotuv + ishchi)
 ↓                          ↓
«Деталний/Кунлик отчёт»     БУХГАЛТЕРИЯ ОТЧЁТ (massa-balans)
 (остатки)
 ↓
Dashboard (liniya yakuni + «Назорат» auto-tekshiruv)
```

## Liniya ↔ mahsulot
| Liniya | Mahsulot |
|---|---|
| L1 FC | VT-110 (FC1/FC2/FCS) |
| L2 PR | VTR-110/114/118, VTS-114 |
| L3 Powder | POWDER VT-110 |
| L4 Flake | FLAKE VT-110 |
| L5 Micronizer | VTMX (118) — VTR-118'dan ishlanadi |
| L6 Dewatering | Безвоз порошок (LMP solinmaydi) |

## Asosiy qoidalar (o'rganilgan, dalillangan)
- **Xomashyo:** НМП (qopда «LMP»). Rang: asosan **oq**; FC2/Красный→**sariq**; Bleached→**qора + bentanit**.
- **Lot kodi:** `L131226` = partiya 131 + liniya 2 + yil 26. (FC=1, PR=2, POWDER=3)
- **Massa-balans (formula otchotда avtomat):** `Расход = ИЧ + oil + grease + otx + musor + poteri`; `НМП = Расход − qayta ишлатилган`.
- **Distillyat (oil/grease)** beradigan markalar: **VT-110P (POWDER), VTS-114, VTR-114, VTR-118** (FC=VT-110 & Bleached=0). Har markada miqdor **har xil**. Mahsulot kg'дан CHIQMAYDI — tank ostatkasidан (DI-A/DI-B), «Сменалар таҳлили»да. Operator yozmasa → **keyingi smena bilan moslanadi**.
- **otx** = Производственные отходы (elak toza chiqindi, qayta ишлатилади, 3-sort). **musor** = Сортировочный (to'kilgan LMP).
- **ИЧ = shu smena ko'rsatkichi** (kümulativ emas).
- **FC=FCS** bir xil marka; ombor balansiga qarab tanlanadi.
- Samara (НМП/1kg): FC 1.00 · POWDER 1.11 · VTR-114 1.25 · VTS 1.29 · VTR-118 1.52 · Bleached 1.63.

## Smena ish tsikli (boshidan oxirigacha)
> Vizual: `struktura.png`.
1. **Smena boshlanadi** («16--16» kunduz / «16--17» tun) — nachalnik qabul qiladi,
   **boshlang'ich uroven (ko'z bilan)** va ostatkilarni yozadi.
2. **Xomashyo tayyorlash** — НМП/LMP skladdan (zayavka) → tanklarga (M/HV/R).
3. **Ишлаб чиqarиш** (L1–L6). To'xtasa → **sabab** (svet/gaz/сырьё yo'q, ремонт, boshqa ish).
4. **Natija** — mahsulot (kg, lot) · distillyat (DI-A/DI-B → oil/grease) · chiqindi (otx/musor).
5. **Smena oxiri** — yakuniy uroven (ko'z bilan), mahsulot skladga topshirish, sotuv/otgruzka.
6. **Uzatish/hisobot** — Telegram (foto+kg) → buxgalteriya otchot (massa-balans) → Назорат.
→ keyingi smenaga uzatiladi (tsikl takrorlanadi).

## Простой — ishlab chiqarish to'xtash sabablari
Smenada ишлаб чиqarиш **bo'lmaganда**, otchotга/izohга **sabab** yoziladi:
- **Svet yo'q** (elektr uzilgan)
- **Gaz yo'q**
- **Сырьё (xomashyo) yo'q**
- **Ремонт** (ta'mirlash)
- **Boshqa ish** (uborka, qoplarni topshirish, sovitish va h.k.)
- Boshqa sabab (qo'lда yoziladi)

> DRAFT'дagi misol: «18--18 Den-4: Ишлаб чиqarиш yo'q (Dewatering sovitish)»,
> «19--19 Den-5: Ишлаб чиqarиш yo'q (uborka)».

## Fayllar / manbalar
- Buxgalteriya otchoti (lokal Mac): `~/Downloads/2026_Июнь_Производственный_отчет_для_бухгалтерии_7.xlsx`
  (63 blok: 1-chi Итого, qolgan har smena «16--16»=kunduz, «16--17»=tun. INPUT: ИЧ/oil/grease/otx/musor; НМП·Расход=formula.)
- To'ldirilган nusxa: `~/Downloads/2026_Июнь_otchot_TOLDIRILDI.xlsx`
- Oylik smena otчёт: `~/Downloads/Июнь_2026_–_Сменный_производственный_отчет_1.xlsx` (oil/grease + остатки)
- Google Sheets:
  - Katta sklad (tayyor mahsulot+НМП kunlik): `14FVp93uWOO031AX-Yhp1qytxE5jaxxd2zbzAIqGifvs`
  - Sotuv (eksport otgruzka + ichki bozor zakaz): `1PBigBhGeNMdqRCJXfG6LrRUdBC9uRmYWCb1VgNM9rKc`
  - Buxgalteriya (jonli): `1SZYNg7Sj5aTIgmp3pKcnqWNI0sb7FbLooLx6dr7WieA`

## HOZIRGI HOLAT (qayerda to'xtadik)
- Buxgalteriya otchoti **«16--16» (16-iyun kunduz)gacha** to'ldirilgan edi; undan keyin 36 smena BO'SH.
- `TOLDIRILDI.xlsx` ga **3 smena** yozildi (faqat ишлаб чиqarиш, distillyat keyин):
  - 16--17 (Noch 2): VTR-118 L131226=4000, L132226=7000+Элак1650
  - 17--17 (Den-3): VTR-118 L132226=11500+elak1550
  - 17--18 (Noch 3): VTR-118 L132226=500, L134226=9000
- Kümulativ tekshiruv to'g'ri: Lot131→19000, Lot132→19000, Lot134→9000.

## KEYINGI QADAMLAR
1. `TOLDIRILDI.xlsx` ni Excel/Sheets'да ochib НМП/Расход formulalarini tekshirish.
2. **oil/grease** ni smenalararo moslab to'ldirish (Сменалар таҳлили / DI-tank).
3. 18-19 (Dewatering 765) — alohida bo'lim, qo'shish.
4. Qolgan bo'sh smenalarni (19.06+) guruh kelgan sari to'ldirish.
5. Sotuv (Экспорт/Внутр.рынок) — sotuv sheet'dан otchotга bog'lash.

> **TEKSHIRILDI (2026-06-19):** Jonli Buxgalteriya otchoti (`1SZYNg...`) HAM,
> Сменный производственный отчет (`1NxdsBAe...`) HAM «16.06 kunduz»dan keyin
> BO'SH. Demak 16.06 tun / 17 / 18 / 19 smenalar uchun oil/grease faqat
> **Telegram guruh + balans rasmi**dan olinadi (jadvalда yo'q).
> Ishlab chiqarish (mahsulot/lot/kg/НМП) `DRAFT_bosh_smenalar.md` da tayyor;
> qolgani — balans rasmlari kelishini kutadi.

## Telegram bot (nazorat boti)
- @OilaNazoratBot, zaxiradан: `~/44_102_BACKUP_2026-06-19/` (`venv/bin/python main.py --telegram`). Faqat egasi (chat_id 38292334).
- Kuzatadigan guruhlar: VEKTAN Production L1–L6 (-1003385027924), VEKTAN 2026 (-1004292982625, sotuv), Oxranala, Склад↔Производство.
- ⚠️ Seansга bog'liq — uzilsa to'xtaydi. 24/7 uchun launchd kerak.
