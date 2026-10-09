<div align="center">

# Delcom Auction

**Aplikasi lelang daring berbasis Vue 3 dengan manajemen state Pinia dan antarmuka Tailwind CSS v4.**

![Vue](https://img.shields.io/badge/Vue-3-42b883?style=flat-square&logo=vuedotjs&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-Build_Tool-646cff?style=flat-square&logo=vite&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-v4-38bdf8?style=flat-square&logo=tailwindcss&logoColor=white)
![Pinia](https://img.shields.io/badge/Pinia-State_Management-f7d336?style=flat-square)
![Bun](https://img.shields.io/badge/Bun-Runtime-000000?style=flat-square&logo=bun&logoColor=white)
![Vitest](https://img.shields.io/badge/Vitest-100%25_Coverage-6e9f18?style=flat-square&logo=vitest&logoColor=white)

[Demo Langsung](https://ifs24024-pabwe2026-sk-p5-vue.netlify.app) | [Dokumentasi API](https://open-api.delcom.org/docs/1.0/api-aucations)

</div>

---

## Ringkasan

Delcom Auction adalah aplikasi web lelang yang memungkinkan pengguna membuat lelang barang, mengajukan penawaran (bid), dan mengelola profil akun. Seluruh data bersumber dari REST API Delcom Auction. Kode disusun dengan arsitektur berbasis fitur (feature-based architecture) sehingga setiap domain, yaitu autentikasi, pengguna, dan lelang, memiliki lapisan API, state, layout, komponen, dan halaman tersendiri.

Proyek ini merupakan tugas mata kuliah Pengembangan Aplikasi Web (PABWE) 2026, Studi Kasus 1, Praktikum 5 (VueJS).

## Informasi Pengembang

| Keterangan | Detail |
| --- | --- |
| Nama | lysonmnk |
| ID | ifs24024 |
| Mata Kuliah | Pengembangan Aplikasi Web (PABWE) 2026 |
| Repositori | `ifs24024-pabwe2026-sk-p5-vue` |
| Demo | https://ifs24024-pabwe2026-sk-p5-vue.netlify.app |

## Daftar Isi

- [Fitur](#fitur)
- [Teknologi](#teknologi)
- [Arsitektur](#arsitektur)
- [Memulai](#memulai)
- [Konfigurasi Environment](#konfigurasi-environment)
- [Skrip yang Tersedia](#skrip-yang-tersedia)
- [Pengujian](#pengujian)
- [Struktur Proyek](#struktur-proyek)
- [Pemetaan Rute](#pemetaan-rute)
- [Referensi Endpoint API](#referensi-endpoint-api)
- [Deployment](#deployment)
- [Lisensi](#lisensi)

## Fitur

**Autentikasi**
- Registrasi akun dan login pengguna.
- Token akses disimpan di `localStorage` dan dilampirkan otomatis pada setiap permintaan melalui header `Authorization: Bearer <token>`.
- Validasi formulir dan dialog konfirmasi menggunakan SweetAlert2.

**Profil dan Pengguna**
- Direktori seluruh pengguna terdaftar.
- Pembaruan data profil, unggah foto avatar, dan penggantian kata sandi.

**Lelang**
- Dashboard dengan filter: Semua Lelang, Lelang Saya, Lelang Berlangsung, dan Lelang Ditutup.
- Pencarian langsung (live search) berdasarkan judul dan deskripsi.
- Pembuatan, pengubahan, dan penghapusan lelang, termasuk penggantian foto cover dengan pratinjau.
- Deskripsi barang berformat Markdown melalui Toast UI Editor.
- Pengajuan dan pembatalan bid dengan validasi bahwa nominal harus lebih tinggi dari penawaran tertinggi.
- Halaman detail yang memuat cover, deskripsi, dan riwayat penawaran.
- Penghapusan seluruh lelang milik pengguna.

**Kualitas Kode**
- Pengujian unit dan integrasi dengan Vitest dan Testing Library.
- Ambang batas coverage 100% menggunakan provider v8.

## Teknologi

| Kategori | Teknologi |
| --- | --- |
| Runtime dan Package Manager | Bun |
| Framework | Vue 3 (JavaScript) |
| Build Tool | Vite |
| State Management | Pinia |
| Routing | Vue Router |
| Styling | Tailwind CSS v4 melalui `@tailwindcss/vite` |
| Ikon | lucide-vue-next |
| Tipografi | Plus Jakarta Sans (Google Fonts) |
| Dialog | SweetAlert2 |
| Editor Markdown | @toast-ui/editor |
| Pengujian | Vitest, jsdom, Testing Library, jest-dom |
| CI | Jenkins (`Jenkinsfile`) |

## Arsitektur

Aplikasi mengikuti pola berlapis pada setiap fitur:

```text
Page / Component  ->  Pinia Store  ->  API Module  ->  apiHelper  ->  Delcom REST API
```

| Lapisan | Tanggung Jawab |
| --- | --- |
| Page dan Component | Presentasi, interaksi pengguna, dan validasi formulir |
| Store (Pinia) | State reaktif, status loading dan mutasi, serta aksi asinkron |
| API Module | Definisi pemanggilan endpoint per fitur |
| Helper | Wrapper `fetch`, pengelolaan token, notifikasi, dan pemformatan |
| Hook | Logika reusable, misalnya `useInput` untuk two-way binding formulir |

## Memulai

### Prasyarat

- [Bun](https://bun.sh) versi terbaru
- [Git](https://git-scm.com)

### Instalasi

```bash
git clone https://github.com/lysonmnk/ifs24024-pabwe2026-sk-p5-vue.git
cd ifs24024-pabwe2026-sk-p5-vue
bun install
```

Salin berkas environment:

```bash
# macOS / Linux
cp .env.example .env

# Windows (Command Prompt)
copy .env.example .env
```

Jalankan server pengembangan:

```bash
bun run dev
```

Aplikasi dapat diakses pada `http://localhost:<APP_PORT>`.

## Konfigurasi Environment

| Variabel | Deskripsi | Contoh |
| --- | --- | --- |
| `VITE_DELCOM_BASEURL` | Base URL REST API Delcom | `https://open-api.delcom.org/api/v1` |
| `APP_PORT` | Port server pengembangan lokal | `5173` |

Contoh berkas `.env`:

```env
VITE_DELCOM_BASEURL=https://open-api.delcom.org/api/v1
APP_PORT=5173
```

Konstanta `DELCOM_BASEURL` juga didefinisikan pada `vite.config.js` dan diarahkan ke `https://open-api.delcom.org/api/v1`.

## Skrip yang Tersedia

| Perintah | Fungsi |
| --- | --- |
| `bun run dev` | Menjalankan server pengembangan |
| `bun run build` | Membuat build produksi ke direktori `dist` |
| `bun run preview` | Pratinjau hasil build produksi |
| `bun run test` | Menjalankan seluruh pengujian |
| `bun run test:coverage` | Menjalankan pengujian beserta laporan coverage |

Nama skrip mengikuti bagian `scripts` pada `package.json`.

## Pengujian

Lingkungan pengujian menggunakan Vitest dengan `jsdom`. Berkas `src/setupTests.js` memuat konfigurasi `@testing-library/jest-dom`, sedangkan `src/test-utils.js` menyediakan `renderWithProviders` dan `createMockPinia` untuk merender komponen dengan Pinia dan router berbasis memori.

Cakupan pengujian:

| Area | Contoh Modul |
| --- | --- |
| Helper dan hook | `apiHelper`, `toolsHelper`, `useInput` |
| API | `authApi`, `userApi`, `aucationApi` |
| Store | `authStore`, `usersStore`, `aucationsStore` |
| Komponen | Navbar, Sidebar, Markdown Editor dan Viewer, seluruh modal |
| Layout dan halaman | `AuthLayout`, `AucationLayout`, seluruh page |
| Integrasi | `App.test.js` |

Coverage dikonfigurasi dengan threshold 100% (provider v8). Proses pengujian akan gagal apabila cakupan berada di bawah ambang batas.

## Struktur Proyek

```text
.
├── public/
├── src/
│   ├── features/
│   │   ├── auth/
│   │   │   ├── api/               authApi.js
│   │   │   ├── layouts/           AuthLayout.vue
│   │   │   ├── pages/             LoginPage.vue, RegisterPage.vue
│   │   │   └── states/            authStore.js
│   │   ├── users/
│   │   │   ├── api/               userApi.js
│   │   │   ├── pages/             UsersPage.vue, ProfilePage.vue
│   │   │   └── states/            usersStore.js
│   │   ├── aucations/
│   │   │   ├── api/               aucationApi.js
│   │   │   ├── components/        NavbarComponent, SidebarComponent,
│   │   │   │                      MarkdownEditor, MarkdownViewer
│   │   │   │   └── modals/        AddModal, ChangeModal,
│   │   │   │                      ChangeCoverModal, BidModal
│   │   │   ├── layouts/           AucationLayout.vue
│   │   │   ├── pages/             HomePage.vue, DetailPage.vue
│   │   │   └── states/            aucationsStore.js
│   │   └── common/
│   │       └── pages/             NotFoundPage.vue
│   ├── helpers/                   apiHelper.js, toolsHelper.js
│   ├── hooks/                     useInput.js
│   ├── App.vue
│   ├── index.css
│   ├── main.js
│   ├── router.js
│   ├── setupTests.js
│   └── test-utils.js
├── .env.example
├── Jenkinsfile
├── index.html
├── package.json
└── vite.config.js
```

## Pemetaan Rute

| Path | Komponen | Akses | Deskripsi |
| --- | --- | --- | --- |
| `/auth/login` | `LoginPage` | Publik | Halaman login |
| `/auth/register` | `RegisterPage` | Publik | Halaman registrasi |
| `/` | `HomePage` | Terproteksi | Daftar dan filter lelang |
| `/aucations/:aucationId` | `DetailPage` | Terproteksi | Detail lelang dan riwayat bid |
| `/users` | `UsersPage` | Terproteksi | Direktori pengguna |
| `/profile` | `ProfilePage` | Terproteksi | Profil dan pengaturan akun |
| `/:pathMatch(.*)*` | `NotFoundPage` | Publik | Halaman 404 |

Rute `/auth` menggunakan `AuthLayout`, sedangkan rute terproteksi menggunakan `AucationLayout`.

## Referensi Endpoint API

Base URL: `https://open-api.delcom.org/api/v1`

**Autentikasi**

| Metode | Endpoint | Deskripsi |
| --- | --- | --- |
| POST | `/auth/register` | Registrasi akun baru |
| POST | `/auth/login` | Login pengguna |

**Pengguna**

| Metode | Endpoint | Deskripsi |
| --- | --- | --- |
| GET | `/users` | Daftar pengguna |
| GET | `/users/me` | Profil pengguna aktif |
| PUT | `/users/me` | Pembaruan profil |
| POST | `/users/me/photo` | Unggah foto avatar |
| PUT | `/users/me/password` | Penggantian kata sandi |

**Lelang**

| Metode | Endpoint | Deskripsi |
| --- | --- | --- |
| GET | `/aucations` | Daftar lelang, dengan filter `is_me` dan `is_closed` |
| GET | `/aucations/:id` | Detail lelang |
| POST | `/aucations` | Tambah lelang (`title`, `description`, `start_bid`, `closed_at`) |
| PUT | `/aucations/:id` | Ubah lelang |
| POST | `/aucations/:id/cover` | Unggah atau ganti cover |
| DELETE | `/aucations/:id` | Hapus lelang |
| POST | `/aucations/:id/bids` | Ajukan bid |
| DELETE | `/aucations/:id/bids` | Batalkan bid |
| DELETE | `/aucations` | Hapus seluruh lelang milik pengguna |

Dokumentasi lengkap: https://open-api.delcom.org/docs/1.0/api-aucations

## Deployment

Aplikasi telah dipublikasikan di Netlify dan terhubung dengan repositori GitHub ini.

| Pengaturan | Nilai |
| --- | --- |
| Build command | `bun run build` |
| Publish directory | `dist` |
| Environment variable | `VITE_DELCOM_BASEURL` |

Karena aplikasi merupakan single-page application dengan Vue Router, tambahkan aturan pengalihan agar rute langsung (misalnya `/profile`) tidak menghasilkan 404. Buat berkas `public/_redirects` dengan isi:

```text
/*    /index.html   200
```

## Lisensi

Proyek ini dibuat untuk keperluan akademik. Hak cipta atas kode pada repositori ini dimiliki oleh lysonmnk (ifs24024).
