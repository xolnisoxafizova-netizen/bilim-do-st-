# Bilim do'sti: uyga vazifa platformasi

O'qituvchi uyga vazifani rasm, PDF yoki test qilib yuboradi. O'quvchi telefonidan topshiradi. Baholar va hisobot o'zi yig'iladi.

**Raqamli avlod qizlari** tanlovi uchun prototip, **Ta'lim** yo'nalishi.

![Bosh sahifa](docs/screenshots/landing.png)

## Imkoniyatlar

**O'qituvchi profili**
- Ro'yxatdan o'tishda ism-familiya, viloyat, tuman yoki shahar, maktab, biriktirilgan sinflar va fanlar kiritiladi.
- **Sinflar va o'quvchilar:** o'quvchilar bittalab yoki butun ro'yxat bilan qo'shiladi. Login va parol avtomatik yaratiladi, ularni CSV qilib yuklab olsa bo'ladi.
- **Uyga vazifa:** sinf va fan tanlanadi, vazifa rasm yoki PDF qilib yuboriladi yoki test tuziladi. Vazifa sinfdagi barcha o'quvchilarga boradi.
- **Kelgan javoblar:** javoblar o'quvchining ism-familiyasi bilan keladi. Baho (2–5) va izoh qo'yiladi.
- **AI tekshiruvi:** AI o'quvchining javobini (rasm yoki PDF) vazifa bilan solishtiradi, xatolarni topadi va baho taklif qiladi. Bitta tugma bilan hamma javobni tekshirtirsa bo'ladi. Yakuniy bahoni o'qituvchi qo'yadi. Bu imkoniyat hozircha claude.ai versiyasida ishlaydi.
- **Hisobotlar:** sinf va fan bo'yicha natijalar jadvali. Excel'da ochiladigan CSV fayl qilib yuklab olinadi.

**O'quvchi profili**
- **Vazifalar:** qaysi fandan vazifa kelgani ko'rinadi. Savol-javob turidagi vazifaga javob rasm yoki PDF qilib yuklanadi. Test shu yerda ishlanadi va ball darhol chiqadi.
- **Natijalarim:** baholar, test ballari va o'qituvchi izohlari.
- **AI yordamchi:** vazifani tushunishga yordam beradi, lekin javobni aytmaydi. Hozircha faqat claude.ai versiyasida ishlaydi.

| O'qituvchi: vazifa yuborish | O'quvchi: vazifalar |
| --- | --- |
| ![O'qituvchi](docs/screenshots/teacher-homework.png) | ![O'quvchi](docs/screenshots/student-tasks.png) |
| **O'qituvchi: kelgan javoblar** | **O'qituvchi: hisobot** |
| ![Javoblar](docs/screenshots/teacher-inbox.png) | ![Hisobot](docs/screenshots/teacher-report.png) |

## Sinab ko'rish

1. `index.html` faylini brauzerda oching yoki GitHub Pages manzilidan kiring.
2. **Kirish** sahifasida **Demo hisoblarni yaratish** tugmasini bosing.
3. Quyidagi hisoblar bilan kiring:

| Kim | Login | Parol |
| --- | --- | --- |
| O'qituvchi | `oqituvchi` | `demo123` |
| O'quvchi | `aziza` | `demo123` |
| O'quvchi | `jasur`, `madina` | `demo123` |

Platforma ikki rejimda ishlaydi:

