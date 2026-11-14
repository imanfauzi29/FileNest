# Dashboard — Implementation Specification

## 1. Overview

Dashboard merupakan halaman utama aplikasi Desktop & Storage Manager.

Tujuan halaman:
- Memberikan ringkasan kondisi folder yang dikelola.
- Menampilkan penggunaan penyimpanan.
- Menampilkan aktivitas terbaru.
- Menampilkan rekomendasi pengelolaan file.
- Menampilkan status pekerjaan background.
- Memberikan akses cepat ke fitur utama.

Referensi desain: `image-1.jpg`

Implementasikan tampilan dengan mengikuti referensi visual tersebut. Jangan menambahkan elemen AI chatbot, gradient dekoratif, atau komponen yang tidak diperlukan.

## 2. Layout

Dashboard terdiri dari:

1. Sidebar Navigation
2. Page Header
3. Summary Cards
4. Storage Usage
5. Folder Distribution
6. Managed Folders
7. Recent Activities
8. Recommendations
9. Job Status
10. Storage History

Gunakan layout desktop dengan sidebar tetap di sebelah kiri dan konten utama dapat di-scroll.

## 3. Sidebar Navigation

Menu:

- Overview
- Files
- Storage
- Organization
- Smart Rename
- Monitoring
- History
- Managed Folders
- Settings

Behavior:

- Klik menu membuka halaman terkait.
- Menu aktif memiliki background highlight.
- Managed Folders dapat di-expand dan collapse.
- Daftar Managed Folders menampilkan folder yang telah didaftarkan.
- Klik nama folder membuka halaman Files pada folder tersebut.
- Tombol Tambah Folder membuka dialog pemilihan folder Windows.
- Jangan menampilkan folder yang belum didaftarkan.

## 4. Page Header

Menampilkan:

- Title: Overview
- Description: Ringkasan penyimpanan, aktivitas, dan status pengelolaan folder.
- Tombol Refresh.
- Tombol Analisis Folder.
- Dropdown pada tombol Analisis Folder.

### Refresh

Ketika diklik:
- Memuat ulang data dashboard dari database lokal.
- Memperbarui statistik dan status pekerjaan.
- Tidak menjalankan pemindaian filesystem.

### Analisis Folder

Dropdown berisi:

- Analisis Semua Folder
- Analisis Folder Tertentu
- Scan Metadata Saja
- Analisis Mendalam dengan AI

Behavior:
- Analisis Semua Folder memproses seluruh Managed Folders yang aktif.
- Analisis Folder Tertentu membuka dialog pemilihan folder.
- Scan Metadata Saja tidak memanggil AI.
- Analisis Mendalam menggunakan Hermes melalui 9Router.
- Tampilkan progress selama proses berjalan.
- Cegah duplikasi pekerjaan scan yang sama.

## 5. Summary Cards

Terdiri dari empat kartu.

### Folder Dikelola
Menampilkan jumlah folder yang terdaftar dan aktif.

### Total File
Menampilkan jumlah file yang sudah terindeks.

### Total Ukuran
Menampilkan total ukuran file yang sudah terindeks.

### Perubahan Tertunda
Menampilkan jumlah operasi yang menunggu persetujuan.

Behavior:
- Setiap kartu dapat diklik.
- Folder Dikelola membuka Managed Folders.
- Total File membuka Files.
- Total Ukuran membuka Storage.
- Perubahan Tertunda membuka Review Changes.

Data harus berasal dari database, bukan nilai statis.

## 6. Storage Usage

Menampilkan diagram donut penggunaan penyimpanan berdasarkan kategori file.

Kategori:
- Dokumen
- Gambar
- Video
- Arsip
- Lainnya

Setiap kategori menampilkan:
- Nama kategori.
- Persentase.
- Ukuran penyimpanan.

Behavior:
- Hover pada bagian diagram menampilkan tooltip.
- Klik kategori membuka Storage dengan filter kategori tersebut.
- Jika data belum tersedia, tampilkan empty state.
- Jangan mengarang statistik.

## 7. Folder Distribution

Menampilkan distribusi ukuran setiap Managed Folder.

Setiap item menampilkan:
- Nama folder.
- Path folder.
- Ukuran.
- Persentase terhadap total ukuran folder terkelola.
- Progress bar.

Behavior:
- Klik item membuka folder terkait di Files.
- Urutkan berdasarkan ukuran terbesar.
- Tampilkan maksimal lima folder pada dashboard.
- Jika folder lebih dari lima, sediakan View All.

## 8. Managed Folders

Menampilkan daftar folder yang dikelola.

Setiap baris berisi:
- Icon folder.
- Nama folder.
- Full path.
- Total ukuran.
- Jumlah file.
- Toggle monitoring.
- Context menu (titik tiga).

### Toggle Monitoring

- ON: aktifkan monitoring perubahan filesystem.
- OFF: hentikan monitoring folder tersebut.
- Perubahan status harus disimpan di database.
- Jangan menghapus data hasil scan saat monitoring dimatikan.

### Context Menu (Titik Tiga)

Menu yang tersedia:

1. Open Folder
   - Membuka folder melalui Windows File Explorer.

2. Scan Now
   - Menjalankan pemindaian folder.

3. View Analysis
   - Membuka halaman Storage dengan folder tersebut sebagai filter.

4. Monitoring Settings
   - Membuka pengaturan monitoring folder.

5. Folder Settings
   - Membuka konfigurasi folder.

6. Remove from Managed Folders
   - Menghapus registrasi folder dari aplikasi.
   - Tidak menghapus folder atau file asli.
   - Tampilkan confirmation dialog sebelum menghapus.

