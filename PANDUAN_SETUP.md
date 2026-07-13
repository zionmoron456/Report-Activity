# Panduan Setup — Report Activity App

Aplikasi ini adalah **PWA** (web app yang bisa di-install seperti aplikasi native di HP Android). Sekali disetup, kamu tinggal buka, login sekali, lalu tiap catat aktivitas + foto akan otomatis masuk ke Google Sheet kamu — sheet bulan baru dibuat otomatis kalau belum ada.

Spreadsheet ID kamu (sudah diambil dari link yang kamu kirim):
```
1ELWzJ1ycxwX9jRiY5cGeqSLEozbqKuHy
```

Ada 5 langkah setup. Semua **gratis**, dan hanya perlu dilakukan **1 kali**.

---

## Langkah 1 — Buat Google Cloud Project

1. Buka https://console.cloud.google.com/
2. Klik dropdown project di kiri atas → **New Project**
3. Nama bebas, misal `Report Activity App` → **Create**
4. Pastikan project ini aktif/terpilih (cek dropdown kiri atas)

## Langkah 2 — Aktifkan 2 API

1. Buka https://console.cloud.google.com/apis/library
2. Cari **Google Sheets API** → klik → **Enable**
3. Cari **Google Drive API** → klik → **Enable**

## Langkah 3 — Setup OAuth Consent Screen

1. Buka https://console.cloud.google.com/apis/credentials/consent
2. Pilih **External** → Create
3. Isi *App name* (misal "Report Activity"), *User support email*, dan *Developer contact email* (pakai email Google kamu sendiri) → Save & Continue terus sampai selesai
4. Di bagian **Test users**, klik **Add users** → masukkan email Google kamu sendiri → Save
   *(karena app belum diverifikasi Google, hanya email yang didaftarkan di sini yang bisa login — cukup email kamu sendiri karena app ini memang untuk kamu pribadi)*

## Langkah 4 — Hosting file aplikasi

App perlu diakses lewat URL `https://...` (bukan file lokal), karena Google OAuth mewajibkan itu. Cara termudah & gratis: **GitHub Pages**.

1. Buat akun GitHub kalau belum punya: https://github.com/signup
2. Buat repository baru (public), misal nama `report-activity`
3. Upload ke-4 file dari paket ini: `index.html`, `manifest.json`, `sw.js`, `icon-192.png`, `icon-512.png`
   (di halaman repo → **Add file → Upload files** → drag semua file → Commit)
4. Buka **Settings → Pages** di repo tersebut → Source: pilih branch `main`, folder `/ (root)` → Save
5. Tunggu ~1 menit, GitHub akan kasih URL seperti:
   ```
   https://<username-kamu>.github.io/report-activity/
   ```
   Ini URL aplikasi kamu nanti.

> Alternatif lain kalau tidak mau pakai GitHub: **Netlify Drop** (https://app.netlify.com/drop) — tinggal drag folder ke browser, langsung dapat URL. Lebih cepat tapi URL-nya acak/kurang rapi.

## Langkah 5 — Buat OAuth Client ID

1. Buka https://console.cloud.google.com/apis/credentials
2. **Create Credentials → OAuth client ID**
3. Application type: **Web application**
4. Di **Authorized JavaScript origins**, klik **Add URI**, masukkan origin app kamu (tanpa slash di akhir, tanpa path), contoh:
   ```
   https://username.github.io
   ```
5. **Create** → salin **Client ID** yang muncul (bentuknya seperti `xxxxxxxxxx.apps.googleusercontent.com`)

---

## Langkah 6 — Jalankan & Install di HP

1. Di HP Android, buka Chrome, kunjungi URL app kamu dari Langkah 4
2. Tap ikon ⚙ (Pengaturan) di app → isi:
   - **Google OAuth Client ID** → paste dari Langkah 5
   - **Spreadsheet ID** → `1ELWzJ1ycxwX9jRiY5cGeqSLEozbqKuHy`
   - Cek/edit 5 label kategori KPI sesuai KPI kamu (sudah diisi otomatis sesuai sheet "Doni" kamu)
   - Tap **Simpan Pengaturan**
3. Tap **Masuk dengan Google** → pilih akun kamu
   - Karena app belum diverifikasi Google, akan muncul layar peringatan "Google hasn't verified this app" — ini normal untuk app pribadi. Tap **Advanced** → **Go to Report Activity (unsafe)** → Continue → Allow
4. Setelah login, tap menu **⋮** Chrome (pojok kanan atas) → **Add to Home screen** / **Install app**
5. Sekarang ada icon app di HP kamu seperti aplikasi biasa

---

## Cara Pakai Sehari-hari

- Buka app dari icon di HP
- Tap tombol **+** (kuning, kanan bawah)
- Isi Tanggal, Kategori KPI, Keterangan, dan foto (tap kotak foto → kamera langsung terbuka)
- Tap **Simpan Aktivitas**
- App otomatis:
  - Membuat sheet baru sesuai nama bulan (misal "Juli") kalau belum ada, dengan header yang sama seperti sheet bulan lain
  - Upload foto ke folder Google Drive **"Lampiran - Report Activity"**
  - Menambahkan baris baru ke kolom No, Tanggal, Kategori, Keterangan, Lampiran (isi link foto)

## Troubleshooting singkat

- **"Gagal memuat data" / error 401** → sesi login habis, tap Masuk dengan Google lagi
- **Muncul layar developer/unverified warning saat login** → itu normal, ikuti Langkah 6 poin 3
- **Foto gagal upload** → cek koneksi internet, ukuran foto terlalu besar bisa dikompres dulu oleh kamera HP secara otomatis, biasanya aman
- **Mau ganti akun Google** → buka ⚙ Pengaturan → Keluar dari Akun Google
