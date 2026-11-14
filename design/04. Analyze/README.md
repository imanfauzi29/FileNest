\# Feature 04 — Organization



\## 1. Overview



Organization digunakan untuk menganalisis dan menyusun ulang struktur folder serta file menggunakan bantuan AI.



Pengguna memilih Managed Folder, menentukan tujuan organisasi, lalu sistem menganalisis isi folder dan menghasilkan rekomendasi struktur baru beserta daftar perubahan yang diperlukan.



AI hanya bertugas menganalisis dan menghasilkan rekomendasi. Seluruh perubahan filesystem harus melalui Change Plan, Review Changes, dan Transaction Manager.



\### Tujuan



\- Membuat struktur folder lebih rapi.

\- Mengelompokkan file berdasarkan tipe atau konteks.

\- Memindahkan file ke lokasi yang sesuai.

\- Mengidentifikasi file yang belum terorganisasi.

\- Membuat aturan organisasi yang dapat digunakan kembali.

\- Mendukung eksekusi manual maupun berdasarkan Approved Rules.



\## 2. Layout



Halaman menggunakan layout utama aplikasi:



1\. Sidebar Navigation

2\. Page Header

3\. Organization Tabs

4\. Configuration Panel

5\. Analysis Result

6\. Structure Comparison

7\. Change Plan



\### Sidebar



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



Menu Organization harus aktif.



\### Page Header



Judul: `Organization`



Deskripsi: `Analyze and organize files into a cleaner and more structured folder layout using AI.`



Komponen:

\- Last Analysis

\- Refresh

\- Analyze \& Plan

\- Dropdown Analyze \& Plan



Dropdown:

\- Analyze All Managed Folders

\- Analyze Selected Folder



Refresh hanya memuat data yang sudah tersimpan. Tidak menjalankan analisis ulang.



\## 3. Organization Tabs



Sediakan empat tab:



1\. Create Plan

2\. Review Plan

3\. Organization Rules

4\. History



\### Create Plan



Digunakan untuk memilih folder, menentukan tujuan organisasi, dan membuat rekomendasi struktur baru.



\### Review Plan



Menampilkan seluruh Change Plan yang pernah dibuat dan statusnya.



\### Organization Rules



Menampilkan aturan organisasi yang telah disimpan dan disetujui pengguna.



\### History



Menampilkan aktivitas organisasi dan riwayat eksekusi.



\## 4. Create Plan



Create Plan dibagi menjadi dua area utama:



\- Configuration Panel di sebelah kiri.

\- Analysis Result dan Change Plan di sebelah kanan.



\### 4.1 Select Folder



Pengguna memilih folder yang akan dianalisis.



Komponen:

\- Managed Folder dropdown

\- Folder picker

\- Selected folder path



Perilaku:

\- Hanya menampilkan folder yang sudah terdaftar sebagai Managed Folder.

\- Pengguna dapat memilih satu folder untuk setiap plan.

\- Tampilkan lokasi folder secara lengkap.

\- Jangan mengizinkan path di luar Managed Folders.



Jika belum ada Managed Folder, tampilkan tombol untuk menambahkan folder terlebih dahulu.



\### 4.2 Organization Goal



Pengguna menentukan bagaimana file akan diorganisasi.



Sediakan tiga pilihan utama.



\*\*Organize by file type\*\*



Mengelompokkan file berdasarkan jenisnya.



Contoh struktur:

\- Documents

\- Images

\- Videos

\- Audio

\- Archives

\- Applications

\- Others



\*\*Organize by project structure\*\*



Mengelompokkan file berdasarkan konteks proyek atau hubungan antarfile.



Contoh:

\- Source

\- Assets

\- Documents

\- Resources

\- Temporary

\- Archive



AI dapat menggunakan nama file, struktur direktori, metadata, dan konten yang diizinkan untuk menyarankan pengelompokan.



\*\*Custom (with AI)\*\*



Pengguna menjelaskan struktur yang diinginkan menggunakan bahasa natural.



Contoh:

\- Group files by project.

\- Move old files to Archive.

\- Separate images, documents, and source files.

\- Group files based on their related project.



Sediakan textarea untuk instruksi custom.



Instruksi custom harus divalidasi dan dibatasi pada folder yang dipilih.



\### 4.3 Options



Sediakan opsi berikut:



\*\*Include subfolders\*\*

\- Jika aktif, analisis mencakup subfolder.

\- Jika nonaktif, hanya isi folder utama yang dianalisis.



\*\*Suggest new folder structure\*\*

\- Mengizinkan AI menyarankan struktur folder baru.

\- Jika nonaktif, gunakan struktur folder yang sudah tersedia.



\*\*Detect and group related files\*\*

\- Menganalisis hubungan antarfile untuk menyarankan pengelompokan.



