# Checklist Pengujian Setelah Upgrade

## Firebase
- [ ] Authentication Email/Password aktif.
- [ ] Authentication Anonymous aktif.
- [ ] UID admin sesuai di `index.html` dan `firestore.rules`.
- [ ] Firestore Rules dari paket telah dipublikasikan tanpa error.

## Website
- [ ] Beranda terbuka dan jam/kalender WIB berubah otomatis.
- [ ] Daftar cabang muncul di GTK, Olahraga, dan Seni Pertunjukan.
- [ ] Jumlah cabang di beranda sesuai jumlah cabang aktif.
- [ ] Admin dapat menambah cabang, memilih kategori, dan memilih jenis formulir.
- [ ] Juknis per kategori dapat disimpan dan dibuka.
- [ ] Timeline GTK, Olahraga, dan Seni dapat dikelola terpisah.

## Pendaftaran
- [ ] Form GTK: akun baru berstatus PENDING dan menunggu verifikasi.
- [ ] Form stan: data stan, koordinator, sekolah, anggota, email disimpan; password tidak masuk Firestore.
- [ ] Form olahraga: tim dapat mendaftar tanpa login interaktif.
- [ ] Form drumband: regu dapat mendaftar tanpa login interaktif.
- [ ] Pendaftar terlihat pada cabang yang benar dan diurutkan berdasarkan waktu.
- [ ] Ringkasan publik tidak menampilkan email, nomor telepon, atau daftar lengkap anggota.
- [ ] Admin dapat mengubah status pendaftaran dan menghapus data uji yang dipilih.
- [ ] CSV semua cabang dan CSV per cabang berhasil diunduh.

## Keamanan dan data
- [ ] Peserta PENDING tidak dapat mengirim karya.
- [ ] Peserta VERIFIED dapat mengirim tautan berkas.
- [ ] Peserta tidak dapat mengubah/menghapus kiriman sendiri.
- [ ] Peserta tidak dapat mengubah pengumuman, kategori, timeline, atau status pendaftaran.
- [ ] Data penting lama tetap ada.
- [ ] Pengumuman dan sinkronisasi ant perangkat masih berfungsi.

Jangan menghapus akun/data percobaan sebelum memastikan data yang dihapus memang hanya data uji dan sudah dicadangkan.


## Manajemen logo tambahan
- [ ] Login sebagai admin, buka tab **Edit Logo & Informasi Utama Web**.
- [ ] Tambahkan satu logo PNG/JPG/WebP dari komputer dan pastikan pratinjau muncul.
- [ ] Klik **Simpan Galeri Logo ke Cloud**, lalu buka website pada perangkat/jendela lain untuk memeriksa sinkronisasi.
- [ ] Uji tampil/nonaktif, ubah urutan, dan hapus logo; simpan kembali setiap kali selesai mengatur.
- [ ] Pastikan logo utama GTK dan Disdikbud tetap tampil seperti sebelumnya.
