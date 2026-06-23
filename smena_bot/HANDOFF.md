# Smena Otchot Bot — HANDOFF

> Telefon (claude.ai) yoki VS Code'да davom ettirish uchun.
> Asosiy hujjat: `STRUKTURA.md` (shu papkada). Oxirgi yangilanish: 2026-06-23.

## Claude'ga ko'rsatma
Hozir **faqat dizayn/struktura** tuzilyapti — **KOD YOZILMAYDI**, ish keyin,
hammasi tayyor bo'lgach boshlanadi. Vazifa: egadan (Kamoliddin) qolgan
ma'lumotlarni so'rab, `STRUKTURA.md` dagi ochiq joylarni to'ldirib borish.
Har yangilanганда `STRUKTURA.md` ni qayta yozib qo'y.

## Loyiha nima
**Smena otchot topshiradigan Telegram bot** (VEKTAN TRADING, mum/parafin).
Operator/brigadirlar smena tugagach botga **tuzilgan** otchot topshiradi —
guruhga tartibsiz rasm/izoh tashlash o'rniga. Bot wizard (savol-javob) qiladi,
validatsiya qiladi, massa-balansni hisoblaydi, jadvalga yozadi.

## Wizard oqimi (kelishilgan)
1. **Smena turi**: Den / Noch
2. **Sana** → vaqt oralig'i avtomat (Den 08–20 / Noch 20–08)
3. **Boshlang'ich uroven** (tank, ko'z bilan) — distillyat hisobi uchun
4. **Ishchilar soni**: nachalnik / operator / raznorabochiy → tannarx
5. **Liniya** L1–L6 (brigada AVTOMAT — grafikdan)
6. **Mahsulotlar sikli** (5–6 xil): marka, lot(avtomat), miqdor kg, vaqt,
   qadoq, qop soni(avtomat), oil, griz, otx, musor, chiqindi
7. **Skladdan xomashyo (KIRISH)**: НМП oq/sariq/qora, umumiy kg, qop soni
8. **Smena oxiri**: yakuniy uroven (ko'z bilan), to'xtash sababi (bo'lsa)
9. **Xulosa va tasdiq** (tasdiq / tahrir / bekor)
10. **Saqlash** + tannarx + massa-balans + egaga xabar

## Massa-balans
КИРИШ (НМП) ≈ ЧИҚИШ (mahsulot) + otx + musor + chiqindi + oil + griz + poteri.
`Расход = ИЧ + oil + grease + otx + musor + poteri`

## Brigada — AVTOMAT (hal qilingan)
- Fayl: `Мой диск/ПР2025--2026/.../Смена график/2026_4smena_grafik.xlsx`
- List `ГРАФИК_2026`: д=kunduz, Н=tun, bo'sh=выход. (sana, smena_turi) → brigada.

## TO'LDIRISH KERAK (egadan so'ra)
1. ~~3 otxod nomlari~~ ✅ HAL: otx / musor / qayta ishlanmaydigan chiqindi
2. ~~Qadoq turlari~~ ✅ HAL: STRUKTURA.md 2-bo'lim
3. **Xomashyo (kirish)** — lot/partiya kerakmi yoki nomi+kg+qop yetarli?
4. **Tannarx formulasi** — har lavozim stavkasi (so'm/soat yoki so'm/smena)?
5. **Saqlash joyi** — Google Sheets / Excel / ikkalasi?
6. **Kim ishlatadi** — faqat ega (sinov) yoki bir nechta brigadir?
7. **Uroven birligi** — kg / % / belgi?

## Texnologiya (rejalashtirilgan, hali yozilmagan)
Python + aiogram. Asl papka Mac'да: `/Users/kamoliddin/smena_bot/`.
Bu repo nusxasi — telefon + VS Code uchun (GitHub orqali sinxron).
