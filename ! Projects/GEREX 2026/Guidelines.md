## 🚀 Tech Stack
Aplikasi ini menggunakan kombinasi teknologi modern untuk performa, kemudahan pengembangan, serta pengalaman pengguna yang optimal:
### Frontend & UI
*   **React 19**: Framework antarmuka komponen berbasis state terbaru.
*   **Vite 8**: Tooling build super cepat untuk web modern.
*   **TypeScript**: Menjamin keandalan tipe data di seluruh codebase.
*   **Tailwind CSS v4 (Alpha/Beta)**: Utilitas CSS generasi terbaru dengan compiler ultra-cepat `@tailwindcss/vite`.
*   **Framer Motion & GSAP (GreenSock)**: Pustaka animasi kelas industri untuk transisi halaman dan mikro-interaksi yang interaktif.
*   **Radix UI & Shadcn UI**: Fondasi komponen UI yang aksesibel, unstyled/headless, dan dapat dikustomisasi dengan bebas.
*   **React Router DOM v7**: Pengelolaan routing di sisi klien dengan dukungan lazy loading/code splitting.
*   **Zustand & Immer**: State management global yang ringan dan efisien, dikombinasikan dengan Immer untuk pengelolaan state immutable yang mudah.
*   **React Hook Form & Zod**: Penanganan form dan validasi skema tipe data secara deklaratif.
### PWA & Offline Support
*   **Vite PWA Plugin**: Mengonfigurasi aplikasi sebagai Progressive Web App (PWA).
*   **Custom Service Worker (`sw.ts`)**: Penanganan caching taktis (pre-caching bundle besar hingga 5MB) dan fungsionalitas offline.
*   **idb-keyval**: Utilitas ringan untuk berinteraksi dengan IndexedDB untuk penyimpanan lokal persisten.
### Backend & Database
*   **Convex**: Database serverless real-time yang mengintegrasikan query, mutasi, aksi (actions), dan skema basis data langsung dengan TypeScript secara aman.
*   **Hono**: Framework web minimalis untuk penanganan routing API/edge functions.
*   **Cloudflare Pages & Workers (Wrangler)**: Platform deployment edge serverless berlatensi rendah.
### Perkakas (Tooling) & QA
*   **Bun**: Runtime JavaScript dan package manager berkecepatan tinggi (menggunakan berkas lock `bun.lock`).
*   **Biome**: Linter dan formatter modern terintegrasi berkecepatan tinggi yang menggantikan peran ESLint dan Prettier.
---
## 📂 Struktur Project (Project Directory Structure)
Berikut adalah tata letak folder di dalam project:
```text
GEREX-2026/
├── .agents/                 # Kustomisasi lokal untuk asisten AI
├── .github/                 # Alur kerja GitHub Actions (CI/CD)
├── .husky/                  # Git hooks untuk memicu Biome check sebelum commit
├── convex/                  # Direktori Backend & Database (Convex)
│   ├── _generated/          # Tipe data & modul klien auto-generated dari Convex
│   ├── adminAuth.ts         # Mutasi & query untuk otentikasi admin
│   ├── adminAuthActions.ts  # Aksi aman (seperti enkripsi/verifikasi bcrypt)
│   ├── blocks.ts            # Skrip pengelolaan data blok halaman dinamis (CMS)
│   ├── editions.ts          # Pengelolaan edisi event (aktif/arsip)
│   ├── health.ts            # Pemeriksaan kesehatan API
│   ├── members.ts           # Skrip pengelolaan data anggota panitia
│   ├── navSections.ts       # Navigasi sidebar dinamis
│   ├── pages.ts             # Metadata halaman dinamis
│   ├── schema.ts            # Skema tabel & indeks basis data utama
│   ├── seed.ts              # Seeder data awal & data dummy
│   ├── staffAnnouncements.ts# Data pengumuman kelulusan staff
│   └── tsconfig.json        # Konfigurasi TS khusus direktori Convex
├── public/                  # Aset statis public (gambar, ikon PWA, manifest)
├── src/                     # Source Code Aplikasi Utama (React)
│   ├── app/                 # Pengaturan global (seperti font kustom)
│   ├── components/          # Komponen UI modular
│   │   ├── admin/           # Dashboard manajemen, sidebar admin, auth session provider
│   │   ├── announcement/    # Hasil pengumuman (Accepted/Rejected) & sistem pencarian
│   │   ├── blocks/          # Blok UI modular (Hero, Grid, Card, SOP, dll.) untuk CMS
│   │   ├── editor/          # Komponen editor visual untuk memanipulasi konten halaman
│   │   ├── layout/          # Layout layout global seperti Sidebar & Topbar publik
│   │   ├── shared/          # Komponen pakai ulang (Typography, Image, Button, dll.)
│   │   └── ui/              # Komponen dasar (Shadcn UI primitives)
│   ├── hooks/               # Custom hooks React (PWA, interaksi UI, dll.)
│   ├── lib/                 # Utilitas global (validasi, helper data, parser Excel)
│   │   ├── blocks/          # Utilitas pendukung tata letak blok
│   │   ├── excel/           # Utilitas parse file `.xlsx` untuk batch upload data
│   │   └── utils.ts         # Helper tailwind merging & classnames (`cn`)
│   ├── pages/               # Tampilan halaman utama (Lazy Loaded)
│   ├── types/               # Berkas deklarasi tipe data TypeScript tambahan
│   ├── App.tsx              # Pusat konfigurasi routing, layout pelindung admin & provider
│   ├── globals.css          # Entri stylesheet utama (Tailwind v4 directive & custom rules)
│   ├── main.tsx             # Titik entri rendering aplikasi React
│   ├── providers.tsx        # Inisialisasi klien Convex & pembungkus provider
│   └── sw.ts                # Kode Service Worker untuk PWA
├── biome.json               # Konfigurasi linter & formatter Biome
├── bun.lock                 # Berkas lock dependensi Bun
├── index.html               # Berkas HTML template utama
├── package.json             # Manifes dependensi & script project
├── tsconfig.json            # Konfigurasi kompiler TypeScript global
├── vite.config.ts           # Konfigurasi bundler Vite dengan plugin PWA & Tailwind v4
└── wrangler.jsonc           # Konfigurasi deployment aset SPA di Cloudflare Pages
```
---
## 🛠️ Fitur & Arsitektur Utama
### 1. Modular CMS Page Builder
Halaman seperti `/coming-soon`, `/resonator-karsa`, `/gema-karsa`, dan `/survival-kit/:slug` tidak bersifat statis, melainkan dirender secara dinamis dari database.
*   **Blok Registri (`src/components/blocks/registry.tsx`)**: Menghubungkan tipe blok dari database (seperti `hero`, `ukmGrid`, `sopSection`, `warningBox`) ke komponen React masing-masing.
*   **Dynamic Fetching**: Setiap halaman mengambil data blok terurut berdasarkan ID halaman, memvalidasinya, kemudian merendernya secara berurutan menggunakan fungsi `renderBlock`.
### 2. Sistem Pencarian Pengumuman Staff (Staff Recruitment Announcement)
Menampilkan status penerimaan panitia/staff dengan UI yang interaktif dan memanjakan mata:
*   Mendukung pencarian berbasis nama atau NIM/NRP mahasiswa baru.
*   **Accepted State**: Menampilkan animasi confetti (`canvas-confetti`), detail sub-divisi yang diterima, serta tombol kontak WhatsApp CP yang langsung mengarah ke narahubung divisi tersebut.
*   **Rejected State**: Menampilkan pesan penyemangat dan ajakan berproses di tempat lain dengan visualisasi yang ramah.
### 3. UKM Finder (Pencari UKM)
Kuis rekomendasi minat bakat untuk mahasiswa baru untuk menemukan unit kegiatan mahasiswa (UKM) yang cocok dengan preferensi mereka:
*   Kuisioner interaktif berbasis pertanyaan berbobot.
*   Kalkulasi persentase kecocokan di sisi database/klien yang memetakan kecenderungan jawaban ke rumpun kategori UKM (Olahraga, Seni, Bela Diri, Bidang Khusus).
### 4. Admin Panel & Excel Batch Uploads
Dashboard administratif yang aman untuk mengelola data operasional orientasi:
*   **Otentikasi Admin**: Menggunakan session berbasis hash token unik yang disimpan di `localStorage` dan divalidasi ke tabel `adminSessions` di Convex.
*   **Batch Upload**: Menggunakan `exceljs` (`src/lib/excel/parse.ts`) untuk mengunggah ratusan hingga ribuan data kelulusan staff atau data Maba secara instan dari spreadsheet Excel langsung ke database Convex.
---
## 🏃 Cara Menjalankan Project Secara Lokal
Ikuti langkah-langkah berikut untuk memulai development server di lokal Anda:
1.  **Instalasi Dependensi**
    Pastikan Anda telah memasang **Bun** di komputer Anda, lalu jalankan:
    ```bash
    bun install
    ```
2.  **Jalankan Backend (Convex Dev)**
    Untuk menyambungkan database lokal Anda ke cloud deployment Convex (atau membuat instance baru), jalankan perintah berikut di terminal terpisah:
    ```bash
    bun run convex:dev
    ```
    *Perintah ini akan membuat berkas `.env.local` secara otomatis dengan konfigurasi `VITE_CONVEX_URL` yang dibutuhkan.*
3.  **Jalankan Frontend (Vite Dev Server)**
    Setelah database terhubung, jalankan development server frontend:
    ```bash
    bun run dev
    ```
    Aplikasi akan berjalan di alamat `http://localhost:5173` secara default.
4.  **Menyemai Data Dummy (Seeding)**
    Jika Anda memerlukan data dummy untuk keperluan development atau demo CMS dan UKM Finder, jalankan perintah seeder berikut:
    ```bash
    bun run seed
    ```
5.  **Memeriksa Kualitas Kode (Linting/Formatting)**
    Gunakan Biome untuk mendeteksi error penulisan dan merapikan format berkas otomatis:
    ```bash
    bun run check        # Memeriksa isu kode
    bun run check:write  # Memeriksa dan memperbaiki isu kode otomatis
    ```
