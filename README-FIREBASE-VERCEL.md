# Kas Warga Blok P — Firebase Phone Authentication + Vercel

## 1. Firebase Authentication
Aktifkan:
- Phone Number

Warga dan Pengurus masuk menggunakan nomor HP + OTP SMS.

## 2. Pengurus / whitelist
Setelah nomor HP Pengurus berhasil login melalui Phone Authentication, buka Firebase Authentication > Users dan salin **UID** akun tersebut.

Di Firestore buat collection:
`pengurus`

Buat document dengan:
- **Document ID = UID Firebase Pengurus**
- `nama`: nama pengurus
- `phone`: nomor HP pengurus (opsional untuk profil)
- `role`: `pengurus`

Contoh:
`pengurus/AbCdEf123...`

Aplikasi hanya memberikan akses Pengurus jika UID hasil login Phone Authentication memiliki document tersebut.

## 3. Firestore
Gunakan `firestore.rules` yang sudah disertakan. Warga yang sudah terautentikasi dapat membaca data transparansi. Hanya UID yang terdaftar di `pengurus` yang dapat membuat, mengubah, atau menghapus transaksi dan data warga.

## 4. Deploy ke Vercel
Upload repository ke GitHub lalu import repository tersebut ke Vercel.

## 5. Phone Authentication di Firebase
Di Firebase Console:
Authentication > Sign-in method > Phone > Enable.

Untuk domain produksi, pastikan domain Vercel Anda ditambahkan pada Authentication > Settings > Authorized domains.

## 6. Format nomor HP
Aplikasi menerima format Indonesia:
- `0812xxxxxxxx`
- `+62812xxxxxxxx`

Aplikasi akan menormalkan nomor menjadi format E.164 (`+62...`) sebelum meminta OTP.
