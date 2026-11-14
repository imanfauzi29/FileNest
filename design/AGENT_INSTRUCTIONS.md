# AI Agent Instructions — Desktop & Storage Manager

## 1. Project Overview

Project ini adalah aplikasi Windows Desktop untuk mengelola, menganalisis, memantau, dan mengorganisasi file serta folder menggunakan AI.

Aplikasi menggunakan:

- Tauri 2
- React
- TypeScript
- Vite
- Tailwind CSS
- shadcn/ui
- Lucide Icons
- Python
- FastAPI
- SQLite
- SQLAlchemy
- Hermes
- 9Router
- MCP

AI digunakan untuk membantu analisis dan memberikan rekomendasi. Eksekusi perubahan filesystem dilakukan oleh backend melalui Transaction Manager.

## 2. Main Responsibilities

AI Agent bertanggung jawab untuk:

1. Membaca instruksi project.
2. Membaca spesifikasi fitur sebelum implementasi.
3. Memahami referensi visual.
4. Mengimplementasikan UI sesuai desain.
5. Mengimplementasikan interaksi setiap komponen.
6. Menghubungkan UI dengan backend API.
7. Menjaga konsistensi antarfitur.
8. Menjalankan pengujian.
9. Melaporkan hasil implementasi.

Jangan langsung melakukan coding sebelum memahami spesifikasi fitur yang sedang dikerjakan.

## 3. Design Reference Structure

Seluruh referensi desain dan spesifikasi fitur berada di folder `design/`.

Struktur:

```text
design/
├── AGENT_INSTRUCTIONS.md
│
├── dashboard/
│   ├── image-1.jpg
│   └── README.md
│
├── files/
│   ├── image-1.jpg
│   └── README.md
│
├── storage/
│   ├── image-1.jpg
│   └── README.md
│
├── organization/
│   ├── image-1.jpg
│   └── README.md
│
├── smart-rename/
│   ├── image-1.jpg
│   └── README.md
│
├── review-changes/
│   ├── image-1.jpg
│   └── README.md
│
├── monitoring/
│   ├── image-1.jpg
│   └── README.md
│
├── history/
│   ├── image-1.jpg
│   └── README.md
│
└── settings/
    ├── image-1.jpg
    └── README.md
```

Setiap folder merupakan spesifikasi implementasi fitur.

### Rules

- Selalu baca `README.md` sebelum mengerjakan fitur.
- Periksa seluruh gambar referensi yang tersedia.
- README merupakan sumber utama requirement fitur.
- Gambar merupakan referensi visual untuk layout, warna, ukuran, dan posisi komponen.
- Jangan menebak fungsi tombol atau komponen yang belum dijelaskan.
- Jika terdapat ketidaksesuaian antara gambar dan README, ikuti README.
- Jika requirement saling bertentangan atau tidak lengkap, identifikasi masalah sebelum mengambil keputusan yang berdampak besar.

## 4. Design Principles

Aplikasi harus terlihat seperti software desktop profesional, bukan aplikasi chatbot atau aplikasi AI generik.

### Visual Direction

- Modern Windows Desktop Application.
- Clean and minimal interface.
- Light theme sebagai default.
- Dark theme sebagai opsi.
- Sidebar navigation.
- Konsisten menggunakan spacing.
- Typography yang mudah dibaca.
- Komponen memiliki ukuran dan alignment konsisten.
- Gunakan warna netral dengan aksen biru.
- Gunakan border dan shadow secara seperlunya.

### Avoid

- Gradient ungu khas aplikasi AI.
- Robot atau mascot AI.
- Chatbot sebagai tampilan utama.
- Animasi dekoratif berlebihan.
- Terlalu banyak kartu statistik.
- Elemen dekoratif yang tidak memiliki fungsi.
- Tombol yang tidak memiliki aksi.
- Informasi dummy pada implementasi final.

### UI Behavior

Semua elemen interaktif harus memiliki fungsi nyata.

Contoh:

- Button harus menjalankan aksi.
- Checkbox harus mengubah status pilihan.
- Toggle harus mengubah konfigurasi.
- Dropdown harus menampilkan pilihan.
- Context menu harus menyediakan tindakan.
- Search harus melakukan pencarian.
- Table row harus dapat membuka detail jika ditentukan spesifikasi.
- Modal harus memiliki mekanisme konfirmasi dan pembatalan.

