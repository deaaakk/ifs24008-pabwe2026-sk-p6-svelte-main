# Delcom Link Tree

Aplikasi web untuk membuat dan mengelola kumpulan tautan (Link Tree) menggunakan **Svelte 5**, **Vite**, dan **JavaScript**. Data diambil dari [Delcom Open API](https://open-api.delcom.org/docs/1.0/api-link-trees).

Proyek: `ifs24008-pabwe2026-sk-p6-svelte`
Repositori: https://github.com/deaaakk/ifs24008-pabwe2026-sk-p6-svelte-main

## Fitur

- **Autentikasi**: login, register, dan logout.
- **Link Tree**: tambah, ubah, hapus, dan hapus semua. Tipe `public`, `unlisted`, atau `private`.
- **Sampul (cover)**: unggah dan ubah sampul link tree.
- **Item tautan**: tambah, ubah, dan hapus item di dalam link tree.
- **Beranda**: daftar, pencarian, filter milik saya, dan statistik.
- **Pengguna & profil**: daftar pengguna, ubah data profil, foto, dan kata sandi.
- **Halaman 404** untuk path yang tidak dikenal.

## Teknologi

| Kebutuhan | Pustaka |
| --- | --- |
| Framework | Svelte 5 + Vite |
| Bahasa | JavaScript |
| Runtime / package manager | Bun |
| Styling | Tailwind CSS v4 |
| Ikon | lucide-svelte |
| Dialog | SweetAlert2 |
| Font | Plus Jakarta Sans |
| State | Svelte store (`writable` / `derived`) |
| Router | Router kustom berbasis History API |
| Pengujian | Vitest + Testing Library + jsdom |

## Prasyarat

- [Bun](https://bun.sh) terpasang.
- Akses ke Delcom Open API `https://open-api.delcom.org/api/v1`.

## Instalasi

```bash
git clone https://github.com/deaaakk/ifs24008-pabwe2026-sk-p6-svelte-main
cd ifs24008-pabwe2026-sk-p6-svelte
bun install
```

## Konfigurasi Lingkungan

Salin `.env.example` menjadi `.env`, lalu isi seperti berikut:

```ini
VITE_DELCOM_BASEURL=https://open-api.delcom.org/api/v1
APP_PORT=3004
```

## Menjalankan Aplikasi

| Perintah | Fungsi |
| --- | --- |
| `bun run dev` | Mode pengembangan di http://localhost:3004 |
| `bun run build` | Build produksi |
| `bun run preview` | Menjalankan hasil build produksi |
| `bun run test` | Menjalankan seluruh pengujian |
| `bun run test:watch` | Pengujian mode watch |
| `bun run test:coverage` | Pengujian dengan laporan coverage |

> Gunakan `bun run test` atau `bun x vitest run`. Jangan memakai `bun test`.

## Struktur Proyek

```
src/
├── App.svelte
├── App.test.js
├── index.css
├── main.js
├── router.js
├── router.test.js
├── setupTests.js
├── test-utils.js
├── features/
│   ├── auth/
│   │   ├── api/
│   │   ├── layouts/        # AuthLayout.svelte
│   │   ├── pages/          # LoginPage, RegisterPage
│   │   └── states/         # authStore.js
│   ├── common/
│   │   └── pages/          # NotFoundPage.svelte
│   ├── linktrees/
│   │   ├── api/            # linkTreeApi.js
│   │   ├── components/     # navbar, sidebar
│   │   ├── layouts/        # LinkTreeLayout.svelte
│   │   ├── modals/         # AddModal, ChangeModal, ChangeCoverModal, ItemModal
│   │   ├── pages/          # HomePage, DetailPage
│   │   └── states/         # linkTreesStore.js
│   └── users/
│       ├── api/
│       ├── pages/
│       └── states/
├── helpers/                # apiHelper.js, toolsHelper.js
└── hooks/                  # useInput.js
```

## Rute

| Path | Halaman | Layout |
| --- | --- | --- |
| `/auth/login` | Login | Autentikasi |
| `/auth/register` | Register | Autentikasi |
| `/` | Daftar link tree | Link Tree |
| `/link-trees/:linkTreeId` | Detail link tree | Link Tree |
| `/users` | Daftar pengguna | Link Tree |
| `/profile` | Profil | Link Tree |
| lainnya | 404 | - |

## Endpoint API

Respons dianggap berhasil bila `status` bernilai `"success"`. Header otorisasi: `Authorization: Bearer <token>`.

| Metode | Endpoint | Keterangan |
| --- | --- | --- |
| POST | `/auth/login`, `/auth/register` | Autentikasi |
| GET | `/users` | Daftar pengguna |
| GET / PUT | `/users/me` | Profil sendiri |
| POST | `/link-trees` | Tambah link tree (`title`, `type`, `description`) |
| POST | `/link-trees/:id/cover` | Unggah sampul (berkas `cover`) |
| GET | `/link-trees`, `/link-trees/:id` | Daftar (`data.link_trees`) dan detail (`data.link_tree` + `items`) |
| PUT | `/link-trees/:id` | Ubah link tree |
| DELETE | `/link-trees/:id`, `/link-trees` | Hapus satu / hapus semua |
| POST / PUT / DELETE | `/link-trees/:id/items` | Kelola item tautan |

## Pengujian

Coverage wajib **100%** untuk `statements`, `branches`, `functions`, dan `lines`.

```bash
bun run test:coverage
```

Pengujian mencakup helper, hook, API, store, navbar, sidebar, layout, modal, halaman, router, dan `App.svelte`.

## Lisensi

Proyek ini dibuat untuk keperluan praktikum PABWE 2026 (Pertemuan 6).