- **Umumiy baza (Firebase ulangan).** Hamma bitta bazaga kiradi: o'qituvchi yuborgan vazifa o'quvchining telefonida chiqadi, javob va baho o'qituvchiga sahifani yangilamasdan keladi. Qanday ulash pastda yozilgan.
- **Demo rejimi (`firebase-config.js` bo'sh).** Ma'lumotlar **faqat shu brauzerda** saqlanadi va boshqa qurilmada ko'rinmaydi. O'qituvchi va o'quvchini bitta qurilmada navbat bilan sinab ko'rish uchun: "Chiqish" tugmasini bosib, boshqa login bilan kiring.

## Umumiy baza ulash (Firebase, bepul)

Firebase: Google'ning bepul xizmati. Bank kartasi kerak emas. Bepul reja: 1 GB ma'lumot, kuniga 50 ming o'qish va 20 ming yozish. Bir nechta sinf uchun bu yetarli.

1. [console.firebase.google.com](https://console.firebase.google.com) saytiga Google hisobi bilan kiring. Buni ustozingiz bilan birga, uning hisobidan qilgan yaxshi: baza maktab nomidan bo'ladi.
2. **Create a project** (yoki **Add project**) tugmasini bosing. Nomi: `bilim-dosti`. Google Analytics kerak emas, o'chirib qo'ysangiz bo'ladi. **Create project**.
3. Chap menyuda **Build → Firestore Database** (yangi ko'rinishda **Databases & Storage → Firestore**) ni oching va **Create database** tugmasini bosing.
   - Edition: **Standard edition**.
   - Location: Yevropa (masalan, `eur3`). Keyin uni o'zgartirib bo'lmaydi.
   - Rules: **Start in test mode**. **Create**.
4. Firestore sahifasida **Rules** yorlig'ini oching. U yerdagi hamma matnni o'chirib, shu repodagi `firestore.rules` fayli matnini qo'ying va **Publish** tugmasini bosing. (Test rejimi 30 kundan keyin bazani yopib qo'yadi, bu qoidalar esa yopmaydi.)
5. Chap yuqoridagi ⚙️ → **Project settings**. Pastda **Your apps** bo'limida veb belgisini (`</>`) bosing. Ilova nomi: `bilim-dosti`, Hosting belgisi kerak emas. **Register app**.
6. Firebase kod ko'rsatadi. Undan faqat `const firebaseConfig = { ... };` qismini nusxalang.
7. GitHub'dagi repoda `firebase-config.js` faylini oching, qalam ✏️ belgisini bosing va bo'sh `firebaseConfig` ni nusxalaganingiz bilan almashtiring. **Commit changes**.
8. 2–3 daqiqadan keyin saytni oching (o'zgarmasa, sahifani yangilang). "Demo rejimi" yozuvi chiqmasa, baza ulangan. Kirish sahifasida **Demo hisoblarni yaratish** tugmasini bir marta bosing: endi bu hisoblar hamma qurilmada ishlaydi.

Xato chiqsa, sayt o'zi sababini yozadi: masalan, baza yaratilmagan bo'lsa yoki Rules ruxsat bermasa.

**Diqqat.** Bu prototip: sayt manzilini bilgan odam bazani o'qiy oladi. Shuning uchun haqiqiy o'quvchilarning ma'lumotini kiritmang, demo yoki to'qima ismlar ishlating. Haqiqiy maktabda ishlatishdan oldin Firebase Authentication qo'shib, qoidalarni kuchaytirish kerak.

## GitHub Pages'ga joylash

1. [github.com](https://github.com) saytida hisob oching yoki kiring.
2. **New repository** tugmasini bosing. Nomi `bilim-dosti` bo'lsin, turi **Public**. Keyin **Create repository**.
3. **uploading an existing file** havolasini bosing. Arxivdan chiqarilgan papka ichidagi hamma narsani (`index.html`, `firebase-config.js`, `firestore.rules`, `README.md`, `src`, `docs`, `build.py`) sudrab tashlang va **Commit changes** tugmasini bosing.
4. **Settings → Pages** bo'limiga kiring. **Source** uchun **Deploy from a branch**, **Branch** uchun `main` va `/ (root)` ni tanlab, **Save** tugmasini bosing.
5. 1–2 daqiqadan keyin sayt shu manzilda ochiladi: `https://<foydalanuvchi-nomi>.github.io/bilim-dosti/`

## Texnik tuzilma

- Butun platforma bitta `index.html` faylida ishlaydi: HTML, CSS va JavaScript. Tashqi kutubxona faqat umumiy baza rejimida yuklanadi (Firebase).
- Manba fayllar `src/` papkasida: `styles.css` (dizayn), `ill.js` (chizilgan rasmlar), `app.js` (mantiq). O'zgartirgandan keyin `python3 build.py` buyrug'i ularni `index.html` ga yig'adi.
- Ma'lumotlar saqlanadigan joy uchta:
  - **claude.ai versiyasi:** ma'lumotlar artefakt bazasida saqlanadi, fayllar alohida yuklanadi, AI yordamchi va AI tekshiruvi ishlaydi.
  - **GitHub Pages + Firebase:** hamma qurilma uchun bitta Firestore bazasi. O'zgarishlar boshqa qurilmalarga darhol yetib boradi. Rasm va PDF fayllar ham bazada bo'laklarga bo'lib saqlanadi (Firebase'ning fayl ombori pullik rejada, shuning uchun u ishlatilmagan). Rasm avtomatik kichraytiriladi, PDF 5 MB dan oshmasligi kerak.
  - **Demo rejimi:** ma'lumotlar brauzerning IndexedDB xotirasida, faqat shu qurilmada.
- Parollar SHA-256 bilan, tasodifiy "tuz" (salt) qo'shib saqlanadi. Bu prototip uchun yetarli, lekin haqiqiy xavfsizlik emas.

## Cheklovlar va keyingi qadamlar

- **Xavfsiz kirish.** Hozir login va parol brauzerda tekshiriladi, baza esa manzilni bilgan har kimga ochiq. Keyingi qadam: Firebase Authentication va har bir foydalanuvchi faqat o'z ma'lumotini ko'radigan qoidalar.
- **AI (yordamchi va tekshiruv) GitHub versiyasida.** U AI xizmati kaliti saqlanadigan kichik server funksiyasi orqali ulanadi.
- **Qo'shimcha imkoniyatlar:** ota-onalar uchun hisobot, eslatmalar, rus va qoraqalpoq tillari.

## Jamoa

- _Ism Familiya_: g'oya va taqdimot
- _Ism Familiya_: dizayn va sinov
- _Ism Familiya_: tadqiqot va so'rovnoma