Jangan membuat komponen interaktif yang hanya berfungsi sebagai dekorasi.

## 5. Component Reusability

Gunakan komponen bersama untuk elemen yang digunakan berulang.

Contoh:

```text
src/
├── components/
│   ├── ui/
│   ├── layout/
│   ├── navigation/
│   ├── data-display/
│   ├── feedback/
│   ├── dialogs/
│   └── common/
│
├── features/
│   ├── dashboard/
│   ├── files/
│   ├── storage/
│   ├── organization/
│   ├── smart-rename/
│   ├── review-changes/
│   ├── monitoring/
│   ├── history/
│   └── settings/
│
├── hooks/
├── services/
├── types/
└── utils/
```

Contoh komponen bersama:

- AppSidebar
- PageHeader
- Breadcrumb
- DataTable
- SearchInput
- FilterDropdown
- ContextMenu
- ConfirmDialog
- EmptyState
- LoadingState
- ErrorState
- StatusBadge
- ProgressBar
- FileIcon
- FolderIcon

Jangan membuat komponen baru jika komponen bersama yang sudah tersedia dapat digunakan.

Jangan menduplikasi implementasi komponen yang sama di setiap fitur.

## 6. Feature Implementation Workflow

Setiap pengerjaan fitur wajib mengikuti tahapan berikut.

### Step 1 — Read Specification

Baca:

- README.md fitur.
- Gambar referensi.
- Instruksi global.
- Komponen bersama yang sudah tersedia.
- API dan tipe data yang berkaitan.

### Step 2 — Analyze Existing Project

Periksa:

- Struktur project.
- Routing.
- Design system.
- Komponen yang sudah tersedia.
- API service.
- Database schema jika relevan.
- Fitur lain yang memiliki dependensi.

Jangan membuat ulang sesuatu yang sudah tersedia.

### Step 3 — Implementation Plan

Sebelum coding, identifikasi:

- Komponen yang diperlukan.
- Halaman dan layout.
- Interaksi pengguna.
- API yang dibutuhkan.
- Data yang diperlukan.
- Loading, empty, dan error states.
- Dependensi terhadap fitur lain.

Untuk pekerjaan kecil, analisis ini tidak perlu menghasilkan dokumen tambahan. Cukup lakukan secara internal.

### Step 4 — Implementation

Implementasikan sesuai spesifikasi.

Prioritaskan:

1. Struktur layout.
2. Kesesuaian visual.
3. Komponen UI.
4. Interaksi.
5. Integrasi API.
6. Error handling.
7. Pengujian.

### Step 5 — Validation

Periksa:

- Visual sesuai referensi.
- Semua tombol berfungsi.
- Tidak ada komponen yang tidak memiliki aksi.
- Data ditampilkan dengan benar.
- Loading dan error state berfungsi.
- Tidak ada error TypeScript.
- Tidak ada error runtime.
- Tidak merusak fitur lain.

### Step 6 — Report

Setelah selesai, laporkan:

- File yang dibuat.
- File yang diubah.
- Fitur yang selesai.
- Interaksi yang sudah berfungsi.
- API yang digunakan.
- Pengujian yang dilakukan.
- Kendala yang belum diselesaikan.

## 7. Backend & Frontend Separation

Frontend bertanggung jawab untuk:

- Menampilkan UI.
- Mengelola state tampilan.
- Menangani interaksi pengguna.
- Memanggil backend API.
- Menampilkan hasil proses.

Backend bertanggung jawab untuk:

- Business logic.
- Filesystem access.
- File scanning.
- File monitoring.
- Database operations.
- AI orchestration.
- Rule execution.
- Transaction management.
- Audit logging.

### Important

- Jangan mengakses filesystem secara langsung dari React.
- Jangan menjalankan operasi file melalui browser API.
- Jangan menyimpan business logic di komponen UI.
- Jangan menyimpan API key dalam frontend.
- Semua operasi filesystem harus melalui backend yang tervalidasi.

## 8. AI Integration Rules

Integrasi AI hanya menggunakan:

- Hermes sebagai agent runtime dan orchestrator.
- 9Router sebagai model gateway.
- MCP sebagai penghubung tool.

