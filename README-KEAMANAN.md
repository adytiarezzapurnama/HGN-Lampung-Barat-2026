# Catatan Keamanan — HGN & HUT PGRI Lampung Barat

## Prinsip yang diterapkan
- Otorisasi admin menggunakan Firebase Authentication dan UID admin yang ditentukan.
- `localStorage` tidak dianggap sebagai bukti otorisasi.
- Koleksi pendaftaran lengkap dipisahkan dari ringkasan pendaftaran publik.
- Kata sandi tidak disimpan pada dokumen Firestore.
- Pembuatan kiriman karya mensyaratkan akun peserta yang sudah berstatus `VERIFIED`.
- Semua jalur Firestore yang tidak didefinisikan secara eksplisit ditolak oleh aturan terakhir.

## Perhatian
1. Jangan mengganti UID admin di `index.html` atau `firestore.rules` kecuali akun admin memang diganti.
2. Jangan membuat aturan luas seperti `allow read, write: if request.auth != null;`.
3. Form olahraga/drumband menggunakan Firebase Anonymous Authentication di belakang layar. Pengunjung tidak perlu membuat akun atau memasukkan password untuk formulir tersebut.
4. `public_registrations` memang dapat dibaca publik, tetapi hanya menyimpan nama/tim, cabang, sekolah, kecamatan, status, dan waktu. Jangan menambahkan email atau nomor telepon ke dokumen ringkasan publik.
5. Admin dapat mengelola data lengkap melalui koleksi `event_registrations`. Data kontak/anggota tidak dibaca publik oleh aturan yang disertakan.
6. Juknis disimpan sebagai tautan yang dikelola admin. Pastikan tautan yang dimasukkan memang boleh diakses peserta.
7. Rules tidak dapat membuktikan bahwa data yang diketik pengguna benar. Validasi pada sisi server/Cloud Functions dapat dipertimbangkan untuk proses yang lebih kritis.

## Jika fitur gagal setelah Rules dipublikasikan
- Pastikan Email/Password dan Anonymous Authentication aktif.
- Pastikan website sudah menggunakan `index.html` dari paket upgrade.
- Periksa tab Console di browser dan error pada Firebase Console.
- Jangan membuka akses semua koleksi sebagai jalan pintas.
