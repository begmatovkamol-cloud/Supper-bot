# Smena Otchot Bot — HANDOFF (telefonда davom ettirish uchun)

> Bu fayl telefonда (claude.ai + Google Drive konnektor) ishni davom ettirish uchun.
> Asosiy hujjat: `STRUKTURA.md` (shu papkada). Oxirgi yangilanish: 2026-06-21.

## Claude'ga ko'rsatma (telefonда o'qiyotgan bo'lsang)
Biz hozir **faqat dizayn/strukturani** tuzyapmiz — KOD YOZILMAYDI, ish keyin, hammasi tayyor bo'lgach boshlanadi. Vazifang: egadan (Kamoliddin) qolgan ma'lumotlarni so'rab, `STRUKTURA.md` dagi `???` va bo'sh joylarni to'ldirib borish. Har gal yangilanganda STRUKTURA.md ni qayta yozib qo'y.

## Loyiha nima
**Smena otchot topshiradigan Telegram bot** (VEKTAN TRADING, mum/parafin ishlab chiqarish). Operator/brigadirlar smena tugagach botga **tuzilgan** otchot topshiradi — guruhga tartibsiz rasm/izoh tashlash o'rniga. Bot savol-javob (wizard) qiladi, validatsiya qiladi, jadvalga yozadi.

## Wizard oqimi (kelishilgan)
1. **Smena turi**: Den / Noch (birinchi)
2. **Sana** → bot **vaqt oralig'ini avtomat** chiqaradi:
   - Den: sana 08:00 – sana 20:00 (obed 12–13, 11 ish soat)
   - Noch: sana 20:00 – ertasi 08:00 (obed 00–01, tунги 7 soat)
3. **Ishchilar soni**: nachalnik / operator / raznorabochiy → tannarx (себестоимость) uchun
4. **Liniya** L1–L6 (brigada AVTOMAT — pastга qara)
5. **Mahsulotlar sikli** (5–6 xil bo'lishi mumkin, har biri):
   - asosiy: marka, lot (avtomat), miqdor kg, vaqt (majburiy, mas. 09:00–16:30), qadoq turi, qop soni (avtomat)
   - ajraladigan: distillat oil (kg), distillat griz (kg), 3 xil otxod (kg)
6. **Skladdan xomashyo (KIRISH)** sikli: siryo nomi (НМП oq/sariq/qora), umumiy kg, qop soni (kiritiladi)
7. **Xulosa va tasdiq** (tasdiq / tahrir / bekor)
8. **Saqlash** + tannarx + massa-balans + egaga xabar

## Massa-balans
KIRISH (НМП) ≈ CHIQISH (mahsulot) + otxodlar + oil + griz.

## Brigada — AVTOMAT (hal qilingan)
Smena grafikidan aniqlanadi, operator kiritmaydi.
- Fayl: `Мой диск/ПР2025--2026/Ишга сухбатдан ўтканла/Смена график/2026_4smena_grafik.xlsx`
- List `ГРАФИК_2026`: д=kunduz, Н=tun, bo'sh=выход. Har kun 1 brigada kunduz, 1 tun.
- Misol: 01.01.2026 → A=kunduz, B=tun.
- Qoida: (sana, smena_turi) → grafikdan brigada.

## TO'LDIRISH KERAK (egadan so'ra — checklist)
1. **3 otxod nomlari** — har mahsulotdan chiqadigan 3 xil otxod qanday ataladi?
2. **Qadoq turlari** to'liq ro'yxati (hozir ma'lum: 25 kg ko'k qop, 25 kg oq qop, 500 kg big bag, + boshqalar)
3. **Xomashyo (kirish)** — lot/partiya raqami kerakmi yoki nomi+kg+qop yetarli?
4. **Tannarx formulasi** — har lavozim stavkasi (so'm/soat yoki so'm/smena)? Ish soat: kunduz 11, tun 7.
5. **Saqlash joyi** — Google Sheets yoki Excel yoki ikkalasi?
6. **Kim ishlatadi** — faqat ega (sinov) yoki bir nechta brigadir?

## Texnologiya (rejalashtirilgan, hali yozilmagan)
Python + aiogram. Asl papka Mac'da: `/Users/kamoliddin/smena_bot/`. Bu Drive nusxasi — telefon uchun.
