# VEKTAN Smena Otchot Bot — TEXNIK TOPSHIRIQ (TZ)

> Versiya: 1.0 · Sana: 2026-06-23 · Holat: **dizayn (kod yozilmagan)**
> Ega: Kamoliddin (Бегматов К.А.) · Loyiha: VEKTAN TRADING (mum/parafin)
> Manbalar: `STRUKTURA.md`, `HANDOFF.md`, `../CONTEXT.md`, `../MARKALAR.md`, `../YOMKOSTLAR.md`

---

## 1. Loyiha maqsadi
VEKTAN ishlab chiqarish smenasi otchotini **Telegram bot** orqali tuzilgan
(strukturali) ko'rinishда yig'ish. Operator/smena nachalniklari smena tugagach
botga savol-javob (wizard) orqali otchot topshiradi; bot validatsiya qiladi,
massa-balansni hisoblaydi va jadvalga (Google Sheets/Excel) yozadi.

## 2. Hozirgi muammo
- Smena ma'lumoti Telegram guruhga **tartibsiz rasm/izoh** bo'lib tashlanadi.
- Buxgalteriya otchotiga qo'lда ko'chirishда xato va kechikish.
- oil/grease (distillyat), chiqindi, uroven izchil yozilmaydi.

## 3. Yechim qamrovi (scope)
- ✅ Smena otchotini wizard orqali yig'ish (kirish + chiqish + balans).
- ✅ Avtomat hisob: lot, qop soni, vaqt oralig'i, brigada, massa-balans, tannarx.
- ✅ Jadvalga yozish + egaga xabar.
- ❌ Hozircha emas: to'liq ERP, sotuv/otgruzka moduli (keyin).

## 4. Foydalanuvchilar (rollar)
| Rol | Vazifa |
|---|---|
| Smena nachalnigi / operator | Smena otchotini botga kiritadi |
| Ega (Kamoliddin) | Natijani ko'radi, tasdiqlaydi, sozlaydi |
> ⏳ Ochiq: faqat ega (sinov) yoki bir nechta brigadir ishlatadimi.