AI digunakan untuk:

- Menganalisis struktur folder.
- Mengelompokkan file.
- Memberikan rekomendasi struktur.
- Memberikan rekomendasi nama file.
- Mengidentifikasi kemungkinan duplikat.
- Membantu membuat organization rules.

### AI Restrictions

AI tidak boleh:

- Mengakses filesystem tanpa pembatasan.
- Menjalankan shell command secara bebas.
- Menghapus file secara langsung.
- Memindahkan file tanpa Transaction Manager.
- Mengganti nama file tanpa validasi backend.
- Mengakses folder di luar Managed Folders.

AI hanya boleh menghasilkan rekomendasi atau structured change plan.

Semua output AI harus divalidasi menggunakan schema sebelum digunakan oleh backend.

## 9. Filesystem Safety

Aplikasi hanya boleh mengelola folder yang didaftarkan secara manual oleh pengguna.

Setiap operasi harus memvalidasi:

- Root folder terdaftar.
- Path berada di dalam root yang diizinkan.
- Source file tersedia.
- Destination valid.
- Tidak terdapat konflik nama.
- File tidak berubah sejak rencana dibuat.
- Operasi tidak menyentuh protected paths.

Jangan mengikuti symbolic links atau Windows junctions secara default.

Jangan melakukan permanent deletion otomatis.

Operasi berisiko harus membutuhkan persetujuan pengguna.

## 10. Transaction Manager

Semua perubahan filesystem harus melalui Transaction Manager.

Alur:

```text
User Request
     |
     v
AI Recommendation
     |
     v
Structured Change Plan
     |
     v
Backend Validation
     |
     v
Approval Check
     |
     v
Transaction Manager
     |
     v
Filesystem Executor
     |
     v
Verification
     |
     v
Audit Log
```

### Approval Rules

Terdapat dua jenis persetujuan:

**Manual Approval**

Pengguna menyetujui setiap change plan sebelum eksekusi.

**Approved Rules**

Pengguna menyetujui aturan tertentu sebelumnya. Aturan tersebut dapat dieksekusi otomatis selama:

- Masih aktif.
- Masih berada dalam cakupan folder yang diizinkan.
- Operasinya sesuai dengan izin aturan.
- Tidak terdapat konflik atau kondisi berisiko.

Jika ditemukan kondisi yang tidak sesuai, hentikan operasi terkait dan masukkan ke Review Changes.

## 11. Monitoring & Background Jobs

Monitoring menggunakan Watchdog.

Semua pekerjaan background dikelola backend.

Ketentuan:

- Gunakan persistent task state.
- Hindari duplikasi event.
- Gunakan debounce untuk event filesystem.
- Simpan status pekerjaan di database.
- Tangani kegagalan pekerjaan.
- Pekerjaan yang terputus harus dapat dipulihkan jika memungkinkan.
- Jangan menjalankan analisis AI untuk setiap event tanpa aturan yang sesuai.

## 12. Database Rules

Gunakan SQLite sebagai database lokal.

SQLAlchemy digunakan sebagai ORM dan Alembic untuk migrasi.

Ketentuan:

- Jangan membuat tabel duplikat.
- Periksa model yang sudah tersedia.
- Gunakan migration untuk perubahan schema.
- Hindari hardcoded database values.
- Gunakan transaction database ketika diperlukan.
- Simpan status pekerjaan dan audit log secara persisten.
- Jangan menyimpan API key dalam plaintext database.

## 13. API Integration

Semua komunikasi frontend-backend harus menggunakan service layer.

Ketentuan:

- Pisahkan API service berdasarkan domain.
- Gunakan TypeScript types untuk request dan response.
- Tangani HTTP errors.
- Gunakan loading dan error states.
- Hindari pemanggilan API langsung dari banyak komponen.
- Jangan mengarang endpoint jika backend contract belum tersedia.
- Jika endpoint belum tersedia, tandai sebagai dependency dan jangan berpura-pura integrasi sudah selesai.

## 14. Coding Standards

### TypeScript / React

- Gunakan TypeScript strict mode.
- Hindari penggunaan `any`.
- Gunakan functional components.
- Pisahkan komponen berdasarkan tanggung jawab.
- Gunakan custom hooks untuk logic yang dapat digunakan ulang.
- Jangan membuat satu komponen terlalu besar.
- Hindari duplikasi kode.

