# Kas Warga Blok P — Firebase Email/Password Authentication + Vercel

## 1. Firebase Authentication
Aktifkan:
- Phone Number

Warga dan Pengurus masuk menggunakan email Pengurus + OTP SMS.

## 2. Pengurus / whitelist
Setelah email Pengurus Pengurus berhasil login melalui Email/Password Authentication, buka Firebase Authentication > Users dan salin **UID** akun tersebut.

Di Firestore buat collection:
`pengurus`

Buat document dengan:
- **Document ID = UID Firebase Pengurus**
- `nama`: nama pengurus
- `phone`: email Pengurus pengurus (opsional untuk profil)
- `role`: `pengurus`

Contoh:
`pengurus/AbCdEf123...`

Aplikasi hanya memberikan akses Pengurus jika UID hasil login Email/Password Authentication memiliki document tersebut.

## 3. Firestore
Gunakan `firestore.rules` yang sudah disertakan. Warga yang sudah terautentikasi dapat membaca data transparansi. Hanya UID yang terdaftar di `pengurus` yang dapat membuat, mengubah, atau menghapus transaksi dan data warga.

## 4. Deploy ke Vercel
Upload repository ke GitHub lalu import repository tersebut ke Vercel.

## 5. Email/Password Authentication di Firebase
Di Firebase Console:
Authentication > Sign-in method > Phone > Enable.

Untuk domain produksi, pastikan domain Vercel Anda ditambahkan pada Authentication > Settings > Authorized domains.

## 6. Format email Pengurus
Aplikasi menerima format Indonesia:
- `0812xxxxxxxx`
- `+62812xxxxxxxx`

Aplikasi akan menormalkan nomor menjadi format E.164 (`+62...`) sebelum meminta OTP.