## 5. Funksional talablar — Wizard oqimi (10 bosqich)
1. **Smena turi:** Den / Noch (tugma).
2. **Sana:** → `vaqt_oraligi` AVTOMAT (Den 08:00–20:00 / Noch 20:00–08:00).
3. **Boshlang'ich uroven:** tank (DI/R) → uroven (ko'z bilan) — distillyat hisobi uchun.
4. **Ishchilar soni:** nachalnik / operator / raznorabochiy → tannarx.
5. **Liniya (L1–L6):** → mahsulot ro'yxati; **brigada AVTOMAT** (grafikdan).
6. **Mahsulotlar sikli (×5–6):** har mahsulot uchun maydonlar (6-bo'lim).
7. **Skladdan xomashyo (KIRISH, ×N):** НМП oq/sariq/qora · umumiy kg · qop soni.
8. **Smena oxiri:** yakuniy uroven (ko'z bilan); to'xtash bo'lsa → sabab.
9. **Xulosa va tasdiq:** hammasi ko'rsatiladi → Tasdiq / Tahrir / Bekor.
10. **Saqlash:** massa-balans + tannarx hisoblanadi → jadvalga yoziladi + egaga xabar.

## 6. Ma'lumot modeli (maydonlar)

### 6.1 Sarlavha (bir marta)
| Maydon | Tur | Avtomat? | Izoh |
|---|---|---|---|
| smena_turi | tanlov | — | Den / Noch |
| sana | sana | — | |
| vaqt_oraligi | matn | ✅ | sana + smena_turidan |
| ishchilar.nachalnik/operator/raznorabochiy | son | — | tannarx uchun |
| brigada | tanlov | ✅ | grafikdan (A/B/C/D) |
| liniya | tanlov | — | L1–L6 |

### 6.2 Mahsulot (CHIQISH, takror)
| Maydon | Tur | Avtomat? | Izoh |
|---|---|---|---|
| marka | tanlov | — | liniyaga mos (`../MARKALAR.md`) |
| lot | matn | ✅ | L + partiya + liniya + 26 |
| miqdor_kg (ИЧ) | son | — | ishlab chiqarilgan kg |
| vaqt_boshlanish / vaqt_tugash | vaqt | — | majburiy |
| qadoq_turi | tanlov | — | 7-bo'lim ro'yxati |
| qop_soni | son | ✅ | = miqdor_kg ÷ qadoq birlik |
| distillat_oil_kg | son | — | DI tankdan (har mahsulotga) |
| distillat_griz_kg | son | — | DI tankdan (har mahsulotga) |
| otx_kg | son | — | Производственные чистий отходы (Элак) |
| musor_kg | son | — | Сортировочный мусор |
| chiqindi_kg | son | — | Отходы, не подлежащие переработке |

### 6.3 Xomashyo (KIRISH, takror)
| Maydon | Tur | Izoh |
|---|---|---|
| siryo_nomi | tanlov | НМП oq/sariq/qora (+ ikkilamchi) |
| umumiy_kg | son | obshi kg |
| qop_soni | son | qo'lда kiritiladi |

### 6.4 Uroven (smena boshi/oxiri, takror)
| Maydon | Tur | Izoh |
|---|---|---|
| tank | tanlov | `../YOMKOSTLAR.md` registri |
| uroven_boshi / uroven_oxiri | son | ko'z bilan (⏳ birlik: kg/%/belgi) |

## 7. Ma'lumotnomalar (reference data)
- **Markalar:** `../MARKALAR.md` (L1–L6, oil/grease beradigan markalar).
- **Qadoq turlari:** Биг бег 500 · кўк қоп 25 · кўк қоп 20 · оқ қоп 25 ·
  қизил қоп 25 · клариянт қоп 20 · қоғоз қоп 12 · қоғоз қоп 15.
- **Chiqindi:** otx (Элак, qayta ishlanadi) · musor · qayta ishlanmaydigan.
- **To'xtash sabablari:** svet yo'q · gaz yo'q · сырьё yo'q · ремонт · boshqa ish.
- **Tanklar:** `../YOMKOSTLAR.md` (DI=oil/grease, M/HV/R=xomashyo).
- **Brigada grafik:** `2026_4smena_grafik.xlsx`, list `ГРАФИК_2026` (д/Н/bo'sh).

## 8. Biznes qoidalar / hisob-kitoblar
- **lot** = `L` + partiya + liniya raqami (FC=1, PR=2, POWDER=3) + `26`.
- **qop_soni** = miqdor_kg ÷ qadoq birlik kg (CHIQISH avtomat; KIRISH qo'lда).
- **vaqt_oraligi**: Den 08–20 (obed 12–13, 11 soat); Noch 20–08 (obed 00–01, 7 soat).
- **massa-balans:** `Расход = ИЧ + oil + grease + otx + musor + poteri`;
  `НМП = Расход − qayta ishlatilgan`. НМП va Расход — formula; INPUT: ИЧ/oil/grease/otx/musor.
- **distillyat:** tank uroven farqidan (boshi − oxiri, ko'z bilan); operator yozmasa
  keyingi smena bilan moslanadi. oil/grease beradigan markalar — `../MARKALAR.md`.
- **tannarx (себестоимость)** = mehnat + xomashyo + energiya — ⏳ formula kerak.

## 9. Validatsiya
- Majburiy maydonlar to'ldirilmasa — keyingi qadamga o'tmaydi.
- Lot kümulativ jami tekshiriladi (oldingi smenadagi bilan mos).
- Massa-balans Разница ≈ 0 bo'lishi kerak; aks holda ogohlantirish.
- Sana/vaqt mantiqiy (tugash > boshlanish).

## 10. Saqlash va integratsiya
- Natija → jadvalga (⏳ Google Sheets / Excel / ikkalasi — tanlanadi).
- Buxgalteriya otchoti formatiga mos ustunlar (`../CONTEXT.md`).
- Egaga (Kamoliddin) Telegram xabar (xulosa + balans holati).

## 11. Texnologiya
- **Til:** Python · **Kutubxona:** aiogram (Telegram bot).
- **Saqlash:** Google Sheets API yoki Excel (openpyxl) — tanlanadi.
- Asl papka Mac'да: `/Users/kamoliddin/smena_bot/`. Repo nusxasi — sinxron uchun.
- Foydalanuvchi cheklovi: faqat ruxsat berilgan chat_id lar.

## 12. Yo'l xaritasi (bosqichlar)
1. ✅ Struktura/TZ (dizayn) — shu hujjat.
2. ⏳ Ochiq savollarni yopish (13-bo'lim).
3. Wizard prototipi (saqlashsiz, faqat oqim).
4. Jadvalga yozish + massa-balans.
5. Tannarx + brigada grafik integratsiyasi.
6. Sinov (ega) → brigadirlarga ochish.

## 13. Ochiq savollar (yopilishi kerak)
1. **Tannarx formulasi** — har lavozim stavkasi (so'm/soat yoki so'm/smena)?
2. **Saqlash joyi** — Google Sheets / Excel / ikkalasi?
3. **Kim ishlatadi** — faqat ega (sinov) yoki bir nechta brigadir?
4. **Uroven birligi** — kg / % / belgi?
5. **Xomashyo kirish** — lot/partiya kerakmi yoki nomi+kg+qop yetarli?
6. **Grafik fayl** — botga nusxa yoki Google Drive'дan o'qish?

## 14. Muvaffaqiyat mezonlari (acceptance)
- Smena nachalnigi 2–3 daqiqaда butun otchotni botga kiritadi.
- Massa-balans avtomat, Разница = 0.
- Buxgalteriya jadvali qo'lда ko'chirishsiz to'ladi.
- Guruhdagi tartibsiz rasm/izoh muammosi yo'qoladi.
