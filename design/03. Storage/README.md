\# Feature 03 — Storage Analyzer



\## 1. Overview



Storage Analyzer digunakan untuk menganalisis penggunaan ruang penyimpanan pada seluruh Managed Folders yang telah didaftarkan pengguna.



Fitur ini membantu pengguna memahami distribusi storage, menemukan file berukuran besar, mendeteksi file duplikat, mengidentifikasi folder kosong, dan melihat peluang penghematan storage.



Storage Analyzer bersifat read-only. Semua perubahan filesystem harus melalui halaman Review Changes dan Transaction Manager.



\## 2. Layout



Halaman mengikuti layout utama aplikasi:



1\. Sidebar Navigation

2\. Page Header

3\. Summary Cards

4\. Analysis Tabs

5\. Analysis Content



\### Sidebar



Gunakan sidebar yang konsisten dengan Dashboard dan Files.



Menu:

\- Overview

\- Files

\- Storage

\- Organization

\- Smart Rename

\- Monitoring

\- History

\- Managed Folders

\- Settings



Menu Storage harus aktif ketika halaman ini dibuka.



\### Page Header



Judul: `Storage Analyzer`



Deskripsi: `Analyze storage usage and discover opportunities to free up space.`



Komponen:

\- Last Analyzed

\- Refresh

\- Analyze Now

\- Dropdown Analyze Now



Dropdown Analyze Now:

\- Analyze All Managed Folders

\- Analyze Selected Folder



Perilaku:

\- Last Analyzed menampilkan waktu analisis terakhir.

\- Refresh hanya memuat ulang hasil dari database.

\- Analyze Now menjalankan analisis melalui backend.

\- Analisis harus berjalan sebagai background job.



\## 3. Summary Cards



Tampilkan empat kartu ringkasan dalam satu baris.



\### Total Storage



Menampilkan:

\- Total ukuran seluruh file.

\- Total jumlah file.



Contoh:

\- 482.6 GB

\- 37,812 files



\### Large Files



Menampilkan:

\- Jumlah file berukuran besar.

\- Total ukuran file tersebut.

\- Persentase terhadap total storage.



Contoh:

\- 248 files

\- 356.8 GB (73.9%)



Klik kartu membuka tab Large Files.



\### Duplicate Files



Menampilkan:

\- Jumlah grup duplikat.

\- Estimasi ukuran yang berpotensi dihemat.



Contoh:

\- 24 groups

\- 18.4 GB potential savings



Klik kartu membuka tab Duplicates.



\### Empty Folders



Menampilkan:

\- Jumlah folder kosong.



Contoh:

\- 132 folders



Klik kartu membuka tab Empty Folders.



Semua angka harus berasal dari hasil analisis aktual. Jangan menggunakan data dummy ketika aplikasi sudah terhubung ke backend.



\## 4. Analysis Tabs



Sediakan lima tab:



\- Overview

\- Large Files

\- Duplicates

\- File Types

\- Empty Folders



Tab harus mempertahankan filter yang masih relevan ketika pengguna berpindah halaman.



\## 5. Overview Tab



Overview merupakan halaman utama Storage Analyzer.



\### 5.1 Storage Distribution by File Type



Tampilkan donut chart distribusi storage berdasarkan kategori file.



Kategori:

\- Documents

\- Images

\- Videos

\- Audio

\- Archives

\- Others



Setiap kategori menampilkan:

\- Type

\- Files

\- Size

\- Percentage



Di tengah donut chart tampilkan total storage.



Interaksi:

\- Hover pada chart menampilkan detail kategori.

\- Klik kategori membuka tab File Types dengan filter kategori tersebut.

\- Tooltip menampilkan jumlah file dan ukuran.



\### 5.2 Largest Folders



Tampilkan daftar folder dengan penggunaan storage terbesar.



Kolom:

\- Folder

\- Size

\- Files

\- Percentage



Default sorting berdasarkan ukuran terbesar.



Tampilkan maksimal beberapa folder teratas pada Overview. Sediakan tombol View All untuk membuka daftar lengkap.



Interaksi:

\- Klik folder membuka folder pada halaman Files.

\- Klik View All membuka daftar Largest Folders.

\- Tampilkan lokasi folder secara lengkap atau gunakan tooltip jika terlalu panjang.



\### 5.3 Recommendations



Tampilkan rekomendasi berdasarkan hasil analisis.



Jenis rekomendasi:



\*\*Review large files\*\*

\- Jumlah file besar.

\- Total ukuran file.

\- Tombol View Files.



\*\*Manage duplicate files\*\*

\- Jumlah grup duplikat.

\- Estimasi ukuran yang dapat dihemat.

\- Tombol View Duplicates.



\*\*Review empty folders\*\*

\- Jumlah folder kosong.

\- Tombol View Folders.



\*\*Review file types\*\*

\- Kategori file yang menggunakan storage paling besar.

\- Tombol View File Types.



Perilaku:

\- Tombol rekomendasi hanya membuka halaman analisis terkait.

