# KAS WARGA BLOK P — Firebase + Vercel

Versi ini memakai Firebase Authentication + Cloud Firestore. Warga masuk tanpa password melalui Anonymous Authentication; pengurus masuk memakai Email/Password Firebase Authentication.

## 1. Buat Firebase Project

Di Firebase Console:
1. Create project.
2. Add Web App.
3. Copy Firebase Web App configuration ke `firebase-config.js`.
4. Authentication > Sign-in method: aktifkan **Anonymous** dan **Email/Password**.
5. Firestore Database: Create database.
6. Firestore Rules: gunakan isi `firestore.rules`.

Dokumentasi resmi:
- https://firebase.google.com/docs/web/setup
- https://firebase.google.com/docs/auth/web/start

## 2. Buat akun pengurus

Di Firebase Console > Authentication > Users:
- Add user.
- Masukkan email pengurus.
- Tentukan password.

Jangan menyimpan password di Firestore.

## 3. Isi profil pengurus

Setelah login sebagai pengurus, gunakan menu **Akun Pengurus RT** untuk menyimpan nama, jabatan, dan email profil.

## 4. Deploy ke Vercel

Upload seluruh folder project ini sebagai project baru di Vercel.

Tidak membutuhkan build command karena aplikasi adalah static web app.

Setelah deploy, buka URL Vercel dari smartphone dan pilih **Add to Home Screen**.

## 5. Struktur data Firestore

- `transaksi` — pemasukan/pengeluaran
- `warga` — daftar warga dan status iuran
- `pengurus` — profil publik pengurus (tanpa password)

## 6. Catatan keamanan

Firestore Rules membolehkan read publik untuk transparansi, tetapi create/update/delete hanya untuk akun yang memiliki email Authentication. Untuk produksi, review rules sebelum go-live.