\*\*Move unorganized files only\*\*

\- Hanya mengusulkan pemindahan file yang belum berada pada struktur yang sesuai.

\- Tidak memindahkan file yang sudah terorganisasi.



\*\*Keep original structure as backup\*\*

\- Mengusulkan penyimpanan struktur awal sebagai backup.

\- Tidak boleh membuat backup secara otomatis tanpa persetujuan.



\### 4.4 Analyze \& Create Plan



Tombol utama untuk menjalankan analisis dan menghasilkan Change Plan.



Alur:

1\. Validasi folder dan konfigurasi.

2\. Kirim permintaan ke backend.

3\. Backend membuat analysis job.

4\. Hermes menjalankan analisis menggunakan AI.

5\. AI menghasilkan rekomendasi struktur folder.

6\. Backend memvalidasi rekomendasi.

7\. Backend menghasilkan Change Plan.

8\. Tampilkan Analysis Result dan Change Plan.



Proses berjalan sebagai background job.



Tampilkan status:

\- Queued

\- Running

\- Completed

\- Failed

\- Cancelled



Jangan melakukan perubahan filesystem pada tahap ini.



\## 5. Analysis Result



Setelah analisis selesai, tampilkan ringkasan hasil.



\### Summary Cards



Empat kartu:



\*\*Files Analyzed\*\*

\- Jumlah file yang dianalisis.



\*\*Suggested Folders\*\*

\- Jumlah folder yang direkomendasikan.



\*\*Files to Move\*\*

\- Jumlah file yang akan dipindahkan berdasarkan plan.



\*\*Total Size\*\*

\- Total ukuran file yang dianalisis.



Semua nilai berasal dari hasil analisis aktual.



\### Re-analyze



Tombol Re-analyze menjalankan analisis ulang dengan konfigurasi yang sama.



Sebelum membuat hasil baru, simpan hasil analisis sebelumnya sebagai riwayat. Jangan mengubah atau menghapus plan yang sudah dibuat.



\## 6. Structure Comparison



Tampilkan dua panel berdampingan.



\### 6.1 Current Structure



Menampilkan struktur folder saat ini.



Contoh:



Mobile App

\- assets

\- src

\- temp

\- download

\- other



Setiap folder dapat menampilkan:

\- Nama folder

\- Jumlah file

\- Ukuran folder jika tersedia



\### 6.2 Proposed Structure



Menampilkan struktur folder yang direkomendasikan AI.



Contoh:



Mobile App

\- 01\_Source

\- 02\_Assets

\- 03\_Documents

\- 04\_Resources

\- 05\_Temporary

\- 06\_Archive



Setiap folder menampilkan:

\- Nama folder

\- Jumlah file yang akan ditempatkan

\- Ukuran total jika tersedia



\### 6.3 Comparison Behavior



\- Kedua struktur harus dapat di-expand dan collapse.

\- Klik folder untuk melihat detail file di dalamnya.

\- Tampilkan perbedaan struktur secara visual.

\- Tampilkan folder baru dengan indikator New.

\- Tampilkan folder yang tidak berubah tanpa indikator perubahan.

\- Tampilkan file yang akan dipindahkan beserta lokasi asal dan tujuan.



Struktur yang diusulkan bukan berarti sudah diterapkan pada filesystem.



\## 7. Change Plan



Change Plan berisi daftar operasi yang dihasilkan dari analisis.



\### Summary



Tampilkan:

\- Total changes

\- Files to move

\- Folders to create

\- Potential conflicts

\- Estimated total size



\### Table Columns



\- Number

\- Action

\- Source

\- Destination

\- Status



Contoh operasi:



| Action | Source | Destination |

|---|---|---|

| Move | assets/\* | 02\_Assets/ |

| Move | src/\* | 01\_Source/ |

| Move | \*.pdf, \*.docx | 03\_Documents/ |

| Move | temp/\* | 05\_Temporary/ |



Data di atas hanya contoh tampilan. Implementasi harus menggunakan hasil analisis aktual.



\### Actions



\*\*View Details\*\*



Membuka seluruh daftar operasi secara lengkap.



\*\*Save Plan\*\*



Menyimpan Change Plan sebagai draft untuk ditinjau nanti.



\*\*Review Changes\*\*



Membuka halaman Review Changes dengan plan yang sudah dibuat.



Tidak boleh menjalankan perubahan filesystem langsung dari tombol Save Plan atau Analyze \& Plan.



\## 8. Review Plan Tab



Menampilkan daftar seluruh plan yang pernah dibuat.



\### Table Columns



\- Plan Name

\- Managed Folder

\- Created At

\- Total Changes

\- Status

\- Actions



Status:

\- Draft

\- Pending Review

\- Approved

\- Executing