\- Tidak boleh langsung menghapus atau memindahkan file.

\- Jangan menyebut ukuran sebagai ruang yang pasti dapat dihemat sebelum tindakan benar-benar dilakukan.



\### 5.4 Storage Usage Trend



Tampilkan line chart penggunaan storage dari waktu ke waktu.



Default:

\- Last 7 Days



Pilihan rentang:

\- Last 7 Days

\- Last 30 Days

\- Last 90 Days

\- All Time



Data:

\- Date

\- Total Storage



Interaksi:

\- Hover menampilkan tanggal dan total penggunaan storage.

\- Perubahan rentang memperbarui chart.

\- Jika histori belum tersedia, tampilkan empty state.



Data trend berasal dari snapshot hasil analisis yang tersimpan di database. Jangan mengarang histori sebelum tersedia.



\## 6. Large Files Tab



Menampilkan file dengan ukuran besar.



\### Filters



\- Managed Folder

\- File Type

\- Minimum Size

\- Modified Date



Default sorting:

\- Size descending



\### Table Columns



\- Checkbox

\- File Name

\- Location

\- Size

\- Type

\- Modified Date



\### Actions



\- Open File

\- Open File Location

\- View Details

\- Analyze File

\- Copy Path

\- Select Multiple



Jika pengguna memilih beberapa file, tampilkan selection toolbar.



Jangan menyediakan penghapusan langsung. Pengguna dapat membuat usulan perubahan melalui Review Changes.



\## 7. Duplicates Tab



Menampilkan file duplikat berdasarkan content hash.



\### Duplicate Detection



Tahapan:

1\. Kelompokkan file berdasarkan ukuran.

2\. Lakukan pemeriksaan hash pada kandidat dengan ukuran sama.

3\. File dengan hash identik dimasukkan ke grup duplikat.



Nama file yang sama tidak cukup untuk menyatakan file sebagai duplikat.



\### Duplicate Groups



Setiap grup menampilkan:

\- File Name

\- Number of Copies

\- Total Size

\- Potential Savings

\- File Locations



\### Duplicate Details



Ketika grup dibuka, tampilkan:



\- Checkbox

\- File Name

\- Location

\- Size

\- Modified Date

\- File Hash



Aksi:

\- Open

\- Open Location

\- Copy Path

\- Compare Details

\- Select as Keep

\- Mark for Review



`Select as Keep` hanya menandai file yang ingin dipertahankan.



`Mark for Review` membuat usulan perubahan untuk ditinjau melalui Review Changes.



Tidak boleh menghapus file duplikat secara otomatis.



\## 8. File Types Tab



Menampilkan distribusi file berdasarkan ekstensi.



Contoh:

\- .jpg

\- .png

\- .pdf

\- .docx

\- .xlsx

\- .mp4

\- .zip

\- Others



\### File Type Table



Kolom:

\- Extension

\- File Count

\- Total Size

\- Average Size

\- Percentage



Aksi:

\- View Files

\- Analyze Type



Klik extension membuka halaman Files dengan filter ekstensi terkait.



Ekstensi yang tidak dikenal dimasukkan ke kategori Others.



\## 9. Empty Folders Tab



Menampilkan folder yang benar-benar tidak memiliki file maupun subfolder.



\### Table Columns



\- Checkbox

\- Folder Name

\- Location

\- Created Date

\- Modified Date



\### Actions



\- Open Folder

\- Copy Path

\- View Details

\- Mark for Review



Folder kosong tidak boleh langsung dihapus.



Folder yang memiliki file tersembunyi, file sistem, atau isi yang tidak dapat diakses tidak boleh dianggap kosong tanpa pemeriksaan lebih lanjut.



\## 10. Search and Filters



Sediakan pencarian dan filter sesuai tab.



Filter umum:

\- Managed Folder

\- File Type

\- File Size

\- Modified Date



Perilaku:

\- Search hanya bekerja dalam Managed Folders.

\- Filter dapat dikombinasikan.

\- Sediakan Clear Filters.

\- Tampilkan jumlah hasil.

\- Tampilkan empty state jika tidak ada hasil.



\## 11. Analyze Workflow



Ketika pengguna menjalankan Analyze Now:



1\. Tampilkan pilihan folder yang akan dianalisis.

2\. Pengguna memilih satu atau seluruh Managed Folders.

3\. Frontend mengirim permintaan ke backend.

4\. Backend membuat analysis job.

5\. Proses berjalan di background.

6\. Tampilkan progress analisis.

7\. Hasil analisis disimpan ke SQLite.

8\. Summary Cards, chart, dan tabel diperbarui.



Informasi progress:

\- Analysis Status

\- Current Folder

\- Files Processed

\- Total Files

\- Elapsed Time

\- Cancel Analysis



Jika proses gagal pada sebagian folder, tampilkan hasil yang berhasil dan daftar folder yang gagal secara terpisah.



\## 12. UI States



\### Loading



Tampilkan skeleton pada:

\- Summary Cards

\- Charts

