# Truth Doang

1000 pertanyaan truth buat tongkrongan. Putar botolnya, botol nunjuk siapa yang harus jawab jujur.

**Main di sini:** https://raihankarim19.github.io/truth-doang/

## Isi

| File | Fungsi |
|---|---|
| `index.html` | Seluruh aplikasi, termasuk 1000 pertanyaannya |
| `manifest.webmanifest` | Identitas PWA: nama, ikon, warna, mode layar penuh |
| `sw.js` | Service worker — aplikasi jalan penuh tanpa internet |
| `privacy.html` | Kebijakan privasi (wajib untuk listing Play Store) |
| `fonts/` | Poppins versi subset, supaya tidak bergantung Google Fonts |
| `icons/icon-*.png` | Ikon aplikasi (192 & 512, biasa & maskable) |
| `icons/play-*.png` | Aset untuk halaman Play Store, bukan bagian aplikasi |

## Fitur

- 1000 pertanyaan dalam 9 kategori, tanpa pengulangan sampai habis
- Botol memutar dan menunjuk pemain; orang yang sama tidak kena dua kali berturut-turut
- Paket sekali tap: Semua, Cinta doang, Aman tanpa cinta, Ringan & ketawa
- Jalan offline, progres tersimpan di perangkat masing-masing
- Mode gelap mengikuti setelan sistem

## Cara update

1. Ubah `index.html`.
2. Naikkan `VERSION` di `sw.js` (`truth-doang-v1` → `truth-doang-v2`).
3. Commit dan push. GitHub Pages menerbitkan ulang dalam 1–2 menit.

## Jadikan aplikasi Android

Lihat `README-cara-publish.md` untuk langkah membungkus situs ini jadi file `.aab`
lewat PWABuilder dan menerbitkannya di Google Play.
