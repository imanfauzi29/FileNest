# Files Manager — Implementation Specification

## 1. Overview

Files Manager merupakan antarmuka penjelajah berkas (Files Explorer) desktop utama untuk mengelola, menelusuri, memeriksa metadata, dan memanipulasi berkas serta direktori yang berada di dalam **Managed Folders** yang telah didaftarkan pengguna.

Tujuan halaman:
- Memberikan pengalaman penjelajahan berkas desktop native yang responsif dan aman.
- Menampilkan struktur hierarki folder yang terdaftar dan subfoldernya.
- Menyediakan mode tampilan ganda: **List View** dan **Grid View** dengan kontrol zoom thumbnail.
- Menampilkan rincian detail berkas (metadata lengkap, tipe MIME, hash, izin, dan kapabilitas).
- Memberikan pratinjau langsung yang terisolasi dan aman untuk gambar dan cuplikan teks/kode (*bounded preview*).
- Menyediakan kontrol mutasi filesystem standar (*New Folder*, *Rename*, *Move*, *Copy*, *Delete*) yang sepenuhnya divalidasi dan dicatat melalui Transaction Manager.

Referensi desain: `image-1.png` dan `screens.png`.

> [!IMPORTANT]
> **Filesystem Safety & Confinement Constraints:**
> 1. Hanya folder yang telah didaftarkan secara manual sebagai **Managed Folder** yang boleh ditelusuri atau dimanipulasi.
> 2. Semua operasi berkas wajib melewati validasi batas canonical path backend (`PathValidator.resolve_and_verify_scope`).
> 3. Path traversal (`../`), NTFS Alternate Data Streams (`:`), symlink escape, dan Windows DOS reserved names (`CON`, `PRN`, `AUX`, `NUL`, `COM1-9`, `LPT1-9`) diblokir keras.
> 4. Seluruh mutasi filesystem (membuat folder, rename, move, copy, delete) tidak boleh dieksekusi langsung oleh frontend tanpa melalui **Transaction Manager** backend.
> 5. Penghapusan berkas tidak pernah bersifat permanen langsung; selalu dialihkan ke Windows Recycle Bin atau sistem karantina `.trash` dengan log audit yang dapat di-rollback.

---

## 2. Layout Arsitektur (3-Pane Workspace)

Files Manager dirancang menggunakan arsitektur antarmuka desktop **3-Pane Layout** terintegrasi penuh:

```
+-------------------------------------------------------------------------------------------------------+
| Top Breadcrumb & Navigation Bar                                                      [Search / Filter] |
+------------------+-----------------------------------------------------------------+------------------+
|                  | Action Toolbar: [+ Folder] [Upload] [Rename] [Move] [Copy] [Del] |                  |
| Left Pane        +-----------------------------------------------------------------+ Right Pane       |
| (240px)          |                                                                 | (320px)          |
|                  | Center Pane (Explorer Canvas)                                   |                  |
| Managed Folders  | - List View (Tabel detail berkas, ukuran, tanggal modifikasi)   | Persistent       |
| Subfolder Tree   |   atau                                                          | File/Folder      |
|                  | - Grid View (Card thumbnail dengan icon/preview berkas)         | Details Panel    |
| [+ Add Folder]   |                                                                 |                  |
|                  |                                                                 | [Quick Actions]  |
+------------------+-----------------------------------------------------------------+------------------+
| Bottom Status Bar: [1 item dipilih (2,8 KB)] [8 item | 231,5 MB]        [List | Grid] [Zoom Slider]   |
+-------------------------------------------------------------------------------------------------------+
```

1. **Left Pane (240px — Managed Folders & Directory Tree)**:
   - Menampilkan daftar Managed Folder aktif.
   - Pohon direktori (subfolder tree) yang dapat di-expand/collapse secara interaktif.
   - Tombol `+ Add Folder` untuk mendaftarkan folder baru melalui dialog native folder picker Windows.
   - Indikator status folder (aktif, dipantau, jumlah berkas).