\- Largest Folders

\- Recommendations

\- Tables



\### Empty State



Jika belum ada hasil analisis:

\- Tampilkan pesan bahwa storage belum dianalisis.

\- Tampilkan tombol Analyze Now.

\- Jangan menampilkan data dummy.



\### Analyzing



Tampilkan status dan progress job.



\### No Results



Jika filter tidak menemukan hasil:

\- Tampilkan pesan tidak ada hasil.

\- Sediakan Clear Filters.



\### Error



Tampilkan pesan error yang mudah dipahami dan opsi untuk mencoba kembali.



\### Partial Failure



Tampilkan folder yang berhasil dianalisis dan folder yang gagal dianalisis.



\## 13. Data Requirements



\### Storage Analysis



\- id

\- managed\_folder\_id

\- total\_size

\- total\_files

\- analyzed\_at

\- status



\### File Analysis



\- file\_id

\- path

\- name

\- extension

\- size

\- modified\_at

\- content\_hash

\- managed\_folder\_id



\### Duplicate Group



\- id

\- content\_hash

\- file\_count

\- total\_size

\- potential\_savings

\- analyzed\_at



\### Storage Snapshot



\- id

\- total\_size

\- total\_files

\- captured\_at



\### Empty Folder



\- id

\- path

\- managed\_folder\_id

\- created\_at

\- modified\_at

\- analyzed\_at



Seluruh data harus terhubung dengan Managed Folders.



\## 14. Technical Requirements



\- Backend menggunakan Python.

\- Database menggunakan SQLite.

\- Proses analisis berjalan sebagai background job.

\- Gunakan hashing untuk mendeteksi file duplikat.

\- Gunakan chunked hashing untuk file besar.

\- Hindari membaca isi file jika metadata sudah cukup.

\- Simpan snapshot untuk Storage Usage Trend.

\- Frontend hanya menampilkan data dan mengirim permintaan analisis.

\- Jangan mengikuti symbolic links, junctions, atau reparse points secara default.

\- Validasi canonical path sebelum mengakses file.

\- Jangan melakukan scanning di luar Managed Folders.

\- Semua operasi filesystem yang mengubah data harus melalui Transaction Manager.

\- Catat aktivitas analisis ke History.



\## 15. Safety Constraints



Storage Analyzer bersifat read-only.



Dilarang:

\- Menghapus file secara langsung.

\- Memindahkan file secara langsung.

\- Mengubah nama file.

\- Mengubah isi file.

\- Mengakses folder di luar Managed Folders.

\- Menganggap file dengan nama atau ukuran sama sebagai duplikat tanpa verifikasi hash.



Semua perubahan harus:

1\. Dibuat sebagai change plan.

2\. Ditampilkan di Review Changes.

3\. Disetujui pengguna atau aturan yang sudah disetujui sebelumnya.

4\. Dijalankan melalui Transaction Manager.



\## 16. Acceptance Criteria



\- \[ ] Sidebar Storage aktif pada halaman ini.

\- \[ ] Last Analyzed menampilkan waktu analisis terakhir.

\- \[ ] Refresh hanya memuat data dari database.

\- \[ ] Analyze Now dapat menganalisis semua atau folder tertentu.

\- \[ ] Summary Cards menampilkan data aktual.

\- \[ ] Storage Distribution menampilkan distribusi kategori file.

\- \[ ] Largest Folders menampilkan folder berdasarkan ukuran.

\- \[ ] Recommendations mengarahkan ke tab terkait.

\- \[ ] Storage Usage Trend menggunakan snapshot historis.

\- \[ ] Large Files dapat dicari, difilter, dan diurutkan.

\- \[ ] Duplicate Detection menggunakan content hash.

\- \[ ] Duplicate Details menampilkan lokasi setiap salinan.

\- \[ ] File Types menampilkan distribusi ekstensi.

\- \[ ] Empty Folders hanya menampilkan folder yang benar-benar kosong.

\- \[ ] Background analysis menampilkan progress.

\- \[ ] Error dan partial failure ditangani.

\- \[ ] Tidak ada penghapusan atau pemindahan langsung.

\- \[ ] Aktivitas analisis tercatat di History.

\- \[ ] Seluruh proses hanya bekerja dalam Managed Folders.



\## 17. Design Reference



Gunakan `image-1` sebagai referensi visual halaman Storage Analyzer.



Ketentuan:

\- Pertahankan sidebar dan visual language dari Dashboard dan Files.

\- Gunakan background putih atau abu-abu sangat terang.

\- Gunakan navy untuk sidebar.

\- Gunakan biru sebagai warna aksen utama.

\- Gunakan card dengan border halus dan radius konsisten.

\- Hindari dekorasi AI, gradient berlebihan, dan elemen yang tidak memiliki fungsi.

\- Chart harus mudah dibaca.

\- Tabel harus konsisten dengan halaman Files.



Jika terdapat perbedaan antara gambar dan spesifikasi perilaku, README ini menjadi acuan utama implementasi.

