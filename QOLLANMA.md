# «Хуррият» архиви — qo'llanma

## Fayllar

```
index.html        sayt (bitta fayl, hech qanday server kerak emas)
sonlar.js         butun baza — sonlar, materiallar, matnlar
skan/             bet skanlari
QOLLANMA.md       shu fayl
```

Ochish uchun `index.html` ni brauzerda ochish kifoya. Internetga qo'yish uchun uch faylni birga
yuklash kerak (GitHub Pages, Netlify — ikkalasi ham bepul).

## Yangi son qo'shish

`sonlar.js` dagi `SONLAR` massiviga yangi obyekt qo'shiladi:

```js
{
  "raqam": 2,
  "nom": "2-сон",
  "izoh": "",
  "sana": "1997 йил 3 январь",
  "yil": 1997,
  "betlar": [
    { "bet": 1, "skan": "skan/2-son-1-bet.jpg", "kichik": "skan/2-son-1-bet-kichik.jpg" }
  ],
  "materiallar": [ ... ]
}
```

Hozir sayt faqat birinchi sonni ko'rsatadi (`SONLAR[0]`). Ikkinchi son qo'shilganda sonlar
o'rtasida o'tish tugmalari kerak bo'ladi — o'shanda aytsangiz qo'shib beraman.

## Material obyekti

```js
{
  "id": "2-01",                    // son raqami + tartib raqami
  "sarlavha": "Сарлавҳа",
  "rubrika": "Кеча",               // rubrika nomi ro'yxatdagi filtrga o'zi qo'shiladi
  "muallif": "Исм Фамилия",        // yo'q bo'lsa ""
  "tur": "maqola",                 // maqola | xabar | hujjat | lugat | surat
  "bet": 1,
  "matn": "Абзац.\nЯна абзац.",    // \n — yangi abzats
  "hudud": [ { "x": 1.8, "y": 16.0, "w": 24.8, "h": 83.5 } ]
}
```

`hudud` — materialning betdagi o'rni, skan rasmiga nisbatan foizda. Bitta material bir necha
joyga bo'lingan bo'lsa (masalan, ustuni pastda davom etsa), massivga ikkinchi to'rtburchak
qo'shiladi.

Foizni qo'lda hisoblash shart emas: skan ustidagi to'rtburchakning chap-yuqori burchagi va
o'lchamini rasm kengligiga bo'lib 100 ga ko'paytirasiz. Yoki menga skan bilan birga materiallar
ro'yxatini bersangiz, koordinatalarini o'zim chiqarib beraman.

## Matnni tekshirish

Har bir materialning o'qish oynasida o'ng tomonda o'sha materialning skandan kesilgan bo'lagi
turadi — matnni ko'zdan kechirib, xatosini `sonlar.js` dan to'g'rilash uchun. `[…]` belgisi
skanda o'qib bo'lmagan joyni bildiradi: buklama izi, dog', yoki ustun cheti kesilgani.

## Lotin yozuvi

Lotincha variant alohida saqlanmaydi — brauzerda kirillchadan o'giriladi (`lotin()` funksiyasi
`index.html` ichida). Agar biror so'z noto'g'ri o'girilsa, funksiyani tuzatish kerak, matnlarga
tegilmaydi.

## Skanni tayyorlash

Bet surati to'g'ri turishi, qiyshiqligi tuzatilgani va eni ~1800 piksel bo'lgani ma'qul
(taxminan 900 KB). Kichik nusxa (~520 px) ro'yxat uchun.


## Qirqim suratlar bilan ishlash

Materialning betdagi o'rni noma'lum bo'lsa (qirqim qilib olingan suratlar), `hudud` bo'sh
qoladi va o'rniga `qirqim` ishlatiladi:

```js
{
  "id": "1-14",
  "sarlavha": "Олис нолалар",
  "rubrika": "Йўқлов",
  "muallif": "Рўзибой Саидов",
  "bet": null,                       // null = bet aniqlanmagan
  "matn": "",                        // bo'sh = "matni ko'chirilmagan" deb ko'rinadi
  "izoh": "Матн ҳали кўчирилмаган.", // matn bo'lmaganda o'quvchiga ko'rsatiladi
  "hudud": [],
  "qirqim": ["skan/q07-yoqlov-olis-nolalar.jpg", "skan/q08-olis-nolalar-davomi.jpg"]
}
```

Keyinchalik betning to'liq skani topilsa: `bet` ga raqamni yozasiz, `betlar` ga skanni
qo'shasiz, `hudud` ni to'ldirasiz — `qirqim` ni o'chirish shart emas.

## Matn kiritilganda

`matn` maydoniga matnni yozganingizdan keyin `izoh` ni bo'shatib qo'ying (`""`), aks holda
matn ham, "ko'chirilmagan" izohi ham bir vaqtda ko'rinib qolishi mumkin emas —
sayt `matn` bo'sh bo'lmasa izohni ko'rsatmaydi, lekin tartib uchun tozalagan ma'qul.