2. **Center Pane (Main Explorer Canvas)**:
   - **Breadcrumbs Address Bar**: Menampilkan rantai path navigasi (*e.g.* `Projects > Web App > src > components`). Tiap segmen dapat diklik untuk melompat langsung ke folder induk.
   - **Filter & Search Bar**: Input pencarian real-time dengan tombol clear dan shortcut `Ctrl + K`.
   - **Action Toolbar**:
     - `+ New Folder`: Membuat folder baru di direktori aktif.
     - `Upload`: Menambahkan berkas ke direktori aktif.
     - `Rename` (`F2`): Mengubah nama item terpilih.
     - `Move`: Memindahkan item ke subfolder lain dalam managed folder.
     - `Copy`: Menyalin item ke lokasi tujuan.
     - `Delete` (`Delete`): Memindahkan item ke Recycle Bin / karantina `.trash`.
     - `Refresh`: Menyinkronkan ulang data dari filesystem lokal.
   - **Content Canvas**:
     - **List View**: Tabel responsif dengan kolom Checkbox, Name, Size, Modified Date, Type, dan Actions menu.
     - **Grid View**: Grid kartu berkas/folder responsif dengan thumbnail icon dan label nama truncate.

3. **Right Pane (320px — Persistent Details Inspector)**:
   - Menampilkan detail lengkap item yang sedang dipilih (Single Selection) atau ringkasan multiseleksi.
   - Ikon berkas/folder besar dengan kategori warna visual.
   - Nama berkas lengkap beserta ekstensi.
   - Tipe format dan MIME type resmi.
   - Ukuran presisi dalam format manusiawi dan hitungan eksak byte (*e.g.* `2.84 MB (2,981,888 bytes)`).
   - Waktu pembuatan berkas, waktu modifikasi terakhir, dan waktu akses terakhir.
   - Status verifikasi keamanan dan izin filesystem.
   - **Quick Actions Panel**:
     - *Open* (Pratinjau modal atau aplikasi default).
     - *Open in Explorer* (Membuka file di Windows File Explorer).
     - *Rename* (Memicu modal/input pengubahan nama).
     - *Copy Full Path* (Menyalin path absolut ke clipboard).
     - *Scan Folder Size* (Memicu kalkulasi rekursif ukuran folder).

4. **Bottom Status Bar**:
   - Menampilkan status seleksi aktif: `N item dipilih (X KB/MB)`.
   - Total item dan total ukuran direktori aktif saat ini: `Total: M item | X GB`.
   - Tombol toggle mode tampilan: `List View` vs `Grid View`.
   - Slider zoom responsif (50% hingga 150%) untuk mengatur ukuran kartu/thumbnail pada mode Grid View.

---

## 3. Komponen Spesifik & Interaksi

### 3.1. Subfolder Navigation Tree (Left Pane)
- Menampilkan folder akar (*Root Managed Folders*) dan anak-anak foldernya.
- Menggunakan ikon `Folder`, `FolderOpen`, `ChevronRight`, dan `ChevronDown` dari Lucide React.
- Mengklik tanda panah melakukan expand/collapse subfolder tanpa mengubah direktori aktif jika diinginkan, sedangkan mengklik nama folder langsung mengarahkan tampilan Center Explorer ke direktori tersebut.
- Folder yang sedang aktif diberikan aksen highlight `bg-primary/10 text-primary font-medium`.

### 3.2. Address Breadcrumbs
- Terletak di atas explorer canvas.
- Memiliki tombol navigasi `Back` (folder induk `..`) dan `Refresh`.
- Format: `[Folder Root Name] / [Subfolder 1] / [Subfolder 2]`.
- Klik pada segmen mana pun mengarahkan navigasi langsung ke path tersebut.

