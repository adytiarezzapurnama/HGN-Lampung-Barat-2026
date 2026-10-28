# HGN & HUT PGRI Ke-81 Lampung Barat — Paket Upgrade

Paket ini mempertahankan aplikasi HTML yang sudah ada dan menambahkan pengelolaan tiga kategori lomba.

## Isi paket

- `index.html` — website lengkap (single-page app).
- `firestore.rules` — aturan keamanan untuk Firebase Cloud Firestore.
- `README.md` — panduan pemasangan.
- `README-KEAMANAN.md` — catatan keamanan dan data.
- `CHECKLIST-PENGUJIAN.md` — daftar uji setelah deploy.

## Fitur upgrade

### 0. Manajemen beberapa logo
- Admin dapat mengunggah hingga 8 logo tambahan dari komputer (PNG/JPG/WebP, maksimal 2 MB per file).
- Gambar otomatis diperkecil dan disimpan pada dokumen Firestore `settings/site_logo_gallery`, tanpa Firebase Storage.
- Logo tampil berjajar di bagian atas beranda, dekat identitas dan judul acara.
- Admin dapat mengaktifkan/nonaktifkan logo, mengubah urutan, dan menghapus logo. Klik **Simpan Galeri Logo ke Cloud** agar perubahan tersinkron ke semua perangkat.
- Logo utama GTK dan Disdikbud yang sudah ada tetap dipertahankan.


### 1. Kategori lomba dinamis
- **GTK:** Guru Berprestasi, Guru Inovasi, Kepala Sekolah Inovasi, Menulis Esai, Menulis Jurnal, Stan Pendidikan dan Inovasi, Komunitas Belajar.
- **Olahraga:** Voli GTK Putra, Voli GTK Putri, Futsal GTK Putra.
- **Seni Pertunjukan:** Drumband.
- Admin dapat menambah/mengubah/menghapus cabang dan memilih kategori serta jenis formulirnya.
- Jumlah cabang di beranda mengikuti jumlah cabang aktif.

### 2. Formulir sesuai jenis lomba
- Lomba GTK menggunakan sistem akun dan verifikasi admin yang sudah ada.
- Stan Pendidikan dan Inovasi memiliki formulir khusus, membuat akun email/password, dan setelah disetujui dapat mengirim tautan berkas melalui portal peserta.
- Olahraga menggunakan formulir tim tanpa login interaktif; sistem menggunakan Firebase Anonymous Authentication di belakang layar untuk mengamankan pengiriman.
- Drumband menggunakan formulir regu tanpa login interaktif.
- Anggota tim/stan dapat ditambah barisnya.
- Daftar publik hanya menampilkan ringkasan pendaftar. Nomor telepon, email, dan detail anggota disimpan di koleksi privat.

### 3. Admin
- Tab **Pendaftaran Tim** menampilkan data menurut waktu pendaftaran terbaru.
- Admin dapat mengubah status atau menghapus data pendaftaran yang dipilih.
- Ekspor CSV tersedia untuk semua cabang atau cabang yang dipilih. Ekspor peserta lama tetap tersedia di tombol ekspor peserta.
- Cabang baru dapat dimasukkan ke kategori yang dipilih admin.

### 4. Juknis, jam, kalender, timeline
- Beranda menampilkan jam dan kalender WIB yang diperbarui otomatis.
- Juknis tersedia per kategori.
- Timeline publik dan admin dipisahkan untuk GTK, Olahraga, dan Seni Pertunjukan.

## Sebelum memasang

1. Cadangkan file website lama dan data penting Firestore.
2. Buka Firebase Console dan pilih proyek `hgn-lambar-2026`.
3. Pada **Authentication → Sign-in method**, aktifkan:
   - **Email/Password** (untuk admin dan peserta/stan).
   - **Anonymous** (dibutuhkan untuk formulir olahraga dan seni yang tidak meminta peserta login).
4. Pastikan UID admin pada `firestore.rules` dan `index.html` adalah UID akun admin yang benar:
   `qMepfpYhfqPLTE47eysdUlwoWbj2`
5. Jangan membagikan kata sandi admin.

## Cara memasang

### A. Perbarui website GitHub Pages
1. Ekstrak ZIP.
2. Buka folder `HGN-HUT-PGRI-LAMPUNG-BARAT-GITHUB`.
3. Ganti `index.html` pada repositori GitHub dengan `index.html` dari paket ini.
4. Commit dan push perubahan. Tunggu GitHub Pages selesai menerbitkan website.

### B. Perbarui Firestore Rules
1. Firebase Console → **Firestore Database → Rules**.
2. Cadangkan aturan lama di file teks.
3. Salin seluruh isi `firestore.rules` dari paket ini, ganti isi Rules di Firebase, lalu tekan **Publish**.
4. Jika Firebase menampilkan error, jangan menghapus blok aturan secara acak; salin pesan error dan periksa baris yang ditunjukkan.

### C. Masukkan tautan juknis
Paket ini menyimpan **tautan** juknis per kategori, bukan mengunggah file PDF ke Firestore. Untuk menghindari biaya Firebase Storage dan batas ukuran dokumen Firestore:
1. Unggah PDF juknis ke Google Drive atau hosting yang dapat diakses peserta.
2. Atur izin file agar peserta yang memiliki tautan dapat membukanya.
3. Login admin → tab **Real-Time Editor & Logo Upload**.
4. Isi tautan Juknis Kategori GTK, Olahraga, dan Seni Pertunjukan.
5. Klik **Simpan Juknis Kategori**.

## Koleksi Firestore yang digunakan

Semua koleksi berada di namespace yang sudah digunakan aplikasi:
`artifacts/hgn-pgri-lampungbarat-2026/public/data/`

- `settings` — konfigurasi, kategori, timeline, tautan juknis, dan galeri logo tambahan (`site_logo_gallery`).
- `users` — profil akun peserta, hanya admin dapat melihat daftar semua profil.
- `submissions` — tautan berkas karya peserta.
- `event_registrations` — data pendaftaran lengkap, termasuk kontak dan anggota; hanya admin atau pemilik terkait yang dapat membacanya.
- `public_registrations` — ringkasan pendaftar yang aman untuk ditampilkan di halaman publik.
- `announcements` — pengumuman publik.

Koleksi baru dibuat otomatis saat pendaftaran pertama kali disimpan; tidak perlu membuat koleksi manual.

## Pengujian setelah deploy

Lihat `CHECKLIST-PENGUJIAN.md`. Minimal uji:
- login admin dan peserta;
- cabang tampil dalam tiga kategori;
- pendaftaran olahraga dan drumband tanpa login interaktif;
- pendaftaran stan dan verifikasi akun;
- upload tautan berkas untuk akun yang sudah diverifikasi;
- status pendaftaran dan ekspor CSV;
- pengumuman, kategori, juknis, timeline, galeri logo tambahan, dan sinkronisasi perangkat.

## Batasan dan catatan

- File sudah diperiksa secara statis untuk sintaks JavaScript dan struktur HTML, tetapi koneksi langsung ke proyek Firebase milik pengguna tidak dapat diuji dari lingkungan pembuatan paket. Pengujian nyata setelah deploy tetap wajib.
- Sistem pendaftaran olahraga/seni publik tetap berpotensi menerima spam. Untuk pemakaian resmi berskala besar, pertimbangkan Firebase App Check dan pemantauan pendaftaran.
- Penghapusan akun Authentication tidak otomatis menghapus dokumen Firestore atau berkas Google Drive yang terkait.