\- Completed

\- Failed

\- Rejected

\- Cancelled



\### Actions



\- View Plan

\- Continue Review

\- Duplicate Plan

\- Delete Draft



Delete Draft hanya menghapus data plan yang belum dieksekusi. Tidak menghapus file fisik.



Plan yang sudah disetujui atau dieksekusi tidak boleh dihapus dari riwayat.



\## 9. Organization Rules Tab



Menampilkan aturan organisasi yang sudah disimpan dan disetujui pengguna.



\### Rule Information



Setiap rule menampilkan:

\- Rule Name

\- Managed Folder Scope

\- Description

\- Organization Strategy

\- Created At

\- Last Executed

\- Status



Status:

\- Active

\- Paused

\- Disabled



\### Rule Actions



\- View Details

\- Edit Rule

\- Pause Rule

\- Enable Rule

\- Delete Rule



Perubahan rule yang memengaruhi cakupan atau tindakan harus memerlukan persetujuan ulang.



\### Approved Rules



Aturan yang telah disetujui dapat dijalankan otomatis hanya dalam batas:



\- Managed Folder yang telah disetujui.

\- Jenis operasi yang telah disetujui.

\- Pola file dan tujuan yang telah disetujui.

\- Kondisi yang telah ditentukan dalam rule.



Rule tidak boleh memperluas scope secara otomatis.



Operasi yang ambigu, konflik, atau berada di luar cakupan rule harus masuk Review Changes.



\## 10. History Tab



Menampilkan riwayat aktivitas Organization.



Informasi:

\- Timestamp

\- Folder

\- Action

\- Number of Files

\- Status

\- Executed By



Jenis aktivitas:

\- Analysis started

\- Analysis completed

\- Plan created

\- Plan saved

\- Plan approved

\- Rule created

\- Rule executed

\- Organization completed

\- Organization failed



Klik item untuk melihat detail aktivitas dan hasil eksekusi.



\## 11. Background Job



Analisis dan eksekusi organisasi harus menggunakan background worker.



Informasi job:

\- Job ID

\- Job Type

\- Managed Folder

\- Status

\- Progress

\- Files Processed

\- Total Files

\- Started At

\- Completed At

\- Error Details



Frontend harus dapat mengambil status job secara berkala melalui API.



Pengguna dapat meninggalkan halaman tanpa membatalkan job.



Cancel hanya tersedia untuk job yang masih dapat dibatalkan dengan aman.



\## 12. API Requirements



API dapat disesuaikan dengan arsitektur backend, tetapi minimal mendukung operasi berikut:



\### Create Analysis



`POST /api/organization/analyze`



Menerima:

\- managed\_folder\_id

\- organization\_goal

\- custom\_instruction

\- include\_subfolders

\- suggest\_new\_structure

\- detect\_related\_files

\- move\_unorganized\_only

\- keep\_original\_structure



Respons:

\- job\_id

\- status



\### Get Analysis Job



`GET /api/organization/jobs/{job\_id}`



Mengembalikan status dan progress analisis.



\### Get Analysis Result



`GET /api/organization/analyses/{analysis\_id}`



Mengembalikan hasil analisis dan struktur yang direkomendasikan.



\### Create Plan



`POST /api/organization/plans`



Membuat Change Plan berdasarkan hasil analisis.



\### Get Plans



`GET /api/organization/plans`



Mengambil daftar plan.



\### Get Plan Details



`GET /api/organization/plans/{plan\_id}`



Mengambil detail operasi dalam plan.



\### Save Rule



`POST /api/organization/rules`



Menyimpan rule organisasi yang telah disetujui.



\### Get Rules



`GET /api/organization/rules`



Mengambil daftar rule.



Endpoint di atas merupakan rancangan kontrak API. Sesuaikan implementasinya dengan konvensi backend yang sudah digunakan.



\## 13. Data Requirements



\### Organization Analysis



\- id

\- managed\_folder\_id

\- organization\_goal

\- configuration

\- status

\- files\_analyzed

\- created\_at

\- completed\_at



\### Organization Plan



\- id

\- analysis\_id

\- managed\_folder\_id

\- plan\_name

\- status

\- total\_changes

\- created\_at

\- updated\_at



\### Organization Plan Operation



\- id

\- plan\_id

\- operation\_type

\- source\_path

\- destination\_path

\- file\_count

\- status

\- validation\_result



\### Organization Rule



\- id

\- name

\- managed\_folder\_id

\- rule\_definition

\- approved\_scope

\- status

\- created\_at

\- updated\_at

\- last\_executed\_at



Simpan konfigurasi dan hasil analisis dalam format terstruktur. Jangan menjadikan output teks bebas dari AI sebagai sumber langsung untuk eksekusi filesystem.



\## 14. AI and Backend Requirements



