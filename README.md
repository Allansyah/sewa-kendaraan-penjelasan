# sewa-kendaraan-penjelasan



# 🚛 MiningCo Fleet

**Sistem Manajemen Reservasi Kendaraan untuk Perusahaan Pertambangan**

[![Next.js](https://img.shields.io/badge/Next.js-16-black?logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Prisma](https://img.shields.io/badge/Prisma-6-2D3748?logo=prisma)](https://www.prisma.io/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-4-06B6D4?logo=tailwindcss)](https://tailwindcss.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

</div>

---

## 📑 Daftar Isi

- [Deskripsi Proyek](#-deskripsi-proyek)
- [Masalah Bisnis](#-masalah-bisnis)
- [Fitur Aplikasi](#-fitur-aplikasi)
- [Peran Pengguna](#-peran-pengguna)
- [Alur Kerja (Workflow)](#-alur-kerja-workflow)
- [Dashboard](#-dashboard)
- [Aturan Bisnis](#-aturan-bisnis)
- [Tech Stack](#-tech-stack)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Desain Database](#-desain-database)
- [Struktur Folder](#-struktur-folder)
- [Instalasi](#-instalasi)
- [Environment Variables](#-environment-variables)
- [Akun Demo](#-akun-demo)
- [Keamanan](#-keamanan)
- [Dukungan Bahasa](#-dukungan-bahasa)
- [Screenshot](#-screenshot)
- [Deployment](#-deployment)
- [Status Proyek](#-status-proyek)
- [Lisensi](#-lisensi)

---

## 📋 Deskripsi Proyek

**MiningCo Fleet** adalah aplikasi web manajemen reservasi kendaraan yang dirancang khusus untuk perusahaan pertambangan. Sistem ini menyediakan platform terintegrasi untuk mengelola armada kendaraan, mengatur jadwal driver, memproses pemesanan kendaraan dengan alur persetujuan bertingkat, serta menghasilkan laporan operasional secara komprehensif.

Aplikasi ini dikembangkan sebagai proyek **technical test magang fullstack developer** dengan menerapkan standar kualitas profesional, arsitektur yang terstruktur, dan fitur enterprise-grade.

### 🎯 Mengapa Perusahaan Pertambangan Membutuhkan Sistem Ini?

Di lingkungan operasional pertambangan, kendaraan merupakan aset kritis yang mendukung mobilitas tenaga kerja dan logistik. Tanpa sistem reservasi yang terstruktur, perusahaan menghadapi berbagai masalah:

| Masalah | Dampak |
|---------|--------|
| Pemesanan manual via WhatsApp/telepon | Jadwal bentrok, kendaraan double-booked |
| Tidak ada persetujuan bertingkat | Kendaraan dipakai tanpa otorisasi yang cukup |
| Tidak ada pelacakan penggunaan | Sulit mengaudit penggunaan armada |
| Status kendaraan tidak terpusat | Kendaraan rusak tetap dijadwalkan |
| Driver tanpa penugasan jelas | Efisiensi kerja menurun |

MiningCo Fleet menyelesaikan masalah-masalah tersebut dengan menyediakan **sistem terpusat** yang mengotomatisasi alur reservasi, persetujuan, dan pelaporan.

---

## 🏢 Masalah Bisnis

### Sebelum MiningCo Fleet

```
❌ Pemesanan kendaraan melalui pesan teks / telepon
❌ Jadwal bentrok karena tidak ada pengecekan ketersediaan
❌ Persetujuan hanya satu level atau bahkan tidak ada
❌ Tidak ada riwayat penggunaan kendaraan
❌ Laporan harus dibuat manual di Excel
❌ Sulit melacak siapa yang menyetujui pemesanan
```

### Setelah MiningCo Fleet

```
✅ Pemesanan kendaraan melalui sistem terpusat
✅ Validasi otomatis mencegah double booking
✅ Persetujuan bertingkat (Level 1 → Level 2)
✅ Riwayat aktivitas tercatat secara otomatis
✅ Laporan dapat di-generate dan diekspor ke Excel
✅ Audit trail lengkap untuk setiap persetujuan
```

---

## ✨ Fitur Aplikasi

### 1. 📊 Dashboard Operasional

Dashboard menyajikan ringkasan data armada secara real-time, membantu pengambilan keputusan cepat berdasarkan kondisi operasional terkini.

**Untuk Admin:**
- Statistik total kendaraan, driver, dan pemesanan
- Grafik penggunaan pemesanan bulanan (Bar Chart)
- Distribusi status pemesanan (Pie Chart)
- Peringkat kendaraan paling sering digunakan
- Daftar pemesanan terbaru dan mendatang
- Ringkasan ketersediaan kendaraan (Tersedia / Digunakan / Perawatan)

**Untuk Approver:**
- Jumlah pemesanan yang menunggu persetujuan
- Statistik keputusan yang telah dibuat (disetujui / ditolak)
- Riwayat persetujuan terkini
- Daftar permintaan yang membutuhkan tindakan segera

### 2. 🚗 Manajemen Kendaraan

Modul ini memungkinkan administrator mengelola seluruh armada kendaraan perusahaan, termasuk kendaraan milik perusahaan maupun sewa. Setiap kendaraan memiliki kode unik, nomor plat, tipe (Penumpang/Barang), status kepemilikan (Perusahaan/Sewa), serta informasi wilayah dan kantor cabang.

**Fitur utama:**
- Tambah, edit, dan hapus kendaraan (soft delete)
- Pencarian berdasarkan nama, kode, atau plat nomor
- Filter berdasarkan status (Tersedia / Digunakan / Perawatan) dan tipe
- Pagination untuk data besar
- Validasi kode kendaraan unik — sistem menolak kode yang sudah terdaftar

### 3. 👨‍✈️ Manajemen Driver

Modul ini mengelola informasi lengkap setiap driver, termasuk status ketersediaan untuk memastikan hanya driver aktif yang dapat ditugaskan pada pemesanan.

**Fitur utama:**
- Tambah, edit, dan hapus data driver
- Pencarian berdasarkan nama atau nomor SIM
- Filter berdasarkan status (Aktif / Tidak Aktif)
- Pagination untuk data besar
- Validasi nomor SIM unik — sistem menolak nomor SIM yang sudah terdaftar

### 4. 📋 Sistem Reservasi Kendaraan

Ini adalah modul inti yang menghubungkan kendaraan, driver, dan alur persetujuan. Setiap pemesanan menghasilkan kode unik otomatis (format: `RSV-YYYY-NNN`) dan melalui validasi ketat sebelum masuk ke alur persetujuan.

**Fitur utama:**
- Buat pemesanan baru dengan pemilihan kendaraan dan driver
- Validasi otomatis: cek ketersediaan kendaraan dan driver pada tanggal yang dipilih
- Pencegahan **double booking** — sistem menolak jika kendaraan/driver sudah dipesan pada tanggal yang sama
- Edit pemesanan saat masih berstatus menunggu persetujuan
- Batalkan pemesanan dengan alasan pembatalan (sebelum disetujui)
- Mulai perjalanan (status → In Progress) dan selesaikan perjalanan (status → Completed)
- Timeline riwayat persetujuan pada detail pemesanan

**Status Pemesanan:**

| Status | Penjelasan |
|--------|------------|
| `DRAFT` | Pemesanan baru dibuat, belum diajukan |
| `PENDING_L1` | Menunggu persetujuan Level 1 |
| `PENDING_L2` | Disetujui L1, menunggu persetujuan Level 2 |
| `APPROVED` | Disetujui kedua level, siap digunakan |
| `IN_PROGRESS` | Perjalanan sedang berlangsung |
| `COMPLETED` | Perjalanan telah selesai |
| `REJECTED` | Ditolak oleh approver (alur berhenti) |
| `CANCELLED` | Dibatalkan oleh admin (dengan alasan) |

### 5. ✅ Persetujuan Bertingkat (Multi-Level Approval)

Sistem persetujuan dua level memastikan setiap pemesanan kendaraan mendapat otorisasi yang cukup sebelum dieksekusi. Setiap level memiliki approver yang berbeda, sehingga tidak ada satu orang pun yang bisa menyetujui pemesanan secara sepihak.

**Mekanisme:**
- **Level 1 (Persetujuan Awal):** Approver pertama meninjau detail pemesanan dan memutuskan approve atau reject
- **Level 2 (Persetujuan Final):** Setelah L1 approve, approver kedua melakukan review akhir
- Jika **ditolak di level mana pun**, alur persetujuan berhenti — pemesanan berstatus REJECTED
- Admin **tidak dapat menyetujui** pemesanan — hanya approver yang berwenang
- Setiap keputusan disertai catatan opsional dan tercatat di audit trail

### 6. 📈 Laporan & Ekspor

Modul laporan menyediakan kemampuan filtering dan ekspor data pemesanan untuk keperluan operasional dan audit. Laporan dapat difilter berdasarkan periode, status, dan kendaraan tertentu.

**Fitur utama:**
- Filter berdasarkan tanggal mulai dan selesai
- Filter berdasarkan status pemesanan
- Filter berdasarkan kendaraan tertentu
- Ekspor hasil laporan ke file Excel (.xlsx)
- Header laporan otomatis menyesuaikan bahasa aktif (Indonesia/Inggris)

### 7. 📝 Log Aktivitas (Audit Trail)

Setiap aksi yang dilakukan di sistem tercatat secara otomatis sebagai audit trail. Ini memastikan transparansi dan akuntabilitas operasional — siapa melakukan apa, kapan, dan perubahan apa yang terjadi.

**Informasi yang dicatat:**
- Pengguna yang melakukan aksi
- Jenis aktivitas (Login, Buat, Update, Hapus, Setujui, Tolak, Batalkan)
- Modul terkait (Auth, Vehicle, Driver, Reservation, Approval)
- Alamat IP pengguna
- Waktu aktivitas
- Nilai sebelum dan sesudah perubahan (before/after)
- Filter berdasarkan modul dan pencarian teks bebas

### 8. 🌐 Dua Bahasa (i18n)

Seluruh tampilan aplikasi mendukung dua bahasa yang dapat diganti secara instan tanpa reload halaman. Bahasa aktif tersimpan otomatis di browser pengguna.

| Kode | Bahasa | Status |
|------|--------|--------|
| `id` | Bahasa Indonesia | ✅ Lengkap (440+ key) |
| `en` | English | ✅ Complete (440+ key) |

### 9. 🌙 Mode Gelap

Aplikasi mendukung tema terang dan gelap yang dapat di-toggle melalui navbar. Preferensi tema tersimpan otomatis di browser dan mengikuti preferensi sistem operasi saat pertama kali digunakan.

### 10. 📅 Kalender Pemesanan

Tampilan kalender visual yang memudahkan admin melihat jadwal penggunaan kendaraan secara periodik (bulanan/mingguan). Fitur ini membantu perencanaan armada dan mengidentifikasi potensi bentrok jadwal.

---

## 👥 Peran Pengguna

Sistem menerapkan **Role-Based Access Control (RBAC)** yang ketat. Setiap peran memiliki akses yang berbeda — tidak ada tumpang tindih fitur antara admin dan approver.

### Perbandingan Akses

| Fitur | Admin | Approver L1 | Approver L2 |
|-------|:-----:|:-----------:|:-----------:|
| Dashboard Operasional | ✅ | ❌ | ❌ |
| Dashboard Persetujuan | ❌ | ✅ | ✅ |
| Kelola Kendaraan (CRUD) | ✅ | ❌ | ❌ |
| Kelola Driver (CRUD) | ✅ | ❌ | ❌ |
| Buat Pemesanan | ✅ | ❌ | ❌ |
| Edit Pemesanan (sebelum approve) | ✅ | ❌ | ❌ |
| Batalkan Pemesanan | ✅ | ❌ | ❌ |
| Mulai / Selesaikan Perjalanan | ✅ | ❌ | ❌ |
| Persetujuan Level 1 | ❌ | ✅ | ❌ |
| Persetujuan Level 2 | ❌ | ❌ | ✅ |
| Lihat Laporan | ✅ | ❌ | ❌ |
| Ekspor Laporan | ✅ | ❌ | ❌ |
| Lihat Log Aktivitas | ✅ | ❌ | ❌ |
| Kalender Pemesanan | ✅ | ❌ | ❌ |
| Pengaturan Aplikasi | ✅ | ❌ | ❌ |
| Profil Pengguna | ✅ | ✅ | ✅ |

### Penjelasan Peran

#### 👨‍💼 Admin
Admin bertanggung jawab atas **operasional harian** armada kendaraan. Admin dapat mengelola data master (kendaraan dan driver), membuat dan mengelola pemesanan, serta mengakses laporan dan log aktivitas. Namun, admin **tidak dapat menyetujui pemesanan** — persetujuan sepenuhnya menjadi wewenang approver.

#### ✅ Approver Level 1
Approver L1 adalah **peninjau pertama** yang memvalidasi keperluan dan kelayakan pemesanan. Jika disetujui, pemesanan diteruskan ke Level 2. Jika ditolak, alur berhenti dan pemesanan berstatus REJECTED.

#### ✅ Approver Level 2
Approver L2 adalah **peninjau final** yang memberikan otorisasi terakhir. Hanya setelah persetujuan L2, pemesanan berubah menjadi APPROVED dan kendaraan dapat digunakan. Penolakan di level ini juga menghentikan alur.

### Menu Sidebar per Peran

**Admin:**
```
📊 Dashboard
🚗 Kendaraan
👨‍✈️ Driver
📋 Pemesanan
📅 Kalender
📈 Laporan
📝 Log Aktivitas
⚙️ Pengaturan
```

**Approver:**
```
📊 Dashboard Persetujuan
✅ Permintaan Persetujuan
📜 Riwayat Persetujuan
👤 Profil
```

---

## 🔄 Alur Kerja (Workflow)

### Alur Lengkap Pemesanan Kendaraan

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ALUR RESERVASI KENDARAAN                         │
└─────────────────────────────────────────────────────────────────────┘

  [1] ADMIN MEMBUAT PESANAN
       │
       │  • Pilih kendaraan & driver
       │  • Tentukan tanggal, tujuan, keperluan
       ▼
  [2] SISTEM VALIDASI
       │
       │  • Cek ketersediaan kendaraan pada tanggal tsb
       │  • Cek ketersediaan driver pada tanggal tsb
       │  • Cegah double booking
       │
       ├── Tidak valid ──→ ❌ Pemesanan ditolak, kembalikan ke form
       │
       ▼ Valid
  [3] STATUS: PENDING_L1
       │
       │  Pemesanan menunggu persetujuan Level 1
       ▼
  [4] APPROVER L1 MENINJAU
       │
       │  • Melihat detail pemesanan
       │  • Memberikan catatan (opsional)
       │
       ├── Tolak ──→ ❌ STATUS: REJECTED (alur berhenti)
       │
       ▼ Setujui
  [5] STATUS: PENDING_L2
       │
       │  Pemesanan diteruskan ke Level 2
       ▼
  [6] APPROVER L2 MENINJAU
       │
       │  • Melihat detail pemesanan + catatan L1
       │  • Memberikan catatan (opsional)
       │
       ├── Tolak ──→ ❌ STATUS: REJECTED (alur berhenti)
       │
       ▼ Setujui
  [7] STATUS: APPROVED ✅
       │
       │  Pemesanan disetujui sepenuhnya
       │  Kendaraan siap digunakan
       ▼
  [8] ADMIN MULAI PERJALANAN
       │
       ▼ STATUS: IN_PROGRESS 🚗
       │
  [9] ADMIN SELESAIKAN PERJALANAN
       │
       ▼ STATUS: COMPLETED ✔️

  ────────────── SELURUH AKSI TERCATAT DI ──────────────
  📝 Activity Log  │  📈 Laporan  │  ✅ Approval Record
```

### Alur Alternatif: Pembatalan

```
  PENDING_L1 / PENDING_L2 / APPROVED
       │
       │  Admin membatalkan dengan alasan
       ▼
  STATUS: CANCELLED 🚫
       │
       └──→ Tercatat di Activity Log + Laporan
```

### Diagram Status

```
  DRAFT ──→ PENDING_L1 ──→ PENDING_L2 ──→ APPROVED ──→ IN_PROGRESS ──→ COMPLETED
                │                │
                │ reject         │ reject
                ▼                ▼
             REJECTED         REJECTED

  (PENDING_L1 / PENDING_L2 / APPROVED) ──cancel──→ CANCELLED
```

---

## 📊 Dashboard

Sistem menyediakan **dua jenis dashboard** yang berbeda berdasarkan peran pengguna. Perbedaan ini dirancang agar setiap pengguna hanya melihat informasi yang relevan dengan tugasnya.

### Dashboard Admin

Admin membutuhkan gambaran menyeluruh tentang operasional armada. Dashboard admin menampilkan:

| Komponen | Penjelasan |
|----------|------------|
| Kartu Statistik | Total kendaraan, driver, pemesanan, yang disetujui, menunggu, ditolak |
| Grafik Bulanan | Bar chart penggunaan pemesanan per bulan (disetujui vs menunggu vs ditolak) |
| Distribusi Status | Pie chart proporsi status pemesanan |
| Kendaraan Terpopuler | Bar chart kendaraan paling sering digunakan |
| Ketersediaan Kendaraan | Ringkasan jumlah kendaraan tersedia, digunakan, dan dalam perawatan |
| Pemesanan Terbaru | Tabel 5 pemesanan terakhir |
| Pemesanan Mendatang | Daftar pemesanan yang sudah disetujui dan akan berlangsung |

### Dashboard Approver

Approver membutuhkan informasi tentang pemesanan yang menunggu keputusannya. Dashboard approver menampilkan:

| Komponen | Penjelasan |
|----------|------------|
| Menunggu Persetujuan Saya | Jumlah pemesanan yang perlu ditinjau segera |
| Disetujui Oleh Saya | Total pemesanan yang telah disetujui |
| Ditolak Oleh Saya | Total pemesanan yang telah ditolak |
| Total Diproses | Jumlah seluruh keputusan yang telah dibuat |
| Riwayat Persetujuan | Timeline keputusan persetujuan terkini |

---

## 📐 Aturan Bisnis

Berikut adalah aturan bisnis yang diterapkan dalam sistem untuk menjaga konsistensi dan keamanan data operasional:

| # | Aturan | Penjelasan |
|---|--------|------------|
| 1 | **Kendaraan tidak boleh double booking** | Sistem memvalidasi bahwa kendaraan belum dipesan orang lain pada tanggal yang sama sebelum pemesanan dibuat |
| 2 | **Driver tidak boleh ditugaskan bersamaan** | Satu driver hanya bisa ditugaskan pada satu pemesanan dalam periode waktu yang sama |
| 3 | **Approval Level 2 hanya muncul setelah Level 1 approve** | Approver L2 tidak dapat melihat atau memproses pemesanan yang belum disetujui L1 |
| 4 | **Penolakan menghentikan workflow** | Jika ditolak di level mana pun, pemesanan langsung berstatus REJECTED dan tidak dapat dilanjutkan |
| 5 | **Admin tidak dapat menyetujui pemesanan** | Persetujuan sepenuhnya menjadi wewenang approver — admin hanya membuat dan mengelola pemesanan |
| 6 | **Approver tidak dapat membuat pemesanan** | Approver hanya berwenang menyetujui atau menolak — tidak bisa CRUD kendaraan, driver, atau pemesanan |
| 7 | **Pembatalan memerlukan alasan** | Admin wajib memberikan alasan saat membatalkan pemesanan yang sudah diajukan |
| 8 | **Soft delete pada kendaraan** | Kendaraan yang dihapus tidak benar-benar hilang dari database, hanya ditandai sebagai deleted |
| 9 | **Kode pemesanan otomatis** | Setiap pemesanan mendapat kode unik (RSV-YYYY-NNN) yang di-generate sistem, tidak bisa diubah manual |
| 10 | **Hanya pemesanan menunggu yang bisa diedit** | Pemesanan yang sudah disetujui, ditolak, atau selesai tidak dapat diedit lagi |
| 11 | **Aktivitas tercatat otomatis** | Setiap aksi (buat, edit, hapus, setujui, tolak, batalkan) tercatat di Activity Log dengan informasi lengkap |

---

## 🛠️ Tech Stack

| Teknologi | Versi | Fungsi dalam Proyek |
|-----------|-------|---------------------|
| **Next.js** | 16 | Framework React dengan App Router, SSR, dan API Routes |
| **TypeScript** | 5 | Bahasa pemrograman bertipe untuk type safety dan developer experience |
| **Tailwind CSS** | 4 | Utility-first CSS framework untuk styling responsif |
| **shadcn/ui** | — | Komponen UI berbasis Radix UI, konsisten dan aksesibel |
| **Prisma ORM** | 6 | ORM untuk interaksi database SQLite dengan type-safe queries |
| **SQLite** | — | Database ringan yang cocok untuk development dan demo |
| **Zustand** | 5 | State management ringan untuk client-side state |
| **Recharts** | 2 | Library chart React untuk visualisasi data |
| **XLSX** | 0.18 | Library untuk ekspor data ke format Excel (.xlsx) |
| **bcryptjs** | 2 | Hashing kata sandi dengan algoritma bcrypt |
| **Lucide React** | — | Library ikon SVG untuk interface yang konsisten |
| **Sonner** | 2 | Toast notification yang elegan |
| **NextAuth.js** | 4 | Library autentikasi untuk Next.js |
| **date-fns** | 4 | Utility untuk manipulasi dan format tanggal |
| **Zod** | 4 | Library validasi schema untuk input data |

---

## 🏗️ Arsitektur Sistem

### Arsitektur High-Level

```
┌──────────────────────────────────────────────────────────────────┐
│                         CLIENT (Browser)                         │
│                                                                  │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────┐            │
│  │ React Components │  │  Zustand Store   │  │  i18n System   │            │
│  │ (shadcn/ui)      │  │  (Auth, Page,    │  │  (ID / EN)     │            │
│  │                   │  │   Locale, Theme) │  │                 │            │
│  └────────┬──────────┘  └────────┬─────────┘  └────────────────┘            │
│           │                      │                                         │
│           └──────────┬───────────┘                                         │
│                      │ fetch() dengan x-user-id, x-user-role headers      │
└──────────────────────┼──────────────────────────────────────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────────────────────────┐
│                      NEXT.JS API ROUTES                          │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌───────────────────┐      │
│  │  Middleware    │  │  Auth Helper  │  │  Route Handlers    │      │
│  │  (RBAC check) │─→│  (requireAuth)│─→│  (CRUD + Logic)    │      │
│  └──────────────┘  └──────────────┘  └─────────┬─────────┘      │
│                                                  │                │
└──────────────────────────────────────────────────┼────────────────┘
                                                   │
                                                   ▼
┌──────────────────────────────────────────────────────────────────┐
│                       PRISMA ORM                                 │
│                                                                  │
│  ┌─────────────────────────────────────────────────────────┐     │
│  │  Prisma Client (type-safe queries)                       │     │
│  │  Schema: User, Vehicle, Driver, Reservation, Approval,  │     │
│  │          ActivityLog                                     │     │
│  └──────────────────────────┬──────────────────────────────┘     │
│                              │                                   │
└──────────────────────────────┼───────────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────────┐
│                       DATABASE (SQLite)                          │
│                                                                  │
│  File: db/custom.db                                              │
│  Tables: users, vehicles, drivers, reservations,                 │
│          approvals, activity_logs                                │
└──────────────────────────────────────────────────────────────────┘
```

### Alur Request

```
User Action → React Component → Zustand State Update
                                → fetch() to API Route
                                  → Middleware (RBAC check)
                                    → Auth Helper (verify user)
                                      → Route Handler (business logic)
                                        → Prisma Client (query)
                                          → SQLite Database
                                        ← Prisma Result
                                      ← JSON Response
                                    ← 401/403 if unauthorized
                                  ← Data / Error
                                ← UI Update
```

### Lapisan Keamanan

```
Request masuk
     │
     ▼
[1] Next.js Middleware ─── Cek header x-user-id (auth)
     │                       Cek header x-user-role (RBAC)
     │                       Tolak jika tidak sesuai → 401/403
     ▼
[2] Auth Helper ─────────── Verifikasi user di database
     │                       Cek user.isActive
     │                       Cek role vs required role
     ▼
[3] Route Handler ──────── Validasi input (Zod / manual)
     │                       Business logic check
     │                       Double booking prevention
     ▼
[4] Prisma Query ────────── Parameterized queries (SQL injection safe)
     │
     ▼
     Database
```

---

## 🗄️ Desain Database

### Entity Relationship Diagram

```
┌──────────────┐          ┌──────────────────┐          ┌──────────────┐
│     User     │          │   Reservation    │          │   Vehicle    │
│──────────────│          │──────────────────│          │──────────────│
│ id (PK)      │────┐     │ id (PK)          │     ┌───│ id (PK)      │
│ email        │    │     │ reservationCode  │     │   │ vehicleCode  │
│ name         │    └─────│ requesterId (FK) │     │   │ plateNumber  │
│ password     │          │ vehicleId (FK)   │─────┘   │ vehicleName  │
│ role         │          │ driverId (FK)    │─────┐   │ vehicleType  │
│ approvalLevel│          │ status           │     │   │ ownership    │
│ isActive     │          │ destination      │     │   │ status       │
└──────┬───────┘          │ purpose          │     │   │ isDeleted    │
       │                  │ startDate        │     │   └──────────────┘
       │                  │ endDate          │     │
       │                  │ notes            │     │   ┌──────────────┐
       │                  │ isDeleted        │     │   │   Driver     │
       │                  └──────┬───────────┘     └───│──────────────│
       │                         │                      │ id (PK)      │
       │                         │                      │ driverName   │
       │                  ┌──────┴───────────┐          │ licenseNumber│
       │                  │   Approval       │          │ phoneNumber  │
       │                  │──────────────────│          │ status       │
       │                  │ id (PK)          │     ┌───│ isDeleted    │
       └──────────────────│ approverId (FK)  │     │   └──────────────┘
                          │ reservationId(FK)│─────┘
                          │ level            │
                          │ status           │     ┌──────────────────┐
                          │ notes            │     │  ActivityLog     │
                          └──────────────────┘     │──────────────────│
                                                   │ id (PK)          │
                                                   │ userId (FK)      │
                                                   │ activity         │
                                                   │ module           │
                                                   │ action           │
                                                   │ beforeValue      │
                                                   │ afterValue       │
                                                   │ ipAddress        │
                                                   └──────────────────┘
```

### Penjelasan Tabel

| Tabel | Fungsi Bisnis | Relasi Utama |
|-------|---------------|--------------|
| `users` | Menyimpan data pengguna dengan peran (admin/approver) dan level persetujuan. Ini adalah fondasi sistem RBAC. | Satu user bisa membuat banyak reservation, memberikan banyak approval, dan memiliki banyak activity log |
| `vehicles` | Menyimpan data armada kendaraan termasuk status ketersediaan. Mendukung soft delete agar data historis tetap utuh. | Satu vehicle bisa terhubung ke banyak reservation |
| `drivers` | Menyimpan data driver dengan status aktif/tidak aktif. Status menentukan ketersediaan driver untuk penugasan. | Satu driver bisa terhubung ke banyak reservation |
| `reservations` | Tabel inti yang menghubungkan kendaraan, driver, dan pemohon. Menyimpan seluruh informasi pemesanan termasuk status dan alasan pembatalan. | Milik satu user (requester), satu vehicle, satu driver; memiliki banyak approval dan activity log |
| `approvals` | Mencatat setiap keputusan persetujuan per level. Setiap pemesanan bisa memiliki maksimal 2 record approval (L1 dan L2). | Milik satu reservation dan satu user (approver) |
| `activity_logs` | Audit trail yang mencatat setiap aksi di sistem. Menyimpan nilai sebelum/sesudah perubahan untuk keperluan audit. | Milik satu user dan opsional terhubung ke satu reservation |

---

## 📁 Struktur Folder

```
my-project/
├── prisma/
│   ├── schema.prisma          # Skema database Prisma (6 model)
│   └── seed.ts                # Script seeding data demo (3 user, 10 kendaraan, 8 driver, 15 reservasi)
│
├── src/
│   ├── app/
│   │   ├── api/               # Backend API Routes (Next.js App Router)
│   │   │   ├── auth/          # Autentikasi
│   │   │   │   ├── [...nextauth]/route.ts    # Konfigurasi NextAuth.js
│   │   │   │   └── credentials-check/route.ts # Validasi login custom
│   │   │   ├── dashboard/route.ts            # API data dashboard (role-filtered)
│   │   │   ├── vehicles/route.ts             # CRUD kendaraan (admin only)
│   │   │   ├── drivers/route.ts              # CRUD driver (admin only)
│   │   │   ├── reservations/route.ts         # CRUD & status update pemesanan
│   │   │   ├── approvals/route.ts            # Persetujuan/penolakan (approver only)
│   │   │   ├── reports/route.ts              # Generate & ekspor laporan (admin only)
│   │   │   ├── activity-logs/route.ts        # Query audit trail (admin only)
│   │   │   └── seed/route.ts                 # Endpoint seeding database
│   │   │
│   │   ├── globals.css        # Global styles + Tailwind directives
│   │   ├── layout.tsx         # Root layout (HTML, metadata, font)
│   │   └── page.tsx           # Halaman utama SPA (client-side routing via Zustand)
│   │
│   ├── components/
│   │   └── ui/                # Komponen shadcn/ui (60+ komponen)
│   │       ├── button.tsx     # Contoh: Button dengan variant
│   │       ├── card.tsx       # Contoh: Card untuk dashboard
│   │       ├── dialog.tsx     # Contoh: Modal dialog
│   │       ├── table.tsx      # Contoh: Tabel data
│   │       ├── chart.tsx      # Komponen chart Recharts
│   │       └── ...            # Dan komponen UI lainnya
│   │
│   ├── hooks/
│   │   ├── use-theme.ts       # Hook manajemen tema (light/dark)
│   │   ├── use-mobile.ts      # Hook deteksi tampilan mobile
│   │   └── use-toast.ts       # Hook toast notification
│   │
│   ├── store/
│   │   └── useAppStore.ts     # Zustand store global (auth, page, locale, sidebar)
│   │
│   ├── lib/
│   │   ├── db.ts              # Prisma Client singleton
│   │   ├── auth.ts            # Helper autentikasi & RBAC (requireAuth, requireAdmin, requireApprover)
│   │   ├── i18n.ts            # Sistem internasionalisasi (440+ key per bahasa)
│   │   ├── types.ts           # TypeScript type definitions & RBAC constants
│   │   ├── helpers.tsx        # Helper UI (status colors, icons, API headers)
│   │   └── utils.ts           # Utility functions (cn, dll)
│   │
│   └── middleware.ts          # Next.js middleware untuk proteksi API routes (RBAC)
│
├── db/
│   └── custom.db              # File database SQLite
│
├── .env                       # Environment variables (tidak di-commit ke Git)
├── package.json               # Dependencies dan scripts
└── README.md                  # Dokumentasi proyek
```

### Penjelasan Folder

| Folder | Kegunaan |
|--------|----------|
| `prisma/` | Berisi skema database dan script seeding. Prisma menggunakan `schema.prisma` untuk mendefinisikan model dan relasi, lalu `seed.ts` untuk mengisi data awal. |
| `src/app/api/` | Backend API routes menggunakan Next.js App Router. Setiap file `route.ts` menangani HTTP method (GET, POST, PUT, DELETE) untuk modul tertentu. |
| `src/components/ui/` | Komponen UI dari shadcn/ui yang sudah dikonfigurasi. Komponen ini bersifat reusable dan konsisten menggunakan Radix UI primitives. |
| `src/hooks/` | Custom React hooks untuk logika yang digunakan berulang, seperti deteksi tema, ukuran layar, dan toast notification. |
| `src/store/` | Zustand store untuk state management global. Menyimpan state autentikasi, halaman aktif, bahasa, dan status sidebar dengan persistensi ke localStorage. |
| `src/lib/` | Modul shared yang berisi logika inti: koneksi database, autentikasi, i18n, type definitions, dan helper functions. Dipakai oleh API routes maupun komponen UI. |
| `src/middleware.ts` | Next.js middleware yang berjalan sebelum setiap request ke API. Berfungsi sebagai garis pertahanan pertama untuk validasi autentikasi dan otorisasi berdasarkan role. |
| `db/` | Berisi file database SQLite. Lokasi ini dikonfigurasi melalui `DATABASE_URL` di file `.env`. |

---

## 🚀 Instalasi

### Prasyarat

| Kebutuhan | Versi Minimum | Cara Cek |
|-----------|---------------|----------|
| Node.js | 18+ | `node --version` |
| Bun | 1.0+ (direkomendasikan) | `bun --version` |
| Git | 2.0+ | `git --version` |

> 💡 **Catatan:** Bun direkomendasikan untuk performa lebih cepat, tapi npm juga kompatibel.

### Langkah Instalasi

#### 1. Clone Repository

```bash
git clone <repository-url>
cd my-project
```

#### 2. Install Dependencies

```bash
bun install
```

#### 3. Konfigurasi Environment

```bash
# Salin file contoh environment
cp .env.example .env

# Edit .env sesuai kebutuhan (lihat section Environment Variables)
```

#### 4. Setup Database

```bash
# Push skema Prisma ke database (membuat tabel)
bun run db:push

# Generate Prisma Client
bun run db:generate
```

#### 5. Seed Database

```bash
# Isi database dengan data demo
# Opsi A: Via API endpoint
curl -X POST http://localhost:3000/api/seed

# Opsi B: Via Prisma seed
bunx prisma db seed
```

Data demo yang di-seed:
- 3 akun pengguna (1 admin, 2 approver)
- 10 kendaraan (5 penumpang, 5 barang)
- 8 driver
- 15 pemesanan dengan berbagai status
- Activity log entries

#### 6. Jalankan Development Server

```bash
bun run dev
```

Aplikasi berjalan di **http://localhost:3000**

#### 7. Production Build (Opsional)

```bash
# Build untuk produksi
bun run build

# Jalankan server produksi
bun run start
```

---

## 🔧 Environment Variables

Buat file `.env` di root project dengan konfigurasi berikut:

```env
# Database
DATABASE_URL="file:./db/custom.db"

# Autentikasi
NEXTAUTH_SECRET="your-secret-key-here"
NEXTAUTH_URL="http://localhost:3000"
```

### Penjelasan Variable

| Variable | Wajib | Penjelasan | Contoh |
|----------|:-----:|------------|--------|
| `DATABASE_URL` | ✅ | Connection string database. Format SQLite: `file:./path/to/db.db`. Untuk production, ganti ke PostgreSQL: `postgresql://user:pass@host:5432/db` | `file:./db/custom.db` |
| `NEXTAUTH_SECRET` | ✅ | Kunci rahasia untuk enkripsi session NextAuth. Gunakan nilai yang kuat dan unik di production. | `mining-vehicle-secret-key-2025` |
| `NEXTAUTH_URL` | ✅ | URL dasar aplikasi. Digunakan oleh NextAuth untuk redirect dan callback. Sesuaikan dengan domain di production. | `http://localhost:3000` |

### Contoh `.env.example`

```env
# Database - SQLite untuk development
DATABASE_URL="file:./db/custom.db"

# Database - PostgreSQL untuk production
# DATABASE_URL="postgresql://user:password@localhost:5432/miningco_fleet"

# NextAuth
NEXTAUTH_SECRET="change-this-to-a-secure-random-string"
NEXTAUTH_URL="http://localhost:3000"
```

> ⚠️ **Keamanan:** Jangan pernah commit file `.env` ke Git. Pastikan `.env` ada di `.gitignore`.

---

## 🔑 Akun Demo

Setelah seeding database, gunakan akun berikut untuk menguji aplikasi:

| Peran | Nama | Email | Kata Sandi |
|-------|------|-------|------------|
| 👨‍💼 Admin | Andi Pratama | admin@miningco.com | `admin123` |
| ✅ Approver L1 | Bambang Suryadi | approver1@miningco.com | `approver123` |
| ✅ Approver L2 | Citra Maharani | approver2@miningco.com | `approver123` |

### Panduan Testing

Untuk menguji alur kerja lengkap, ikuti langkah-langkah berikut:

1. **Login sebagai Admin** → Buat pemesanan baru
2. **Logout** → Login sebagai Approver L1 → Setujui pemesanan
3. **Logout** → Login sebagai Approver L2 → Setujui pemesanan
4. **Login sebagai Admin** → Mulai perjalanan → Selesaikan perjalanan
5. Cek **Laporan** dan **Log Aktivitas** untuk melihat seluruh catatan

---

## 🔒 Keamanan

Sistem menerapkan beberapa lapisan keamanan untuk melindungi data dan membatasi akses sesuai peran:

### 1. Role-Based Access Control (RBAC)

```
┌─────────────────────┐
│   Middleware Layer   │  ← Cek x-user-role header, tolak jika role tidak sesuai
├─────────────────────┤
│   Auth Helper Layer  │  ← Verifikasi user di database, cek isActive
├─────────────────────┤
│   Route Handler      │  ← Business logic validation
└─────────────────────┘
```

- **Middleware** memblokir request di level paling awal berdasarkan role
- **Auth Helper** (`requireAuth`, `requireAdmin`, `requireApprover`) memverifikasi identitas user di setiap route handler
- **Frontend** menyembunyikan menu dan tombol yang tidak sesuai role (defensive UI)

### 2. Password Hashing

- Kata sandi di-hash menggunakan **bcrypt** dengan salt rounds: 10
- Password plaintext **tidak pernah** disimpan di database
- Verifikasi login menggunakan `bcrypt.compare()` — tidak ada dekripsi

### 3. Protected API Routes

| Route | Method | Role yang Diizinkan |
|-------|--------|---------------------|
| `/api/vehicles` | GET | Admin |
| `/api/vehicles` | POST, PUT, DELETE | Admin |
| `/api/drivers` | GET | Admin |
| `/api/drivers` | POST, PUT, DELETE | Admin |
| `/api/reservations` | GET, POST, PUT, DELETE | Admin |
| `/api/approvals` | GET, POST | Approver |
| `/api/reports` | GET | Admin |
| `/api/activity-logs` | GET | Admin |
| `/api/dashboard` | GET | Admin, Approver |
| `/api/auth/*` | POST | Public |
| `/api/seed` | POST | Public |

### 4. Double Booking Prevention

Sistem melakukan validasi di level database query — bukan hanya di frontend. Saat membuat pemesanan baru, backend mengecek:

```typescript
// Cek apakah kendaraan sudah dipesan pada tanggal yang sama
const existingVehicle = await db.reservation.findFirst({
  where: {
    vehicleId,
    status: { in: ["PENDING_L1", "PENDING_L2", "APPROVED", "IN_PROGRESS"] },
    OR: [
      { startDate: { lte: endDate }, endDate: { gte: startDate } }
    ]
  }
})

// Cek apakah driver sudah ditugaskan pada tanggal yang sama
const existingDriver = await db.reservation.findFirst({
  where: {
    driverId,
    status: { in: ["PENDING_L1", "PENDING_L2", "APPROVED", "IN_PROGRESS"] },
    OR: [
      { startDate: { lte: endDate }, endDate: { gte: startDate } }
    ]
  }
})
```

### 5. Approval Authorization

- Approver hanya bisa memproses pemesanan pada **level yang sesuai** dengan `approvalLevel` mereka
- Approver L1 tidak bisa approve di level L2, dan sebaliknya
- Approver tidak bisa menyetujui pemesanan yang sudah diproses

### 6. Input Validation

- Backend melakukan validasi pada setiap input (required fields, format, range)
- Validasi kode kendaraan unik dan nomor SIM unik
- Validasi tanggal (endDate harus setelah startDate)

---

## 🌐 Dukungan Bahasa

Aplikasi mendukung dua bahasa secara penuh dengan sistem i18n custom:

| Aspek | Detail |
|-------|--------|
| Bahasa Tersedia | 🇮🇩 Bahasa Indonesia (default), 🇬🇧 English |
| Jumlah Translation Key | 440+ key per bahasa |
| Cara Penggantian | Klik toggle bahasa di navbar |
| Persistensi | Bahasa tersimpan di localStorage |
| Fallback | Jika key tidak ditemukan, fallback ke English |
| Format Tanggal | Otomatis menyesuaikan locale (id-ID / en-GB) |
| Header Ekspor | Header Excel menyesuaikan bahasa aktif |

---

## 📸 Screenshot

> Placeholder untuk screenshot aplikasi

### Login Page
<!-- ![Login Page](docs/screenshots/login.png) -->

### Dashboard Admin
<!-- ![Dashboard Admin](docs/screenshots/dashboard-admin.png) -->

### Dashboard Approver
<!-- ![Dashboard Approver](docs/screenshots/dashboard-approver.png) -->

### Manajemen Kendaraan
<!-- ![Vehicles](docs/screenshots/vehicles.png) -->

### Manajemen Driver
<!-- ![Drivers](docs/screenshots/drivers.png) -->

### Pemesanan Kendaraan
<!-- ![Reservations](docs/screenshots/reservations.png) -->

### Persetujuan Pemesanan
<!-- ![Approvals](docs/screenshots/approvals.png) -->

### Kalender Pemesanan
<!-- ![Calendar](docs/screenshots/calendar.png) -->

### Laporan & Ekspor
<!-- ![Reports](docs/screenshots/reports.png) -->

### Log Aktivitas
<!-- ![Activity Logs](docs/screenshots/activity-logs.png) -->

### Mode Gelap
<!-- ![Dark Mode](docs/screenshots/dark-mode.png) -->

---

## 🚢 Deployment

### Deploy ke Vercel (Direkomendasikan)

Vercel adalah platform deployment native untuk Next.js dengan konfigurasi minimal.

```bash
# 1. Install Vercel CLI
bun add -g vercel

# 2. Login
vercel login

# 3. Deploy
vercel

# Untuk production:
vercel --prod
```

**Environment Variables di Vercel:**

Set variabel berikut di dashboard Vercel → Settings → Environment Variables:

| Variable | Nilai |
|----------|-------|
| `DATABASE_URL` | `file:./db/custom.db` (SQLite) atau PostgreSQL URL |
| `NEXTAUTH_SECRET` | String acak yang kuat (min. 32 karakter) |
| `NEXTAUTH_URL` | `https://your-domain.vercel.app` |

### Deploy ke Railway

Railway mendukung database PostgreSQL dan deployment otomatis dari GitHub.

```bash
# 1. Hubungkan repository GitHub ke Railway
# 2. Tambahkan PostgreSQL database addon
# 3. Set environment variables
# 4. Railway otomatis build dan deploy
```

**Konfigurasi PostgreSQL di Railway:**

```env
DATABASE_URL="postgresql://postgres:password@host.railway.app:5432/railway"
NEXTAUTH_SECRET="generate-secure-random-string"
NEXTAUTH_URL="https://your-app.up.railway.app"
```

### Migrasi ke PostgreSQL (Production)

Untuk production, disarankan menggunakan PostgreSQL alih-alih SQLite:

```bash
# 1. Install PostgreSQL adapter
bun add @prisma/adapter-pg pg

# 2. Update prisma/schema.prisma
# Ganti: provider = "sqlite"
# Dengan:  provider = "postgresql"

# 3. Set DATABASE_URL ke PostgreSQL connection string

# 4. Push schema ke database baru
bun run db:push

# 5. Seed database
bunx prisma db seed
```

### Generate NEXTAUTH_SECRET yang Aman

```bash
# Menggunakan OpenSSL
openssl rand -base64 32

# Menggunakan Node.js
node -e "console.log(require('crypto').randomBytes(32).toString('base64'))"
```

---

## 📌 Status Proyek

| Aspek | Status |
|-------|--------|
| Fitur Utama | ✅ Selesai |
| Role-Based Access Control | ✅ Terimplementasi |
| Multi-Level Approval | ✅ Terimplementasi |
| Responsif (Mobile/Tablet/Desktop) | ✅ Terimplementasi |
| Dua Bahasa (ID/EN) | ✅ Lengkap |
| Dark Mode | ✅ Terimplementasi |
| Export Laporan | ✅ Terimplementasi |
| Audit Trail | ✅ Terimplementasi |
| Validasi Double Booking | ✅ Terimplementasi |
| Kualitas Code (Lint) | ✅ Lulus |
| Siap Technical Test | ✅ Ya |
| Siap Production | ✅ Ya (dengan PostgreSQL) |

---