### Python

- Gunakan type hints.
- Pisahkan router, service, repository, dan model.
- Validasi request menggunakan schema.
- Tangani exception secara terstruktur.
- Gunakan logging.
- Hindari business logic di API router.

### Naming

- React components: PascalCase.
- Functions and variables: camelCase pada TypeScript.
- Python functions and variables: snake_case.
- Database tables: snake_case.
- Constants: UPPER_SNAKE_CASE.

## 15. Dependency Rules

Sebelum menambahkan package baru:

1. Periksa apakah package sejenis sudah tersedia.
2. Periksa apakah fungsi dapat dilakukan menggunakan package yang ada.
3. Pastikan package kompatibel dengan stack.
4. Jangan menambahkan dependency hanya untuk kebutuhan kecil.
5. Jelaskan alasan jika dependency baru memang diperlukan.

Jangan mengganti framework atau library utama tanpa persetujuan.

## 16. Scope Control

Ketika mengerjakan satu fitur:

- Fokus pada folder fitur tersebut.
- Ubah shared component hanya jika diperlukan.
- Jangan mengubah fitur lain tanpa alasan teknis.
- Jangan menghapus kode yang tidak berkaitan.
- Jangan melakukan refactor besar tanpa persetujuan.
- Jangan mengubah database schema tanpa kebutuhan yang jelas.
- Jangan menambahkan fitur di luar requirement.

Jika perubahan memengaruhi fitur lain, identifikasi dampaknya dan jelaskan sebelum melakukan perubahan besar.

## 17. Mock Data Policy

Mock data hanya boleh digunakan ketika backend belum tersedia atau ketika mengembangkan UI secara terpisah.

Ketentuan:

- Pisahkan mock data dari API service.
- Beri penanda yang jelas bahwa data adalah mock.
- Jangan mencampurkan mock dan real data secara tidak terkontrol.
- Jangan menganggap mock integration sebagai integrasi backend yang selesai.
- Hapus atau nonaktifkan mock mode pada production build.

## 18. Testing Requirements

Setiap fitur harus diuji sesuai fungsinya.

Frontend:

- Component rendering.
- User interactions.
- Navigation.
- Form validation.
- Loading and error states.

Backend:

- API validation.
- Business logic.
- Database operations.
- Filesystem restrictions.
- Error handling.

Integration:

- Frontend-backend communication.
- Task status updates.
- Transaction lifecycle.
- Monitoring event handling.

Jangan menyatakan pengujian berhasil jika belum benar-benar dijalankan.

## 19. Definition of Done

Sebuah fitur dianggap selesai jika:

- [ ] README sudah diikuti.
- [ ] Referensi visual sudah diterapkan.
- [ ] Layout sesuai spesifikasi.
- [ ] Semua action berfungsi.
- [ ] Data berasal dari sumber yang benar.
- [ ] API terintegrasi jika tersedia.
- [ ] Loading, empty, dan error states tersedia.
- [ ] Tidak terdapat error TypeScript atau runtime yang diketahui.
- [ ] Pengujian relevan sudah dilakukan.
- [ ] Tidak merusak fitur lain.
- [ ] Acceptance criteria fitur terpenuhi.
- [ ] Hasil implementasi sudah dilaporkan.

## 20. Final Instructions

Sebelum mulai mengerjakan fitur apa pun:

1. Baca instruksi global ini.
2. Baca README fitur yang diminta.
3. Periksa gambar referensi fitur.
4. Periksa struktur project yang sudah ada.
5. Ikuti arsitektur dan design system.
6. Implementasikan hanya sesuai scope.
7. Uji hasil implementasi.
8. Laporkan hasil pekerjaan.

Jangan berasumsi bahwa semua fitur harus dibuat sekaligus.

Jangan mengarang requirement yang tidak tercantum.

Jangan mengubah keputusan arsitektur tanpa persetujuan.

Jika ada requirement yang tidak jelas, identifikasi bagian yang ambigu dan tanyakan hanya jika keputusan tersebut benar-benar menghambat implementasi.

**Prioritas utama: implementasi harus sesuai spesifikasi, konsisten secara visual, aman terhadap filesystem, dan mudah dikembangkan.**