## 9. Recent Activities

Menampilkan aktivitas terbaru.

Kolom:
- Waktu
- Aktivitas
- Lokasi
- Detail

Jenis aktivitas:
- Scan Completed
- Rename Planned
- Folder Organization
- File Added
- File Modified
- File Moved
- Duplicate Detected
- Rule Executed
- Operation Failed

Behavior:
- Klik baris membuka detail aktivitas.
- View All membuka History.
- Tampilkan maksimal lima aktivitas terbaru.
- Gunakan pagination pada halaman History.

## 10. Recommendations

Menampilkan rekomendasi yang ditemukan dari hasil analisis.

Contoh:

- Rapikan struktur folder.
- Perbaiki nama file.
- Kelola file duplikat.

Setiap rekomendasi memiliki:
- Judul.
- Deskripsi singkat.
- Jumlah file terdampak jika tersedia.
- Tombol atau area klik untuk melihat detail.

Behavior:
- Klik rekomendasi membuka fitur terkait.
- Rekomendasi organisasi membuka Organization.
- Rekomendasi rename membuka Smart Rename.
- Rekomendasi duplikat membuka Storage > Duplicates.

Rekomendasi tidak boleh langsung mengeksekusi perubahan.

## 11. Job Status

Menampilkan pekerjaan background yang sedang berjalan atau tertunda.

Contoh:
- Analisis D:\Projects
- Rencana Organisasi
- Analisis Duplikat

Setiap pekerjaan menampilkan:
- Nama pekerjaan.
- Progress percentage.
- Progress bar.
- Status.
- Action yang tersedia.

Status:
- Queued
- Running
- Completed
- Failed
- Paused
- Cancelled

Behavior:
- Running menampilkan progress.
- Queued menampilkan status menunggu.
- Failed menyediakan akses ke error detail.
- Pause dan Resume hanya ditampilkan jika pekerjaan mendukungnya.
- Klik pekerjaan membuka detail task.

## 12. Storage History

Menampilkan grafik perubahan penggunaan penyimpanan berdasarkan waktu.

Default:
- Tujuh hari terakhir.

Informasi:
- Tanggal.
- Total ukuran terindeks.
- Jumlah file yang ditambahkan.
- Jumlah file yang diubah nama.
- Jumlah file yang dipindahkan.
- Jumlah file yang dihapus.

Behavior:
- Hover grafik menampilkan tooltip.
- Data diambil dari histori scan dan action logs.
- Jangan menganggap file yang dihapus dari disk sebagai penghapusan permanen oleh aplikasi.

## 13. Loading, Empty, dan Error States

Semua komponen harus mempunyai state:

### Loading
Tampilkan skeleton atau progress indicator.

### Empty
Jika belum ada Managed Folder:
- Tampilkan pesan bahwa belum ada folder yang dikelola.
- Tampilkan tombol Tambah Folder.

Jika belum ada aktivitas:
- Tampilkan pesan belum ada aktivitas.

Jika belum ada rekomendasi:
- Tampilkan pesan belum ada rekomendasi.

### Error
- Tampilkan pesan kesalahan yang mudah dimengerti.
- Sediakan tombol Retry jika memungkinkan.
- Jangan menampilkan stack trace kepada pengguna.

## 14. Technical Requirements

- Frontend: React + TypeScript.
- Desktop: Tauri 2.
- Backend: Python + FastAPI.
- Database: SQLite.
- Ikuti komponen dan design system global aplikasi.
- Gunakan data dari API backend.
- Jangan menggunakan hardcoded dummy data pada implementasi final.
- Jangan mengakses filesystem langsung dari komponen frontend.
- Semua operasi filesystem dilakukan melalui backend.

## 15. Constraints

- Dashboard hanya menampilkan data dari Managed Folders.
- Jangan melakukan scan otomatis hanya karena dashboard dibuka.
- Jangan menjalankan operasi rename atau move dari dashboard.
- Semua perubahan file harus melalui Transaction Manager.
- Semua operasi harus tercatat dalam audit log.
- AI tidak boleh mengeksekusi operasi filesystem secara langsung.

## 16. Acceptance Criteria

- [ ] Dashboard dapat dibuka sebagai halaman utama.
- [ ] Sidebar navigation bekerja.
- [ ] Managed Folders ditampilkan sesuai database.
- [ ] Tambah folder dapat dilakukan.
- [ ] Toggle monitoring bekerja.
- [ ] Context menu bekerja sesuai fungsinya.
- [ ] Refresh tidak memicu scan.
- [ ] Analisis Folder dapat membuat background task.
- [ ] Summary Cards menampilkan data aktual.
- [ ] Storage Usage menampilkan data aktual.
- [ ] Recent Activities menampilkan riwayat.
- [ ] Recommendations membuka fitur terkait.
- [ ] Job Status menampilkan status pekerjaan.
- [ ] Loading, empty, dan error states tersedia.
- [ ] Tampilan mengikuti referensi `image-1.jpg`.

## 17. Implementation Notes

Prioritaskan kesesuaian visual dengan `image-1.jpg`, tetapi jangan mengorbankan fungsionalitas.

Jangan membuat fitur tambahan di luar spesifikasi tanpa persetujuan.

Jika API atau backend belum tersedia:
- Buat UI dan state yang diperlukan.
- Gunakan mock service sementara yang terpisah.
- Jangan mencampur mock data dengan implementasi API final.

Laporkan fitur yang sudah selesai, belum selesai, dan kendala implementasi.