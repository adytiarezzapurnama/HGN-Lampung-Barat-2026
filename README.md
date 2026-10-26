# HGN & HUT PGRI Ke-81 Kabupaten Lampung Barat

Website statis untuk informasi lomba, pendaftaran peserta, portal peserta, pengumpulan tautan Google Drive, pengumuman, dan portal admin.

## File
- `index.html` — aplikasi utama.
- `.gitignore` — pengaturan Git.

## Deploy ke GitHub Pages
1. Unggah file `index.html` ke root repository.
2. Buka **Settings → Pages**.
3. Pilih branch `main` dan folder `/ (root)`, lalu simpan.

## Konfigurasi Firebase
Aplikasi menggunakan Firebase Authentication (Anonymous) dan Cloud Firestore melalui SDK CDN. Pastikan konfigurasi pada blok `firebaseConfig` mengarah ke proyek Firebase yang benar, Anonymous Authentication aktif, dan Firestore dibuat pada paket Spark jika ingin tetap gratis tanpa kartu pembayaran.

Aturan Firestore harus disusun sesuai kebutuhan akses. Jangan gunakan aturan `allow read, write: if true;` untuk data peserta. Autentikasi anonim sendiri tidak membuktikan bahwa pengguna adalah admin; proteksi admin di aplikasi statis bukan pengganti otorisasi server. Uji di lingkungan terbatas sebelum mengumpulkan data peserta sebenarnya.

## Kelola cabang lomba
Login ke portal admin, lalu pilih tab **Kelola Cabang Lomba**. Admin dapat menambah, mengedit, atau menghapus cabang; nama, deskripsi, persyaratan, dan ikon dapat diatur. Daftar disimpan pada browser dan didorong ke Firestore pada dokumen `settings/categories_config` untuk sinkronisasi antarperangkat.

## Catatan penting
- Peserta memasukkan tautan Google Drive mereka sendiri; website tidak mengunggah file langsung ke Drive panitia.
- Penghapusan cabang hanya menghapusnya dari daftar aktif; riwayat pengumpulan lama tidak otomatis dihapus.
- Pastikan akses folder Drive peserta dapat dibuka panitia/juri.
- Jangan menaruh password rahasia, service-account key, atau kredensial server di repository publik.
