# Truth Doang — cara jadiin aplikasi Play Store

Paket ini sudah berbentuk **PWA** (Progressive Web App): HTML-nya sudah punya manifest,
service worker (jalan offline), font yang di-bundle, dan ikon ukuran lengkap.
Tinggal di-host, lalu dibungkus jadi file Android (.aab) dan diupload ke Play Console.

## Isi folder

```
index.html                 aplikasi utama (1000 pertanyaan ada di dalam file ini)
manifest.webmanifest       identitas aplikasi: nama, warna, ikon, mode layar penuh
sw.js                      service worker, bikin aplikasi jalan tanpa internet
fonts/                     Poppins versi ringan, supaya tidak perlu Google Fonts
icons/icon-*.png           ikon aplikasi (192 & 512, biasa & maskable)
icons/play-listing-icon-512.png        ikon buat halaman Play Store
icons/play-feature-graphic-1024x500.png  banner feature graphic Play Store
```

Catatan: `icons/play-*.png` hanya untuk diupload ke Play Console, bukan bagian aplikasi.

---

## Langkah 1 — Hosting (gratis, 10 menit)

Pilih salah satu:

**GitHub Pages**
1. Buat repo baru di github.com, misal `truth-doang`, set Public.
2. Upload semua isi folder ini (jangan folder induknya, langsung file-filenya).
3. Settings → Pages → Source: `Deploy from a branch`, Branch: `main`, folder `/root`. Save.
4. Tunggu 1–2 menit, URL muncul: `https://<username>.github.io/truth-doang/`

**Netlify Drop** (lebih cepat, tanpa akun Git)
1. Buka app.netlify.com/drop
2. Seret folder ini ke halaman itu. Langsung dapat URL HTTPS.

Buka URL-nya di Chrome HP, pastikan jalan, lalu coba mode pesawat untuk cek offline.

## Langkah 2 — Bungkus jadi file Android

Pakai **PWABuilder** (gratis, buatan Microsoft, outputnya TWA — aplikasi Android asli yang
menjalankan halaman kamu tanpa address bar):

1. Buka pwabuilder.com, tempel URL dari Langkah 1, klik Start.
2. Lihat skor. Manifest dan service worker harusnya sudah hijau.
3. Package For Stores → Android → Google Play.
4. Isi:
   - Package ID: `id.<namamu>.truthdoang` (format balik domain, huruf kecil, tidak bisa diubah selamanya)
   - App name: Truth Doang
   - **Signing key: Create new** → file `signing.keystore` + password ikut terdownload
5. Download. Isinya: `app-release-bundle.aab`, keystore, dan `assetlinks.json`.

**Simpan keystore dan passwordnya baik-baik.** Hilang = tidak bisa update aplikasi selamanya,
harus bikin listing baru dari nol.

6. Ambil `assetlinks.json` dari hasil download, taruh di hosting pada path:
   `https://domainmu/.well-known/assetlinks.json`
   Di GitHub Pages: bikin folder `.well-known` di repo, isi file itu.
   Kalau langkah ini dilewat, aplikasi akan tampil dengan address bar Chrome di atasnya.

## Langkah 3 — Play Console

1. Daftar di play.google.com/console, biaya pendaftaran USD 25 sekali seumur hidup.
2. Verifikasi identitas (KTP + alamat). Biasanya 1–3 hari.
3. Create app → isi nama, bahasa, tipe Game, gratis.
4. Lengkapi: deskripsi, ikon 512 (`play-listing-icon-512.png`), feature graphic
   (`play-feature-graphic-1024x500.png`), minimal 2 screenshot HP, kebijakan privasi (URL wajib).
5. Content rating: isi kuesioner. Game ini punya tema kencan/romansa ringan, jawab apa adanya,
   kemungkinan dapat rating Teen / 13+.
6. Data safety: aplikasi ini tidak mengumpulkan data apa pun, semua tersimpan di HP pengguna.
7. Upload `app-release-bundle.aab` ke track Closed testing.
8. Akun personal yang dibuat setelah 13 Nov 2023: wajib closed testing dengan minimal
   12 tester opt-in selama 14 hari berturut-turut sebelum bisa minta akses produksi.
   Rekrut 20 orang biar aman kalau ada yang mundur.
9. Setelah 14 hari: Apply for production → review Google → terbit.

## Update aplikasi nanti

1. Ubah `index.html`, naikkan `VERSION` di `sw.js` (misal jadi `truth-doang-v2`).
2. Upload ulang ke hosting. Pengguna otomatis dapat versi baru saat buka aplikasi.
3. Tidak perlu upload ulang ke Play Store, kecuali ikon atau nama aplikasi yang berubah.
   Ini keunggulan TWA: isi aplikasi diambil dari web, jadi update tanpa review Google.