\- Hermes menjadi orchestrator AI.

\- 9Router menjadi model gateway.

\- AI hanya menghasilkan rekomendasi dan struktur data terstruktur.

\- AI tidak boleh melakukan operasi filesystem secara langsung.

\- Validasi Change Plan dilakukan oleh backend.

\- Semua operasi harus melewati Transaction Manager.

\- MCP tools harus memiliki scope terbatas.

\- Jangan memberikan akses shell bebas kepada AI.

\- AI hanya boleh menerima data dari Managed Folders yang dipilih.

\- Pengiriman konten file ke model harus mengikuti pengaturan privasi dan izin pengguna.



Backend wajib memvalidasi:

\- Path sumber.

\- Path tujuan.

\- Scope Managed Folder.

\- File yang masih tersedia.

\- Perubahan metadata sejak analisis.

\- Collision pada destination.

\- Hak akses operasi.



\## 15. Safety Constraints



\- Tidak boleh memindahkan file saat proses analisis.

\- Tidak boleh membuat folder fisik saat proses analisis.

\- Tidak boleh menimpa file tujuan secara diam-diam.

\- Tidak boleh menghapus file secara otomatis.

\- Semua operasi harus masuk Change Plan.

\- Manual mode memerlukan persetujuan untuk setiap plan.

\- Approved Rules hanya boleh mengeksekusi operasi dalam scope yang disetujui.

\- Validasi ulang kondisi filesystem sebelum eksekusi.

\- Gunakan Transaction Manager untuk seluruh perubahan.

\- Catat seluruh operasi ke History.

\- Sediakan rollback best-effort jika operasi gagal.

\- Cross-volume move harus menggunakan copy, verify, lalu delete hanya jika operasi tersebut telah disetujui secara eksplisit.



\## 16. UI States



\### Initial State



Jika belum ada analisis:

\- Tampilkan form konfigurasi.

\- Tampilkan petunjuk untuk memilih Managed Folder.

\- Jangan tampilkan hasil dummy.



\### Analyzing



Tampilkan progress job dan informasi folder yang sedang dianalisis.



\### Analysis Completed



Tampilkan summary, comparison, dan Change Plan.



\### Analysis Failed



Tampilkan error dan opsi untuk mencoba kembali.



\### No Changes Suggested



Jika struktur folder sudah sesuai, tampilkan informasi bahwa tidak ada perubahan yang direkomendasikan.



\### Plan Pending Review



Tampilkan status bahwa plan menunggu persetujuan pengguna.



\## 17. Acceptance Criteria



\- \[ ] Organization menggunakan sidebar dan layout yang konsisten.

\- \[ ] Pengguna hanya dapat memilih Managed Folder.

\- \[ ] Tersedia tiga pilihan Organization Goal.

\- \[ ] Custom instruction dapat dimasukkan.

\- \[ ] Semua opsi konfigurasi berfungsi.

\- \[ ] Analyze \& Plan membuat background job.

\- \[ ] Hermes menghasilkan rekomendasi terstruktur.

\- \[ ] Analysis Result menampilkan data aktual.

\- \[ ] Current Structure dapat dibandingkan dengan Proposed Structure.

\- \[ ] Change Plan menampilkan source dan destination.

\- \[ ] Save Plan menyimpan draft.

\- \[ ] Review Changes membuka halaman Review Changes.

\- \[ ] Tidak ada perubahan filesystem sebelum persetujuan.

\- \[ ] Review Plan menampilkan seluruh plan.

\- \[ ] Organization Rules mendukung pengelolaan rule.

\- \[ ] Approved Rules dibatasi pada scope yang disetujui.

\- \[ ] History mencatat aktivitas analisis dan eksekusi.

\- \[ ] Semua perubahan dijalankan melalui Transaction Manager.

\- \[ ] Validasi path dan collision dilakukan sebelum eksekusi.

\- \[ ] Error dan rollback ditangani.



\## 18. Design Reference



Gunakan `image-1` sebagai referensi visual halaman Organization.



Ketentuan:

\- Pertahankan sidebar dan visual language dari Dashboard, Files, dan Storage Analyzer.

\- Gunakan navy untuk sidebar.

\- Gunakan biru sebagai warna aksen utama.

\- Gunakan panel kiri untuk konfigurasi.

\- Gunakan panel kanan untuk hasil analisis.

\- Current Structure dan Proposed Structure harus mudah dibandingkan.

\- Change Plan harus terlihat jelas di bawah struktur.

\- Jangan menjadikan AI chatbot sebagai fokus utama.

\- Hindari gradient AI dan dekorasi yang tidak memiliki fungsi.



Jika terdapat perbedaan antara gambar dan spesifikasi perilaku, README ini menjadi acuan utama implementasi.