### 3.3. Mode Tampilan (List & Grid)
- **List View**:
  - Kolom dapat disortir berdasarkan Nama, Ukuran, atau Waktu Modifikasi.
  - Mendukung seleksi baris tunggal maupun ganda (*multi-select* via checkbox atau Shift/Ctrl + Click).
  - Double click pada baris folder membuka folder tersebut; double click pada baris berkas membuka modal preview.
- **Grid View**:
  - Kartu thumbnail dengan preview visual langsung untuk berkas gambar.
  - Untuk berkas non-gambar, menampilkan representasi ikon kategori (`image`, `document`, `code`, `archive`, `audio`, `video`, `database`, `other`).
  - Ukuran grid card dikontrol oleh zoom slider di Status Bar (default 100px).

### 3.4. Bounded File Preview Modal
- Terbuka ketika pengguna menekan tombol *Preview* / *Open*, menekan `Enter`, atau double-click pada berkas.
- **Preview Gambar**:
  - Men-stream gambar dari backend endpoint `GET /api/v1/fs/preview` dengan token otentikasi lokal aman (`X-App-Token`).
  - Fitur kontrol zoom: Zoom In (+25%), Zoom Out (-25%), dan Reset Zoom (100%).
  - Header keamanan: `X-Content-Type-Options: nosniff`, `Cache-Control: private, max-age=3600`, dan CSP ketat untuk berkas SVG.
- **Preview Teks & Kode**:
  - Membaca cuplikan teks melalui `GET /api/v1/fs/preview/text` dengan batasan aman maksimal 256KB.
  - Mendeteksi berkas biner (null byte) dan menolak menampilkan teks biner guna mencegah freeze/gangguan memori.
  - Menampilkan nomor baris, total baris berkas, indikator truncasi, serta tombol *Copy Content* ke clipboard.
- **Informasi Metadata**: Menampilkan nama berkas, ukuran, ekstensi, MIME type, dan path relatif.

---

## 4. Shortcut Keyboard Desktop

Untuk memberikan pengalaman desktop native Windows yang cepat dan efisien:
- `F2`: Mengubah nama (Rename) item yang sedang dipilih.
- `Delete` / `Backspace`: Menghapus item terpilih (memindahkan ke Recycle Bin / karantina `.trash`).
- `Enter`: Membuka folder yang dipilih atau membuka Preview Modal jika berkas.
- `Escape`: Menutup modal pratinjau atau membatalkan seleksi berkas.
- `Ctrl + A`: Memilih seluruh berkas dan folder di direktori aktif.
- `Ctrl + K`: Memfokuskan kursor ke input pencarian berkas.
- `Ctrl + Shift + N`: Membuat folder baru (*New Folder*).

---

## 5. Integrasi Backend & Endpoint REST

Files Manager berinteraksi secara eksklusif dengan backend melalui endpoint berikut:

| Endpoint | Method | Fungsi |
|---|---|---|
| `/api/v1/folders/` | GET | Mengambil seluruh Managed Folders yang terdaftar |
| `/api/v1/fs/browse` | GET | Membaca daftar berkas dan subfolder dalam direktori |
| `/api/v1/fs/metadata` | GET | Mengambil metadata presisi suatu berkas/folder |
| `/api/v1/fs/preview` | GET | Men-stream binary/gambar preview secara aman |
| `/api/v1/fs/preview/text` | GET | Mengambil cuplikan isi teks/kode dengan limit byte |
| `/api/v1/transactions/quick/create-folder` | POST | Membuat folder baru melalui Transaction Manager |
| `/api/v1/transactions/quick/rename` | POST | Mengubah nama berkas/folder dengan proteksi collision |
| `/api/v1/transactions/quick/move` | POST | Memindahkan berkas/folder ke target tujuan |
| `/api/v1/transactions/quick/copy` | POST | Menyalin berkas/folder |
| `/api/v1/transactions/quick/delete` | POST | Memindahkan berkas ke karantina / recycle bin |

Setiap permintaan wajib menyertakan header `X-App-Token` untuk otentikasi session desktop lokal.
